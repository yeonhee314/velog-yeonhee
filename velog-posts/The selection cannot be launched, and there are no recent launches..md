<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/5c72a933-67a6-4cf2-905e-cdee36362a4d/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/0c241d39-8300-49eb-ac85-78a9139f2889/image.png" />
<strong>The selection cannot be launched, and there are no recent launches.</strong>
선택 항목을 시작할 수 없으며 최근에 시작한 항목이 없습니다.</p>
<br />

<p>이클립스에서 코드를 실행시켰을 때 발생한 오류이다.
이 에러 메세지는 자바프로젝트를 실행할 때, 정확히는 <strong>이클립스 설치 후 최초로 프로젝트를 실행할 때 발생하는 에러</strong>이다.</p>
<p><strong>프로젝트를 실행할 때 현재 보고있는 프로젝트가 아닌 가장 최근에 실행되었던 프로젝트를 자동으로 실행하고 있는 것이 원인</strong>이다.</p>
<br />

<h2 id="해결-방법">해결 방법</h2>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/1fd90298-ec70-41a2-93ab-5fb8734ce3ba/image.png" /></p>
<p><strong>[Window] &gt; [Preferences] &gt; [Run/Debug &gt; Launching]</strong></p>
<br />

<p>이클립스 첫 설치시에는 <strong>[Launch Operation]이 ‘Launch the previously lanuched application’이 기본 선택</strong>되어있다. 직전에 실행된 애플리케이션(파일)을 실행하라는 뜻인데, 이클립스 최초 실행시에는 직전에 실행된 파일이 존재할리가 없기 때문에 ‘직전에 실행된 파일’이 존재하지 않아 접근 에러가 난다. 이 설정을 <strong>‘Launch the associated project’</strong>로 바꿔준다.</p>