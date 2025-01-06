<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/dbfd27a1-96b3-4de8-8401-e0e818cca02a/image.png" /></p>
<h2 id="jsx란-무엇인가"><strong>JSX</strong>란 무엇인가?</h2>
<blockquote>
<ul>
<li>JSX는 JavaScript XML의 약자이다.</li>
</ul>
</blockquote>
<ul>
<li>React에서 HTML과 유사한 구문을 사용하여 UI를 정의할 수 있게 해주는 확장 문법이다.</li>
</ul>
<pre><code class="language-jsx">const element = &lt;h1&gt;Hello World!&lt;/h1&gt;;</code></pre>
<p>내부적으로 JSX 코드는 <code>React.createElement()</code>로 변환된다.
<br /></p>
<h2 id="jsx의-주요-특징">JSX의 주요 특징</h2>
<ul>
<li>** HTML과 비슷하지만 다르다**
: HTML과 유사하게 보이지만 실제로는 JavaScript 코드이다.</li>
<li><strong>JavaScript 표현식을 사용한다.</strong>
: 중괄호 <code>{}</code>를 사용하여 JavaScript 표현식을 삽입할 수 있다.</li>
</ul>
<pre><code class="language-jsx">const name = 'Yeonhee';
const greeting = &lt;h1&gt;Hello, {name}!&lt;/h1&gt;;</code></pre>
<ul>
<li><strong>class 대신 className 사용</strong> 
: JSX에서 HTML 속성 <code>class</code>는 예약어이므로 <code>className</code>을 사용해야한다.</li>
</ul>
<br />

<h3 id="jsx에서-조건부-렌더링">JSX에서 조건부 렌더링</h3>
<ul>
<li><p><strong>삼항 연산자</strong></p>
<pre><code class="language-jsx">const isLoggedIn = true;
const message = isLoggedIn ? &lt;h1&gt;Welcome!&lt;/h1&gt; : &lt;h1&gt;Please log in!&lt;/h1&gt;</code></pre>
<br />
</li>
<li><p><strong>AND 연산자</strong></p>
<pre><code class="language-jsx">const messages = [];
return(
    &lt;div&gt;
  {messages.length &gt; 0 &amp;&amp; &lt;h2&gt;You have {messages.length} messages.&lt;/h2&gt;}
  &lt;/div&gt;
);</code></pre>
<p><code>messages</code>는 빈 배열이므로 <code>messages.length</code>는 <code>0</code>이다.
조건부 렌더링에서 <code>messages.length &gt; 0</code>은 <code>false</code>가 된다.
<code>false &amp;&amp; &lt;h2&gt;You have {messages.length} messages.&lt;/h2&gt;</code>는 <code>false</code>이므로 아무것도 렌더링되지 않는다.</p>
</li>
</ul>
<br />

<h3 id="jsx와-css-스타일링">JSX와 CSS 스타일링</h3>
<ul>
<li><p><strong>인라인 스타일</strong></p>
<pre><code class="language-jsx">  const style = { color: 'blue', fontSize: '20px' };
  const element = &lt;h1 style={style}&gt;Styled Text&lt;/h1&gt;;</code></pre>
</li>
<li><p><strong>CSS 클래스 적용</strong></p>
<pre><code class="language-css">.container {
width: 100%;
max-width: 1200px;
margin: 0 auto;
padding: 20px
}
</code></pre>
</li>
</ul>
<pre><code>
```jsx
const element = &lt;div className=&quot;container&quot;&gt;&lt;/div&gt;;</code></pre><p>JSX의 <code>style</code>속성은 <strong>JavaScript 객체</strong>로 전달되며, CSS 속성 이름은 카멜케이스(camelCase)로 작성해야 한다.</p>
<blockquote>
<p>예) <code>background-color</code> -&gt; <code>backgroundColor</code></p>
</blockquote>
<p>만약 값이 숫자인 경우 단위를 생략했을 때 자동으로 픽셀(px)로 처리된다.</p>
<pre><code class="language-jsx">const style = { fontSize: 20 };    // '20px'로 해석 된다.</code></pre>
<br />

<h2 id="jsx-사용-시-주의할-점">JSX 사용 시 주의할 점</h2>
<blockquote>
<ul>
<li>JSX는 JavaScript로 변환되므로 문법 오류가 있으면 컴파일 에러가 발생한다.</li>
</ul>
</blockquote>
<ul>
<li>보안상의 이유로 JSX는 HTML을 렌더링할 때 자동으로 XSS(Cross-Site Scripting)를 방지한다.</li>
</ul>
<p><strong>XSS(Cross-Site Scripting)</strong>는 웹 애플리케이션의 취약점을 이용해서 악성 스크립트를 주입하여 실행하는 공격 기법이다.
삽입된 스크립트는 피해자의 브라우저에서 실행되며 주로 JavaScript를 이용한다.</p>