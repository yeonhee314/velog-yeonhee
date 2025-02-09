<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/3a4c275d-fda2-4fa4-bcfd-49596b9b7452/image.png" /></p>
<h2 id="💡-polyfill이란">💡 Polyfill이란?</h2>
<blockquote>
<p>기본적으로 지원하지 않는 이전 브라우저에서 최신 기능을 제공하는데 필요한 코드</p>
</blockquote>
<p>JavaScript는 끊임없이 발전되어왔기 때문에 명세도 계속 변화했다.
이 과정에서 모든 브라우저는 발전된 스크립트 문법을 제공하지 않을 수 있기 때문에 <strong>브라우저 호환성 문제를 해결하기 위해 일종의 코드조각을 추가하는 것을 polyfill</strong>이라고 한다.</p>
<p>예를들면 오래된 버전의 브라우저에는 현재 JavaScript에서 사용하는 <code>Promise</code>나 <code>Set</code>객체가 없는 경우가 있다. <code>Array.prototype.at()</code> API는 Chrome92 이상에서만 지원되기도 한다.</p>
<p>이런 문제를 해결하기 위해서는 오래된 브라우저에서 없는 구현을 채워주어야 한다.
이렇게 구현을 채워주는 스크립트를 <strong>Polyfill</strong>이라고 한다.
대부분의 Polyfill은 이미 브라우저에 포함되어있는지 체크하고, 없으면 값을 채워주는 형태로 동작한다.</p>
<p>표준적으로 사용되는 Polyfill들은 <a href="https://github.com/zloirock/core-js">core-js Repository</a> 에 모여있다. </p>
<pre><code class="language-javascript">import 'core-js/actual';</code></pre>
<p>위 코드를 실행하면 대부분의 ECMAScript 표준 객체와 메서드를 오래된 브라우저에서도 사용할 수 있게 된다.</p>
<h2 id="개념-정리">개념 정리</h2>
<blockquote>
<ul>
<li>Polyfill이란 신규 JavaScript API를 오래된 버전의 브라우저에서도 사용할 수 있도록 하는 방법이다. 그렇지만 Polyfill스크립트가 많아지면 웹 성능이 나빠진다.</li>
</ul>
</blockquote>
<ul>
<li>Babel의 @babel/preset-env 스마트 프리셋을 이용하여 포함할 Polyfill 스크립트의 범위를 지정할 수 있다. 하지만 이 경우에도 최신 브라우저는 오래된 브라우저를 위한 Polyfill을 내려받는다.</li>
<li>User-agent에 따라 동적으로 Polyfill 스크립트를 생성할 수 있다. 이로써 최신 브라우저에서 내려받는 Polyfill 스크립트를 거의 없게 만들 수 있다.</li>
</ul>
<p><br /><br /></p>
<hr />

<p>*<em>참고한 글 *</em>
<a href="https://toss.tech/article/smart-polyfills">똑똑하게 브라우저 Polyfill 관리하기</a>
<a href="https://jinyisland.kr/post/polyfill-and-babel/">Polyfill이 무엇인가요??</a>
<a href="https://ko.javascript.info/polyfills">모던JavaScript 튜토리얼 폴리필</a></p>