<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/e0e2b236-a631-4269-9ff2-e71e4e948f44/image.png" /></p>
<p><strong>‘Launching Tomcat v10.1 Server at localhost’ has encountered a problem.</strong></p>
<p>Several ports (8005, 8080) required by Tomcat v10.1 Server at localhost are already in use. The server may already be running in another process, or a system process may be using the port. To start this server you will need to stop the other process or change the port number(s).</p>
<p><strong>'Localhost에서 Tomcat v10.1 Server를 시작하는 중'에 문제가 발생했습니다.</strong></p>
<p>로컬 호스트에서 Tomcat v10.1 Server에 의해 요구되는 여러 포트(8005, 8080)가 이미 사용 중입니다. 서버가 이미 다른 프로세스에서 실행 중이거나 시스템 프로세스가 포트를 사용 중일 수 있습니다. 이 서버를 시작하려면 다른 프로세스를 중지하거나 포트 번호를 변경해야 합니다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/4194629e-6772-4ff5-9af5-13a9a571e72b/image.png" /></p>
<p>서버 구동 시 톰캣에서 오류가 발생했다.
원인으로는 비정상적으로 서버가 종료되었을 때 발생하는 것으로 추정된다.
<br /></p>
<h3 id="해결-방법">해결 방법</h3>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/9c0f2d43-127d-493d-8ec9-1aa617dd46bc/image.png" /></p>
<p>cmd에 <code>netstat -p tcp -ano</code> 를 입력 하면 포트에 연결된 모든 pid를 확인할 수 있다.</p>
<p>Tomcat이 사용하는 기본 포트 중 이미 연결되어 있다고 뜨는 <strong>0.0.0.0:8080, 127.0.0.1:8005</strong> 를 사용하는 PID를 찾는다.</p>
<p><strong>포트를 사용중인 PID 는 2784이다.</strong>
그렇다면 pid 2784를 삭제해준다.</p>
<p>💡컴퓨터마다 PID 는 다르기 때문에 본인의 PID 를 찾아야 합니다.
<br /></p>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/59600796-0b79-4043-80b7-cdc11c99944a/image.png" />
<code>taskkill /f /pid 2784(pid번호)</code></p>
<p>pid 프로세스가 종료되었다고 출력된다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/1b775041-7322-418d-a56f-def52b21b585/image.png" />
다시 <code>netstat -p tcp -ano</code> 를 입력해서 8080과 8005 포트를 사용하는 프로세스가 있는지 확인한다.</p>
<p>없다면 문제 해결! 😊</p>
<p><br /><br /></p>
<h3 id="해결-되지-않았을-때">해결 되지 않았을 때</h3>
<p>만약 위와 같은 방법으로 실행했는데 <code>taskkill</code> 이 실행되지 않을 수 있다.</p>
<blockquote>
<p>오류 : 프로세스 (PID ——)를 종료할 수 없습니다.
원인 : 액세스가 거부되었습니다.</p>
</blockquote>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/01480317-3fb1-453a-87af-dacf8807c36b/image.png" />
<strong>명령 프롬프트를 관리자 권한으로 실행</strong>시키면 <code>taskkill</code> 이 정상적으로 실행됩니다.</p>