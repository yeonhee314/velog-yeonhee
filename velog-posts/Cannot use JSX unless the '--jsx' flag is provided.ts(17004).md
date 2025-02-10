<p>![] (<a href="https://velog.velcdn.com/images/yeonhee314/post/327cc938-7bfe-4461-8fec-3d0d4f0f918a/image.gif">https://velog.velcdn.com/images/yeonhee314/post/327cc938-7bfe-4461-8fec-3d0d4f0f918a/image.gif</a>)</p>
<hr />

<blockquote>
<p><strong>Cannot use JSX unless the '--jsx' flag is provided.ts(17004)</strong></p>
</blockquote>
<p>리액트 프로젝트에서 타입스크립트를 사용해보려고 했는데 오류가 발생했다.</p>
<br />

<h2 id="💡-해결-방법">💡 해결 방법</h2>
<p><strong><code>tsconfig.json</code> 파일에서 <code>jsx</code>항목을 빼먹었기 때문에 발생한 에러</strong>이다.</p>
<pre><code class="language-json">&quot;jsx&quot;: &quot;preserve&quot; /* Specify JSX code generation: 'preserve', 'react-native', or 'react'. */,</code></pre>
<p>위의 구문을 <code>tsconfig.json</code>의 <code>compilerOptions</code>안에 추가해주면 된다.</p>