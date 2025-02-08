<h2 id="csrclient-side-rendering">CSR(Client-side rendering)</h2>
<pre><code class="language-html">&lt;!DOCTYPE html&gt;
&lt;html&gt;
      &lt;body&gt;
      &lt;div id=&quot;root&quot;&gt;&lt;/div&gt;
      &lt;script src=&quot;/static/js/bundle.js&gt;&lt;/script&gt;
  &lt;/body&gt;
&lt;/html&gt;</code></pre>
<p>클라이언트 사이드 렌더링은 위의 코드를 예로 들었을 때 <code>bundle.js</code> 자바스크립트 파일의 다운로드와 파싱이 완료되며녀 리액트가 작동해서 모든 DOM을 불러오고 비어있는 <code>&lt;div id=&quot;root&quot;&gt;</code>에 저장한다.</p>
<p>이 접근방식에는 작업 수행에 시간이 걸리고, 작업 진행 중에 사용자에게 흰 색 화면만 보인다.
그리고 기능을 추가하면 자바스크립트 번들의 크기가 증가하고 작업 시간도 비례해 늘어난다.</p>
<br />

<h2 id="ssrserver-side-rendering">SSR(Server-side rendering)</h2>
<p>위와 같은 CSR의 단점을 개선하기 위해 서버사이드 렌더링이 등장했다.
SSR에서는 CSR처럼 텅 빈 HTML 파일을 전송하는 것이 아니라 
<strong>직접 App을 렌더링하고 HTML을 생성한다.</strong>
결과적으로 사용자는 완전한 형식의 HTML문서를 받는다.</p>
<hr />

<p>리액트를 클라이언트 단에서도 실행해서 인터랙티브한 부분을 처리해야하므로 HTML 파일에는 여전히 <code>&lt;script&gt;</code>태그가 포함된다.</p>
<p><br /><br /></p>
<hr />

<p>*<em>참고한 글 *</em>
<a href="https://yozm.wishket.com/magazine/detail/2271/">새로 등장한 '리액트 서버 컴포넌트'이해하기</a></p>