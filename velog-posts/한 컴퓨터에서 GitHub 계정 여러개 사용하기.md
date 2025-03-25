<p>재택근무 할 때가 있어서 집 컴퓨터 깃허브를 회사 계정으로 연결해놓았는데,
개인적으로 하는 공부는 원래 사용하던 내 계정 깃허브에서 관리하고 싶어서 알아보게 되었다.</p>
<p>이 경우, 각 계정에 대해 별도의 SSH키를 생성해야 한다.
<strong>SSH(Secure Shell)란 네트워크 상에서 안전하게 원격 서버에 접속하는 프로토콜</strong>이다.
GitHub에서는 SSH를 사용해서 패스워드 없이 안전하게 Git 명령을 실행할 수 있다.</p>
<br />

<p>GitHub 계정을 구분해서 사용하기 위해 SSH키를 각각 설정해준다.</p>
<h2 id="ssh-키-생성">SSH 키 생성</h2>
<h3 id="💡-회사-계정용">💡 회사 계정용</h3>
<pre><code class="language-bash">ssh-keygen -t rsa -b 4096 -C &quot;회사_이메일&quot; -f ~/.ssh/id_rsa_company</code></pre>
<br />

<pre><code class="language-bash">ls ~/.ssh</code></pre>
<p>난 이미 회사 계정을 등록해놓아서 이 부분은 생략하고, 현재 등록되어 있는 SSH키를 확인한다.
<code>id_rsa</code>, <code>id_rsa.pub</code>와 같은 파일이 있다면 등록되어 있는 것이다.</p>
<br />

<h3 id="💡-개인-계정용">💡 개인 계정용</h3>
<pre><code class="language-bash">ssh-keygen -t rsa -b 4096 -C &quot;개인이메일&quot; -f ~/.ssh/id_rsa_personal
</code></pre>
<p>위와 같이 입력하면 비밀번호를 설정하라고 하는데, 그냥 Enter를 두번 눌러 비밀번호 없이 진행했다.</p>
<pre><code class="language-bash">cat ~/.ssh/id_rsa_personal.pub</code></pre>
<p>그리고 공개 키 내용을 확인한다.
<br /></p>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/46cf32aa-4dbf-4c8a-9c43-8e1f80a1022d/image.png" /></p>
<p>이제 개인 계정에서 <code>settings</code> &gt; <code>SSH and GPG keys</code> &gt; <code>New SSH key</code>를 눌러 공개 키 내용을 복사해서 붙여넣은 뒤 저장한다.</p>
<br />

<h2 id="ssh-설정-파일-수정sshconfig">SSH 설정 파일 수정(~/.ssh/config)</h2>
<p>이제 회사 계정과 개인 계정을 구분하기 위해 SSH 설정 파일을 수정한다.</p>
<pre><code class="language-bash">nano ~/.ssh/config</code></pre>
<pre><code class="language-bash">Host github-company
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_rsa  # 기존 회사 SSH 키

Host github-personal
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_rsa_personal  # 개인 SSH 키</code></pre>
<p><code>ctrl</code> + <code>X</code>를 눌러서 저장하고 <code>Y</code>를 눌러서 빠져나온다.</p>
<br />

<h2 id="ssh-연결-테스트">SSH 연결 테스트</h2>
<pre><code class="language-bash">ssh -T git@github-company</code></pre>
<pre><code class="language-bash">ssh -T git@github-personal</code></pre>
<p>명령문을 입력하고, 출력문이 정상적으로 나오면 성공이다.</p>
<br />