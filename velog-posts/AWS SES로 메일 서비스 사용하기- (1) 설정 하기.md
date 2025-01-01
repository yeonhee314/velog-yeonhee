<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/ca458a4d-5b23-4814-95a6-d2d6a97ad7c5/image.gif" /></p>
<h4 id="현재-개발중인-프로젝트의-상태-ui는-매일메일을-많이-참고했습니다-최고의-선배님들">(현재 개발중인 프로젝트의 상태...) UI는 <a href="https://www.maeil-mail.kr/">매일메일</a>을 많이 참고했습니다. 최고의 선배님들...!!!</h4>
<br />
구독한 사용자의 DB에 저장하는 기능까지 완료 했고,
이제 구독한 사용자에게 메일 보내는 기능을 구현해야 한다.
그런데 메일을 보내는 기능 관련해서 고민이 생겼다.
<br />

<p>Spring Boot에서 이메일을 보내는 방법은 Java Mail Sender를 사용하는 것이 일반적인데 
구글을 떠돌며 알아보다가 <strong>AWS SES</strong> 서비스를 알게 되었다.</p>
<p><br /><br /><br /></p>
<h2 id="💡-aws-ses란">💡 AWS SES란?</h2>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/5cfb4233-a943-45d1-aac0-1389951d6769/image.png" /></p>
<blockquote>
<p>SES는 Simple Email Service의 약자로 AWS(Amazone Web Service)의 Email 전송 서비스를 이용할 수 있는 라이브러리이다. </p>
</blockquote>
<p>대량 이메일 발송에 최적화 되어있고, 이메일 수신, 통계 및 분석 등 고급 기능을 제공한다.
서비스 이용자가 많아진다면 대규모 이메일 발송과 더불어 안정성을 위해 AWS SES를 많이 사용 한다.</p>
<p><br /><br /></p>
<h2 id="💡-aws-ses와-java-mail-sender의-차이점">💡 AWS SES와 Java Mail Sender의 차이점</h2>
<table border="1" cellpadding="10">
  <thead>
    <tr>
      <th>특징</th>
      <th>AWS SES</th>
      <th>Java Mail Sender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>성격</strong></td>
      <td>관리형 클라우드 서비스</td>
      <td>Java 라이브러리</td>
    </tr>
    <tr>
      <td><strong>설정</strong></td>
      <td>AWS 콘솔에서 설정, API 또는 SMTP 사용</td>
      <td>JavaMail API를 사용하여 SMTP 설정 필요</td>
    </tr>
    <tr>
      <td><strong>규모</strong></td>
      <td>대량 이메일 발송에 적합</td>
      <td>소규모 이메일 발송에 적합</td>
    </tr>
    <tr>
      <td><strong>확장성</strong></td>
      <td>고도화된 확장성, 자동화된 서비스 제공</td>
      <td>직접 서버를 설정하고 관리해야 함</td>
    </tr>
    <tr>
      <td><strong>이메일 발송</strong></td>
      <td>대량 발송, 트랜잭션 이메일, 마케팅 이메일</td>
      <td>기본적인 이메일 발송</td>
    </tr>
    <tr>
      <td><strong>기타 기능</strong></td>
      <td>이메일 인증, 스팸 방지, 분석 기능 제공</td>
      <td>기본적인 이메일 전송 기능만 제공</td>
    </tr>
    <tr>
      <td><strong>비용</strong></td>
      <td>사용량에 따라 과금</td>
      <td>자체 SMTP 서버 또는 다른 서비스 제공자에 의존</td>
    </tr>
  </tbody>
</table>

<p>볼륨이 크지 않은 개인프로젝트라서 <strong>Java Mail Sender</strong>를 사용하는 것도 나쁘지 않은 선택이지만... </p>
<p><em>개발자는 원래 개척자니까요.</em>...😎</p>
<p><br /><br /><br /></p>
<h2 id="💡-aws-ses-이메일-전송-작동-방식">💡 AWS SES 이메일 전송 작동 방식</h2>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/e15f2f22-a318-4809-8378-fb0a2169b5c5/image.png" /></p>
<blockquote>
<ol>
<li>이메일 발신자 역할을 하는 클라이언트 애플리케이션은 SES에 한 명 이상의 수신자에게 이메일을 보내달라고 요청한다.</li>
<li>요청이 유효하면 SES는 이메일을 수락한다.</li>
<li>SES는 인터넷을 통해 수신자의 수신자에게 메시지를 보낸다. 메시지가 SES에 전달되면 일반적으로 즉시 전송되고 첫 번째 전달 시도는 일반적으로 밀리초 이내에 발생한다.</li>
<li>이 시점에서 여러가지 가능성이 있다. 예) :
ㄱ. ISP가 메시지를 수신자의 받은 편지함으로 성공적으로 전달 한다.
ㄴ. 수신자의 이메일 주소가 존재하지 않으므로 ISP가 SES에 반송 알림을 보낸다. 그러면 SES가 알림을 발신자에게 전달한다.
ㄷ. 수신자는 메시지를 받지만 스팸으로 간주하여 ISP에 불만을 등록한다. SES와 피드백 루프를 설정한 ISP는 불만을 SES로 보내고 SES는 이를 발신자에게 전달한다.</li>
</ol>
</blockquote>
<br />

<p><strong>하루에 2000통까지는 프리티어로도 가능</strong>하기 때문에
이메일 분석 기능을 이용할 수 있는 AWS SES를 사용해 보는 것도 좋은 경험이 될 것 같다.
<br /></p>
<hr />

<p><a href="https://aws.amazon.com/ko/ses/getting-started/">Amazon SES 시작하기</a></p>
<h2 id="💡-aws-ses-사용-하기">💡 AWS SES 사용 하기</h2>
<h3 id="1-이메일-인증">1. 이메일 인증</h3>
<p>우선 프리티어로 AWS에 가입을 하고, 이메일을 인증받아야 한다.</p>
<p><strong>AWS SES는 등록된 이메일 주소에서만 메일을 보낼 수 있기 때문</strong>에
사용하려면 보내는 이메일과 도메인을 등록하고 인증해야한다.
<img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/4bf09f5b-f70d-42dc-b5a9-b9c6b231bc0f/image.png" />
Amazon SES에서 설정 시작을 눌러 유저에게 보낼 이메일 주소를 추가 한다.</p>
<h3 id="2-도메인-인증">2. 도메인 인증</h3>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/1499b24b-2dd9-450c-a3bb-5068fb5a221e/image.png" /></p>
<p><em>어랍쇼......?! 저는 도메인이 없는데요..!</em>
<img src="https://velog.velcdn.com/images/yeonhee314/post/54294eb1-946f-4233-9451-23f7d20adbea/image.png" width="20%" /></p>
<p>2단계에서 문제가 생겼다. 
나는 현재 프로젝트를 개발 중이기 때문에 도메인이 <code>localhost</code> 이다. </p>
<p><code>localhost</code>인 경우, 실제 인터넷 상에서 접근할 수 있는 도메인이 아니기 때문에 인증된 도메인으로 처리할 수 없다.</p>
<p>로컬 개발 환경에서 이메일을 테스트 하려면 <strong>AWS SES의 샌드박스 모드</strong>를 사용해야 한다. </p>
<p>프로덕션 액세스 요청을 할 때 이 포스트는 추가로 업데이트를 해야할 것 같다.
<br /></p>
<hr />
<h2 id="💡-샌드박스-모드란">💡 샌드박스 모드란?</h2>
<blockquote>
<p>도용 및 침해를 방지하기 위해 신규 Amazon SES 계정에 대해 제한이 걸려있는 상태이다. 
샌드박스 환경에서는 Amazone SES에서 제공하는 모든 기능을 사용할 수 있지만, 특정 전송 제한 및 제한 사항이 적용 된다.</p>
</blockquote>
<p>샌드박스가 걸려있다면 자격 증명으로 등록되어 있지 않은 계정에는 메일을 보낼 수가 없다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/eab496cf-6d3b-44e2-950f-c74fd01b30c3/image.png" /></p>
<p>샌드박스 상태에서는 아주 제한된 사용만 가능하다.</p>
<blockquote>
<ol>
<li><strong>하루에 200개의 메일</strong>만 보낼 수 있다.</li>
<li><strong>등록된 사용자에 한해서만</strong> 주고 받는 것이 가능하다.</li>
</ol>
</blockquote>
<p>현재 나는 프로덕트 상태가 아니므로 샌드박스 모드로 진행해보려고 한다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/f57ff113-3419-40f2-864e-1502d9c380a9/image.png" />
왼쪽 메뉴의 자격 증명을 눌러 자격 증명을 생성한다.
이메일 주소를 선택하고 이메일을 입력한 후에 <strong>[자격 증명 생성]</strong>을 클릭하면 해당 이메일로 메일이 온다.
<br /></p>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/66524003-d3e5-42b5-a35c-8a24dcea208f/image.png" /></p>
<p>그 때, 링크를 클릭해주면 승인이 된다.
이메일을 클릭하고 들어간 뒤에는 테스트도 가능 하다.</p>
<p><br /><br /><br /><br /></p>
<hr />
<p>개인적으로 공부하며 작성하는 게시물입니다.
혹시 잘못된 정보가 있거나, 질문은 편하게 댓글 달아주세요.
감사합니다😊</p>
<br />

<p><strong>출처/참고한 글</strong>
<a href="https://docs.aws.amazon.com/ses/latest/dg/send-email-concepts-process.html">Amazon SES에서 이메일 전송이 작동하는 방식</a>
<a href="https://velog.io/@korea3611/aws-ses-%EB%A5%BC-%EC%82%AC%EC%9A%A9%ED%95%98%EC%97%AC-%EB%A9%94%EC%9D%BC%EC%9D%84-%EB%B3%B4%EB%82%B4%EB%B3%B4%EC%9E%90">[Spring Boot] AWS SES를 사용하여 메일을 보내보자</a></p>