<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/7fbe1a7d-af3a-41ec-8f0b-8c559aaf68cc/image.png" /></p>
<p>노트북에서 리액트 프로젝트 세팅하는데 에러가 발생했다.
발생 원인은 PowerShell의 실행 정책 때문에 발생한 에러로, 
실행 정책을 변경하여 PowerShell 스크립트의 실행을 제어하면 된다.</p>
<h2 id="📑-현재-실행-정책-확인">📑 현재 실행 정책 확인</h2>
<pre><code class="language-bash">Get-ExecutionPolicy</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/cc11c459-3680-4955-8596-df6faac1e6eb/image.png" /></p>
<p>이 명령어를 통해 현재 설정된 실행 정책을 확인할 수 있다.</p>
<br />

<h2 id="📑-실행-정책-변경">📑 실행 정책 변경</h2>
<pre><code class="language-bash">Set-ExecutionPolicy RemoteSigned</code></pre>
<p>npm을 사용하기 위해 실행 정책을 변경해야 한다. </p>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/1053884a-e255-4356-97c1-946c6c48a1dd/image.png" /></p>
<p>다음 명령어를 입력해서 실행 정책을 <code>RemoteSigned</code>로 변경한다. 
이 정책은 <strong>로컬에서 작성한 스크립트는 실행할 수 있게 해준다.</strong></p>
<p>변경 사항 적용을 확인하면 해결!</p>