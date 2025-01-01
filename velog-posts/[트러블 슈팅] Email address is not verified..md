<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/16e9b770-96c4-4d33-9c10-ec4c8d53721d/image.png" /></p>
<p><a href="https://velog.io/@yeonhee314/AWS-SES%EB%A1%9C-%EB%A9%94%EC%9D%BC-%EC%84%9C%EB%B9%84%EC%8A%A4-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0-2-Spring-Boot%EC%97%90%EC%84%9C-SES-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0">AWS SES로 메일 서비스 사용하기- (2) Spring Boot에서 SES 사용하기</a></p>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/26aad0c3-ca90-4195-8039-3eec4ef870a6/image.png" /></p>
<p>이 전에 AWS SES로 등록된 메일로 메일을 보냈다.
구독자가 한명일 때는 정상적으로 메일이 보내졌는데 구독자를 한 명 더 추가했더니 오류가 발생했다.</p>
<blockquote>
<p>Email address is not verified. The following identities failed the check in region {region}: {email}</p>
</blockquote>
<p>위 오류의 발생 원인은 <strong>현재 내 SES가 샌드박스 상태</strong>이기 때문이다. </p>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/3fb104eb-6787-4043-b3ac-387bce658083/image.png" /></p>
<h2 id="💡-샌드박스-상태에서의-제한-사항">💡 샌드박스 상태에서의 제한 사항</h2>
<blockquote>
<ul>
<li>확인된 이메일 주소 및 도메인으로만 메일 전송이 가능하다.</li>
</ul>
</blockquote>
<ul>
<li>24시간 동안 최대 200개의 메일 전송이 가능하다.</li>
<li>초당 최대 1개의 메일 전송이 가능하다.</li>
</ul>
<br />


<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/6f1a6601-ad3e-4ab1-9d33-d928fbe4e043/image.png" /></p>
<p>만약 샌드박스 상태에서 구독자(메일 보낼 사람)를 더 늘릴거라면 메일을 인증받아야 가능하다.
메일을 인증받은 후 오류 해결!</p>