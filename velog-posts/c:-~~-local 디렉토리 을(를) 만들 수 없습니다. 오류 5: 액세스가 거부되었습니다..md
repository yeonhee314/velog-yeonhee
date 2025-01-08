<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/7f124ee2-43d5-423e-b0ab-9076d9845ffb/image.png" />
<img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/64c46b76-64d4-4cb9-9b72-d70f70fbf7fd/image.png" /></p>
<blockquote>
<p>&quot;C:\local폴더&quot; 폴더를 만들 수 없습니다..
오류 5: 액세스가 거부되었습니다.</p>
</blockquote>
<blockquote>
<p>설치가 완료되지 않았습니다.
문제를 해결한 후, 다시 설치를 시작하십시오.</p>
</blockquote>
<p><code>Visual Studio Code</code> 사용 중에 간헐적으로 이 오류 창이 떴다.
이전에는 그냥 확인을 눌러서 닫아도 별 문제가 없길래 몇 번씩 닫았는데,
이게 계속 뜨니까 생각보다 거슬렸다.
<br /></p>
<h2 id="💡-발생-원인">💡 발생 원인</h2>
<p>전에 <code>Spring Boot</code> 공부할 때 <code>lombok</code> 라이브러리를 사용하려 하니까 계정 이름이 한글이라 lombok 설치가 제대로 안됐다.
세팅한다고 사용자 계정이름을 <code>김연희</code>에서 <code>yeonhee</code>로 한글에서 영어로 변경했는데 그게 원인이었다.</p>
<br />

<h2 id="💡-해결-방법---1-권한이-없는-경우">💡 해결 방법 - 1. 권한이 없는 경우</h2>
<p>1.<code>Windows 키 + E</code>를 눌러서 파일 탐색기를 연다.
2. 탐색기 상단의 주소창에 <code>C:\Users\[사용자 이름]\AppData\Local</code> 를 입력한다.
3. 해당 폴더에서 마우스 오른쪽 클릭 &gt; 속성 &gt; 보안 탭 &gt; 사용 권한 창의 보안 탭에서 편집 버튼을 클릭하고 추가 버튼을 클릭한다.
<img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/b4b43679-1a61-4d3d-b221-7d59077e295a/image.png" />
<img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/185daef5-7584-47a5-a5e2-e01a944d406a/image.png" />
4. '선택할 개체 이름을 입력하십시오' 항목에 <strong>everyone</strong>을 입력한 후 이름 확인 버튼을 클릭한다.
<img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/dbb2ca12-0598-48db-a786-f71179c26215/image.png" />
5. <code>Everyone</code>이 추가되면 <code>Everyone</code>을 클릭하고 '모든 권한'을 체크한 후 확인 버튼을 클릭한다.
<img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/ef7b644c-d116-4487-9c29-2777f06e6124/image.png" /></p>
<p>만약 이 방법도 안된다면 다른 저장 경로를 사용하는 것도 방법이다.
<br /></p>
<h2 id="💡-해결-방법---2-재설치">💡 해결 방법 - 2. 재설치</h2>
<p>나같은 경우 계정이름이 변경되면서 발생한 오류로 추측된다.
그래서 위의 권한 설정을 해주었음에도 해결되지 않았다.</p>
<blockquote>
<ol>
<li><strong>제어판 &gt; 프로그램 &gt; 프로그램 및 기능</strong>에서 <code>Visual Studio Code</code>를 삭제한다.</li>
<li><code>C:\Users\[사용자 이름]\AppData\Roaming\Code</code> 와 
<code>C:\Users\[사용자 이름]\.vscode</code> 를 모두 삭제한다. </li>
</ol>
<p><strong>(주의 : 만약 위 폴더를 모두 삭제하면 설치된 확장 프로그램과 설정이 모두 초기화되므로 필요한 경우 백업하는 것이 좋다.)</strong>
3. <a href="https://code.visualstudio.com/">Visual Studio Code 공식 웹사이트</a>에서 다시 다운로드 받는다.</p>
</blockquote>
<br />

<p>나는 재설치 후 해당 오류가 더이상 발생하지 않았다.
여기서 얻은 한가지 교훈이라면.. 한글 이름 때문에 예상하지 못한 오류가 여기저기서 너무 많이 발생했다.
개발자라면....<strong>컴퓨터 처음 샀을 때 이름은 무조건 영어로 설정하자..!!</strong></p>
<p><br /><br /></p>
<p>** 참고한 글 **
<a href="https://answers.microsoft.com/ko-kr/windows/forum/all/%EC%84%A4%EC%B9%98/62395cb2-3d5a-4179-9f71-998895c8be57">설치 프로그램에서 c:~~\local 디렉토리 을(를) 만들 수 없습니다. 오류 5: 액세스가 거부되었습니다.</a></p>