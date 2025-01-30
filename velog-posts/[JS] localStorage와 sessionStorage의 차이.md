<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/4b2817ae-7e57-4b08-8e28-67066f79549b/image.png" /></p>
<p><code>localStorage</code>를 사용하여 배열 데이터를 저장하는 작업 중인데, <code>sessionStorage</code>와의 차이점도 함께 정리하면 좋을 것 같아서 정리해두려고 한다.</p>
<hr /><br />

<p><code>localStorage</code>와 <code>sessionStorage</code>는 웹 브라우저에서 데이터를 클라이언트에 저장하지만 
<strong>저장되는 기간과 데이터의 생명주기</strong>가 다르다.
<br /></p>
<h2 id="💡localstorage">💡localStorage</h2>
<p><code>localStorage</code>는 사용자가 브라우저를 닫거나 컴퓨터를 재부팅해도 데이터가 남아있다.
<strong>같은 도메인</strong>에 대해 저장된 데이터는 다른 탭이나 창에서도 공유 된다.
대체로 약 <strong>5MB</strong> 정도로 비교적 많은 데이터를 저장할 수 있다.</p>
<p>페이지를 새로고침하거나 닫아도 데이터가 계속 유지되므로, 사용자에게 지속적인 상태를 제공할 때 사용된다.</p>
<pre><code class="language-javascript">    localStorage.setItem('username', 'hee');
    let username = localStorage.getItem('username');    // 'hee'
    console.log(localStorage.length);    // 1
    console.log(localStorage.key(0));    // 'hee' -&gt; 인수(index)에 해당하는 key의 value 값을 받아 온다.
    localStorage.removeItem('username'); // localStorage 객체에서 원하는 값 삭제
    localStorage.clear();    // 한번에 저장된 모든 값을 삭제</code></pre>
<p>만약 <code>localStorage.getItem()</code>에서 인수를 주지 않으면 전체 값을 받아온다.</p>
<p><code>localStorage</code>는 사용자 테마 설정 등 <strong>장기적으로 보존할 데이터</strong>에 사용하면 적합하다.
<code>localStorage</code>의 값을 지우려면 직접 지워줘야한다.</p>
<p><br /><br /></p>
<h2 id="💡sessionstorage">💡sessionStorage</h2>
<p><code>sessionStorage</code>는 <code>localStorage</code>와 소멸 타이밍이 다르다.
<code>localStorage</code>는 소멸 타이밍이 없어서 직접 지워줘야하지만 <code>sessionStorage</code>는 세션의 종료 시 사라진다.
<code>sessionStorage</code>에서 의미하는 세션은 <strong>가장 작은 단위인 탭 단위</strong>를 의미한다.</p>
<p>데이터는 <strong>브라우저 탭 또는 창이 닫힐 때까지 유지</strong>된다.
즉, <strong>탭을 닫으면 삭제</strong>되며, 같은 페이지를 새로고침해도 데이터는 계속 유지된다.
데이터 범위는 <strong>현재 탭에서만 유효하며</strong> 다른 탭이나 창에서 동일한 웹 페이지를 열면 각 탭마다 별도의 <code>sessionStorage</code> 데이터가 저장된다.</p>
<p>페이지가 새로고침되거나 탭이 닫힐 때 자동으로 삭제되야 하는 데이터에 적합하다.
(ex. 로그인 상태, 일시적인 세션 정보)
용량은 <code>localStorage</code>와 비슷하게 <strong>5MB</strong> 정도이다.</p>
<pre><code class="language-javascript">    sessionStorage.setItem('sessionId', '123456');
    let sessionId = sessoinStorage.getItem('sessionId'); // '123456'</code></pre>
<p><code>sessionStorage</code>는 최근 본 상품 등 탭을 닫으면 데이터가 삭제되므로 <strong>세션 중에만 필요한 데이터, 일시적인 데이터</strong> 저장에 사용하면 적합하다.</p>