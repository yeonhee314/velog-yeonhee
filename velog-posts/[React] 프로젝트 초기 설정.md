<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/a5d13446-be92-4ac3-87a3-0c6cb00ed67f/image.png" /></p>
<p>내가 보려고 정리해두는 리액트 프로젝트 초기 설정
<br /></p>
<h2 id="💡-프로젝트-생성">💡 프로젝트 생성</h2>
<h3 id="1-cra">1. CRA</h3>
<p><strong>기존 방법</strong></p>
<pre><code class="language-bash">npx create-react-app [프로젝트명]
npx create-react-app [프로젝트명] --template typescript</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/85e62f1a-d000-41cf-9f1b-f2b38d190407/image.png" /></p>
<p>기존의 CRA 방식(위의 방식)대로 프로젝트를 생성하면 에러가 발생하는데, 이는 <strong>React19 정식 릴리즈로 인해 <code>create-react-app</code>이 제대로 작동하지 않는 이슈</strong>이다. </p>
<p>주요 내용은 <code>npx create-react-app</code>으로 프로젝트를 생성하면 설치되는 <code>@testing-library/react@13.4.0</code>패키지는 <code>react@^19.0.0</code>와 호환되지 않아서 <code>react@^18.0.0</code>버전을 사용하라는 것이다.</p>
<p>그게 아니면 <code>--force</code>나 <code>--legacy-peer-deps</code>옵션을 사용 하여 강제 설치하라고 하는 문구이다. 에러 관련해서 몇 개 찾아보니 강제 설치는 별로 추천하지 않는듯 하다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/5b411edb-dd6a-4949-a1a6-b9ec3159555b/image.png" /></p>
<p>에러는 발생해도 필수 패키지가 아니므로 프로젝트는 정상적으로 생성되었다.
<code>package.json</code>을 확인해보면 react와 react-dom은 최신버전인 19.0.0으로 설치가 되었다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/fefa060b-9d7a-4c43-b059-569f025d78c7/image.png" /></p>
<p><code>npm run start</code>로 실행을 하면 실행은 되지만 에러가 발생한다.</p>
<h3 id="해결-방법">해결 방법</h3>
<blockquote>
<ul>
<li>react, react-dom을 18버전으로 다운그레이드</li>
</ul>
</blockquote>
<ul>
<li>react 18과 호환되는 버전의 @testing-library/react, web-vitals 패키지 설치</li>
</ul>
<pre><code class="language-bash">npm install react@18 react-dom@18 @testing-library/jest-dom@5.17.0 @testing-library/react@13.4.0 @testing-library/user-event@13.5.0 web-vitals</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/809d0885-f4e2-4758-9c28-765de84038af/image.png" /></p>
<p>위의 패키지들을 설치하여 에러를 해결할 수 있다.</p>
<br />

<h3 id="2-vite">2. Vite</h3>
<pre><code class="language-bash">npm create vite@latest [프로젝트명]
npm create vite@latest [프로젝트명] -- template react-ts</code></pre>
<br />

<h2 id="💡-라이브러리">💡 라이브러리</h2>
<h3 id="styled-components">styled-components</h3>
<p><a href="https://styled-components.com/">[styled components 공식 문서]</a></p>
<pre><code class="language-bash">npm install styled-components</code></pre>
<p>npm으로 install하거나 VS Code에 <a href="https://marketplace.visualstudio.com/items?itemName=styled-components.vscode-styled-components">Extension</a>을 설치해서 사용한다.
styled-component는 리액트 컴포넌트의 CSS 스타일링을 편하게 하기 위해 만들어진 라이브러리이다.</p>
<br />

<h3 id="css-normalize">CSS Normalize</h3>
<pre><code class="language-bash">// npm
npm i normalize.css
npm install --save styled-components

// yarn
yarn add styled-components</code></pre>
<p><a href="https://necolas.github.io/normalize.css/">Normalize.css</a></p>
<p>CSS Normalize는 가능한한 브라우저의 내장 스타일을 최대한 건들지 않는 선에서 브라우저간에 상이한 부분만 스타일을 통일시켜준다.</p>
<p><strong>styled-component의 이름은 파스칼케이스(PascalCase)</strong>로 작성하는 것이 좋다.</p>
<h3 id="css-reset">CSS Reset</h3>
<pre><code class="language-css">/* http://meyerweb.com/eric/tools/css/reset/ 
   v2.0 | 20110126
   License: none (public domain)
*/

html, body, div, span, applet, object, iframe,
h1, h2, h3, h4, h5, h6, p, blockquote, pre,
a, abbr, acronym, address, big, cite, code,
del, dfn, em, img, ins, kbd, q, s, samp,
small, strike, strong, sub, sup, tt, var,
b, u, i, center,
dl, dt, dd, ol, ul, li,
fieldset, form, label, legend,
table, caption, tbody, tfoot, thead, tr, th, td,
article, aside, canvas, details, embed, 
figure, figcaption, footer, header, hgroup, 
menu, nav, output, ruby, section, summary,
time, mark, audio, video {
    margin: 0;
    padding: 0;
    border: 0;
    font-size: 100%;
    font: inherit;
    vertical-align: baseline;
}
/* HTML5 display-role reset for older browsers */
article, aside, details, figcaption, figure, 
footer, header, hgroup, menu, nav, section {
    display: block;
}
body {
    line-height: 1;
}
ol, ul {
    list-style: none;
}
blockquote, q {
    quotes: none;
}
blockquote:before, blockquote:after,
q:before, q:after {
    content: '';
    content: none;
}
table {
    border-collapse: collapse;
    border-spacing: 0;
}</code></pre>
<p><a href="https://cssdeck.com/blog/scripts/eric-meyer-reset-css/">Reset CSS</a>
CSS Reset은 브라우저가 자체적으로 모든 HTML요소에 적용한 스타일이 사라지기 때문에 CSS Reset을 적용하고 아무런 추가 스타일을 해주지 않으면 해당 웹페이지 상의 모든 HTML요소가 동일한 모습으로 보인다.
(HTML 코드를 직접 보지 않는 이상 어디가 <code>&lt;h1&gt;</code>이고 어디가 <code>&lt;p&gt;</code>인지 구분할 수 없다.)</p>
<br />

<h3 id="typescript">TypeScript</h3>
<pre><code class="language-bash">npm install -g typescript</code></pre>
<p><strong>만약 <code>tsconfig.json</code> 파일이 없는 경우</strong></p>
<pre><code class="language-bash">npx tsc --init</code></pre>
<p><br /><br /></p>
<hr />

<p>** 참고한 글 **
<a href="https://rominlamp.tistory.com/36">[React] npx create-react-app으로 프로젝트 생성 시 발생하는 @testing-library/react 호환 문제 (Feat. React 19)</a>
<a href="https://velog.io/@yongyong_21/React-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-%EC%B4%88%EA%B8%B0%EC%84%B8%ED%8C%85-%EA%B0%9C%EC%9D%B8%EC%A0%81-%EC%A0%80%EC%9E%A5%EC%9A%A9">[React] 프로젝트 초기세팅 (개인적 저장용)</a></p>