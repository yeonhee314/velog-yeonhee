<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/ec8518a9-d2ac-40a7-81f3-a2b3e50a69d5/image.png" /></p>
<p>바닐라JS를 다시 공부하다가 문득 <code>&lt;script&gt;</code>태그의 위치에 대해 의문점이 생겼다.
이전에 프로젝트를 할 때 당연하게 <code>&lt;body&gt;</code>태그의 맨 밑에 선언했는데 
학원에서 배울 때는 또 <code>&lt;head&gt;</code>에 선언했다.
그때는 의문점이 없었는데 지금 공부하다보니 갑자기 의문이 생겼다.</p>
<p><code>&lt;script&gt;</code>태그의 위치에 대해서 다시 정리하자.</p>
<hr />

<p><code>&lt;script&gt;</code> 태그는 어디 선언하는지에 따라 자바스크립트의 실행 시점과 동작이 달라진다.
<code>&lt;head&gt;</code> 태그 안에 선언하거나, <code>&lt;body&gt;</code> 태그 안에 선언하는 2가지 방법으로 선언할 수 있다.
<br /></p>
<h2 id="1-body태그-끝에-선언권장">1. <code>&lt;body&gt;</code>태그 끝에 선언(권장)</h2>
<pre><code class="language-html">&lt;body&gt;
  &lt;script src=&quot;../script/app.js&quot;&gt;&lt;/script&gt;
&lt;/body&gt;</code></pre>
<blockquote>
<ul>
<li><strong>HTML이 먼저 로드</strong> 된 후 스크립트가 실행된다.</li>
</ul>
</blockquote>
<ul>
<li>DOM(Document Object Model)이 모두 준비된 상태에서 자바스크립트가 실행되므로 DOM을 조작할 떄 에러가 발생하지 않는다.</li>
<li>브라우저가 HTML을 렌더링하면서 스크립트를 동시에 다운로드 하기 때문에 사용자 경험(UX)에 좋다.</li>
</ul>
<p>웬만하면 <code>&lt;script&gt;</code>는 <code>&lt;body&gt;</code>태그 끝에 선언하는 것을 권장한다.
웹 브라우저에서 html 페이지를 요청하면 브라우저는 <strong>HTML을 위에서 아래로 파싱하면서 렌더링</strong>한다.</p>
<p>만약 <code>&lt;head&gt;</code>나 <code>&lt;body&gt;</code>초반에 <code>&lt;script&gt;</code> 태그를 선언하면, 
브라우저는 <strong>스크립트를 다운로드하고 실행할 때까지 HTML 파싱을 멈춘다</strong>.
결과적으로 <strong>HTML 콘텐츠가 늦게 렌더링</strong>될 수 있다.</p>
<p><code>&lt;body&gt;</code>태그 끝에 스크립트를 넣으면, 브라우저가 HTML을 모두 파싱하고 렌더링한 뒤 스크립트를 실행하기 때문에 사용자 경험(UX)가 개선된다.</p>
<br />

<h3 id="head에-script-태그-선언-시-발생할-수-있는-에러"><code>&lt;head&gt;</code>에 <code>&lt;script&gt;</code> 태그 선언 시 발생할 수 있는 에러</h3>
<pre><code class="language-html">&lt;head&gt;
      &lt;script&gt;
          document.getElementById('myButton').addEventListener('click', () =&gt; alert('클릭!'));
      &lt;/script&gt;
&lt;/head&gt;
&lt;body&gt;
  &lt;button id=&quot;myButton&quot;&gt;클릭하세요&lt;/button&gt;
&lt;/body&gt;</code></pre>
<p> 위의 코드에서는 자바스크립트가 실행될 때 <code>#myButton</code>이 아직 로드되지 않아 <code>null</code> 에러가 발생한다.</p>
<h3 id="수정한-코드">수정한 코드</h3>
<pre><code class="language-html"> &lt;body&gt;
   &lt;button id=&quot;myButton&quot;&gt;클릭하세요&lt;/button&gt;
   &lt;script&gt;
         document.getElementById('myButton').addEventListener('click', () =&gt; alert('클릭!'));
   &lt;/script&gt;
&lt;/body&gt;</code></pre>
<br />



<h2 id="2-head태그-안에-선언">2. <code>&lt;head&gt;</code>태그 안에 선언</h2>
<pre><code class="language-html">&lt;head&gt;
  &lt;script src=&quot;../scripts/app.js&quot;&gt;&lt;/script&gt;
&lt;/head&gt;</code></pre>
<p> 위와 같이 선언하면 스크립트가 <strong>HTML을 파싱하기 전에 실행</strong>된다.
 DOM이 아직 준비되지 않은 상태에서 DOM을 조작하려고 하면 에러가 발생할 수 있다.</p>
<p> 만약 <code>&lt;head&gt;</code>에 선언해야 한다면 <code>defer</code> 또는 <code>async</code> 속성을 사용하자.
<br /></p>
<blockquote>
<p><code>defer</code> : HTML 파싱이 끝난 후 스크립트를 실행한다.</p>
</blockquote>
<pre><code class="language-html">&lt;script src=&quot;../scripts/app.js&quot; defer&gt;&lt;/script&gt;</code></pre>
<blockquote>
<p><code>async</code> : 스크립트를 비동기 로드하지만, 실행순서가 보장되지 않는다.</p>
</blockquote>
<pre><code class="language-html">&lt;script src=&quot;../scripts/app.js&quot; async&gt;&lt;/script&gt;</code></pre>
<p>만약 단순히 외부라이브러리를 로드하거나 DOM에 의존하지 않는 코드라면 <code>head</code>에 선언한다.</p>