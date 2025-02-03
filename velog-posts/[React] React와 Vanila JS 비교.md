<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/03a353a3-46dd-4e79-b027-da6a090c1463/image.png" /></p>
<h2 id="react와-vanila-js-비교">React와 Vanila JS 비교</h2>
<blockquote>
<p><a href="https://codesandbox.io/p/sandbox/react-vs-vanilla-demo-uc08fv?file=%2Fpublic%2Findex.html%3A1%2C1-43%2C8">React Demo</a>
<a href="https://codesandbox.io/p/sandbox/vanilla-js-demo-6049kj?file=%2Findex.js%3A21%2C22">Vanila JS Demo</a></p>
</blockquote>
<br />

<h3 id="왜-리액트를-사용해야하는가">왜 리액트를 사용해야하는가?</h3>
<p>리액트는 더 단순한 심상 모델을 제공하고, 복잡한 웹 앱과 웹 사용자 인터페이스를 더 쉽게 구축하도록 해주기 때문에  바닐라 자바스크립트보다 리액트같은 라이브러리를 사용하는 것이 더 낫다.</p>
<p>리액트 앱에서는 리액트가 사용자 인터페이스 전체를 렌더링한다.
본격적인 내용은 <code>index.js</code>파일부터 시작한다.</p>
<h4 id="indexjs">index.js</h4>
<pre><code class="language-javascript">import { StrictMode } from &quot;react&quot;;
import { createRoot } from &quot;react-dom/client&quot;;

import App from &quot;./App&quot;;

const rootElement = document.getElementById(&quot;root&quot;);
const root = createRoot(rootElement);

root.render(
  &lt;StrictMode&gt;
    &lt;App /&gt;
  &lt;/StrictMode&gt;
);</code></pre>
<h4 id="indexhtml">index.html</h4>
<pre><code class="language-html">&lt;!DOCTYPE html&gt;
&lt;html lang=&quot;en&quot;&gt;

&lt;head&gt;
    &lt;meta charset=&quot;utf-8&quot;&gt;
    &lt;meta name=&quot;viewport&quot; content=&quot;width=device-width, initial-scale=1, shrink-to-fit=no&quot;&gt;
    &lt;meta name=&quot;theme-color&quot; content=&quot;#000000&quot;&gt;
    &lt;link rel=&quot;manifest&quot; href=&quot;%PUBLIC_URL%/manifest.json&quot;&gt;
    &lt;link rel=&quot;shortcut icon&quot; href=&quot;%PUBLIC_URL%/favicon.ico&quot;&gt;
    &lt;title&gt;React App&lt;/title&gt;
&lt;/head&gt;

&lt;body&gt;
    &lt;noscript&gt;
        You need to enable JavaScript to run this app.
    &lt;/noscript&gt;
    &lt;div id=&quot;root&quot;&gt;&lt;/div&gt;
&lt;/body&gt;

&lt;/html&gt;</code></pre>
<p><code>index.js</code>파일에서 <code>document.getElementById(&quot;root&quot;);</code>를 선택해서
<code>index.html</code>의 <code>&lt;div id=&quot;root&quot;&gt;&lt;/div&gt;</code>가 선택되면, 리액트가 이 <code>&lt;div&gt;</code>와 그 내용을 제어하기 시작한다.</p>
<p>그 때 중요한게 <code>App.js</code>파일인데, 말하자면 <strong>핵심 코드가 담겨있다.</strong></p>
<h5 id="appjs">App.js</h5>
<pre><code class="language-javascript">import { useState } from &quot;react&quot;;
import &quot;./styles.css&quot;;

const content = [
  [
    &quot;React is extremely popular&quot;,
    &quot;It makes building complex, interactive UIs a breeze&quot;,
    &quot;It's powerful &amp; flexible&quot;,
    &quot;It has a very active and versatile ecosystem&quot;
  ],
  [
    &quot;Components, JSX &amp; Props&quot;,
    &quot;State&quot;,
    &quot;Hooks (e.g., useEffect())&quot;,
    &quot;Dynamic rendering&quot;
  ],
  [
    &quot;Official web page (react.dev)&quot;,
    &quot;Next.js (Fullstack framework)&quot;,
    &quot;React Native (build native mobile apps with React)&quot;
  ]
];

export default function App() {
  const [activeContentIndex, setActiveContentIndex] = useState(0);

  return (
    &lt;div&gt;
      &lt;header&gt;
        &lt;img src=&quot;react-logo-xs.png&quot; alt=&quot;React logo&quot; /&gt;
        &lt;div&gt;
          &lt;h1&gt;React.js&lt;/h1&gt;
          &lt;p&gt;i.e., using the React library for rendering the UI&lt;/p&gt;
        &lt;/div&gt;
      &lt;/header&gt;

      &lt;div id=&quot;tabs&quot;&gt;
        &lt;menu&gt;
          &lt;button
            className={activeContentIndex === 0 ? &quot;active&quot; : &quot;&quot;}
            onClick={() =&gt; setActiveContentIndex(0)}
          &gt;
            Why React?
          &lt;/button&gt;
          &lt;button
            className={activeContentIndex === 1 ? &quot;active&quot; : &quot;&quot;}
            onClick={() =&gt; setActiveContentIndex(1)}
          &gt;
            Core Features
          &lt;/button&gt;
          &lt;button
            className={activeContentIndex === 2 ? &quot;active&quot; : &quot;&quot;}
            onClick={() =&gt; setActiveContentIndex(2)}
          &gt;
            Related Resources
          &lt;/button&gt;
        &lt;/menu&gt;
        &lt;div id=&quot;tab-content&quot;&gt;
          &lt;ul&gt;
            {content[activeContentIndex].map((item) =&gt; (
              &lt;li key={item}&gt;{item}&lt;/li&gt;
            ))}
          &lt;/ul&gt;
        &lt;/div&gt;
      &lt;/div&gt;
    &lt;/div&gt;
  );
}</code></pre>
<p>안에 <code>App()</code> 이라는 함수가 있는데 <code>HTML</code>코드가 들어있다.
이는 <code>JavaScript</code> 기본 기능이 아니다.
<code>JavaScript</code> 코드에서 <code>HTML</code>코드를 작성하면 원래는 에러가 발생한다.
하지만 React 프로젝트에서는 위와 같은 작업이 가능하다.</p>
<p>** 리액트의 핵심 기능 중 하나는 HTML과 JS 코드를 섞어쓸 수 있는 것이다.**</p>
<h4 id="html에서-동적-요소-사용이-가능한-react">HTML에서 동적 요소 사용이 가능한 React</h4>
<pre><code class="language-javascript">    &lt;button
     className={activeContentIndex === 0 ? &quot;active&quot; : &quot;&quot;}
     onClick={() =&gt; setActiveContentIndex(0)}
    &gt;
        Why React?
    &lt;/button&gt;</code></pre>
<p>리액트에서는 위의 예시와 같이 HTML 코드 안에 <strong>동적 요소</strong>를 사용할 수 있다.</p>
<br />

<p>그리고 <strong>리액트로 작업할 때는 코드를 선언형으로 작성</strong>한다.
즉, 목표로 하는 UI상태를 정의할 뿐 거쳐야하는 단계는 정의하지 않는다.
리액트가 과정을 알아서 파악해서 필요한 단계를 수행한다.</p>
<p>하지만 <strong>Vanila JS는 코드를 명령형으로 작성</strong>한다.</p>
<h5 id="indexjs-1">index.js</h5>
<pre><code class="language-javascript">const content = [
  [
    &quot;React is extremely popular&quot;,
    &quot;It makes building complex, interactive UIs a breeze&quot;,
    &quot;It's powerful &amp; flexible&quot;,
    &quot;It has a very active and versatile ecosystem&quot;
  ],
  [
    &quot;Components, JSX &amp; Props&quot;,
    &quot;State&quot;,
    &quot;Hooks (e.g., useEffect())&quot;,
    &quot;Dynamic rendering&quot;
  ],
  [
    &quot;Official web page (react.dev)&quot;,
    &quot;Next.js (Fullstack framework)&quot;,
    &quot;React Native (build native mobile apps with React)&quot;
  ]
];

const btnWhyReact = document.getElementById(&quot;btn-why-react&quot;);
const btnCoreFeature = document.getElementById(&quot;btn-core-features&quot;);
const btnResources = document.getElementById(&quot;btn-resources&quot;);
const tabContent = document.getElementById(&quot;tab-content&quot;);

function displayContent(items) {
  let listContent = &quot;&quot;;
  for (const item of items) {
    listContent += `&lt;li&gt;${item}&lt;/li&gt;`;
  }
  const list = document.createElement(&quot;ul&quot;);
  tabContent.innerHTML = &quot;&quot;; // clear existing content
  list.innerHTML = listContent; // insert new content
  tabContent.append(list);
}

function highlightButton(btn) {
  // Clear all existing styling / highlights
  btnWhyReact.className = &quot;&quot;;
  btnCoreFeature.className = &quot;&quot;;
  btnResources.className = &quot;&quot;;
  btn.className = &quot;active&quot;; // set new style / highlight
}

function handleClick(event) {
  const btnId = event.target.id;
  highlightButton(event.target);
  if (btnId === &quot;btn-why-react&quot;) {
    displayContent(content[0]);
  } else if (btnId === &quot;btn-core-features&quot;) {
    displayContent(content[1]);
  } else {
    displayContent(content[2]);
  }
}

displayContent(content[0]); // initially show this content

btnWhyReact.addEventListener(&quot;click&quot;, handleClick);
btnCoreFeature.addEventListener(&quot;click&quot;, handleClick);
btnResources.addEventListener(&quot;click&quot;, handleClick);</code></pre>
<p>위와 같이 목표가 아니라 거쳐야할 단계를 정의한다.
<strong>단계별로 명령을 정의했기 때문에 명령형 방식</strong>이라고 부른다.
단계를 정의하는건 훨씬 번거롭다.
도중에 단계를 빼먹거나 오류가 발생하기도 쉽다.</p>
<h2 id="정리">정리</h2>
<blockquote>
<ul>
<li>리액트는 작성할 코드가 비교적 짧고, 리액트 내부에서 자바스크립트로 UI 업데이트도 알아서 해준다.</li>
</ul>
</blockquote>
<ul>
<li>조건과 목표 상태, 상태 변경 조건만 정의하면 나머지는 리액트가 알아서 해준다.</li>
</ul>