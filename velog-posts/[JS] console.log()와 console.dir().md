<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/ecd261b8-f852-4f8b-af00-665278ba8f1b/image.png" /></p>
<p><code>console.log</code>와 <code>console.dir</code>은 둘 다 브라우저 개발자 도구에서 디버깅 목적으로 사용되지만 출력되는 형식은 다르다.</p>
<h2 id="consolelog">console.log</h2>
<blockquote>
<ul>
<li>일반적인 로그 출력 메서드이다.</li>
</ul>
</blockquote>
<ul>
<li>JavaScript 객체를 출력할 때, 객체를 <strong>문자열화</strong>하여 표시하거나, 브라우저의 기본 포맷에 따라 구조화된 데이터를 보여준다.</li>
</ul>
<pre><code class="language-javascript">const obj = {name: '연희', age: 28};
console.log(obj);</code></pre>
<p><strong>출력 결과</strong>
<img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/35d1da7f-4a9e-4611-a23b-0f1770fb695a/image.png" /></p>
<pre><code class="language-css">{name: &quot;연희&quot;, age: 28}</code></pre>
<p>객체를 선언해서 출력값을 확인했을 때 객체를 문자열로 표현해서 보여준다.
만약 DOM요소를 <code>console.log</code>로 찍어보면 HTML 태그 구조를 보여준다.</p>
<hr />
<h2 id="consoledir">console.dir</h2>
<blockquote>
<ul>
<li>객체의 <strong>프로퍼티</strong>와 <strong>메서드</strong>를 트리 형태로 출력한다.</li>
</ul>
</blockquote>
<ul>
<li>DOM요소를 출력할 때는 해당 요소의 JavaScript 객체 표현(속성 및 메서드)를 보여준다.</li>
<li>객체 내부의 구조나 속성 접근 방식을 확인할 때 유용하다.</li>
</ul>
<pre><code class="language-javascript">const obj = {name: '연희', age: 28};
console.dir(obj);</code></pre>
<p>** 출력 결과 **
<img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/d609b8ae-497f-45c7-bedb-a06a61ed6396/image.png" /></p>
<pre><code class="language-css">Object
    age: 28
    name: &quot;연희&quot;</code></pre>
<br />

<p>객체를 선언해서 <code>console.dir</code> 로 확인했을 때 객체가 <strong>트리구조</strong> 로 출력된다.
<strong>트리구조는 데이터가 부모-자식 관계를 가지며 계층적으로 연결</strong> 되어있는 것을 말한다.</p>
<p>여기서 <code>Object</code>는 <strong>루트(root)노드</strong>이고, 
<code>age</code>와 <code>name</code>은 <code>Object</code>의 <strong>자식 노드(child)</strong>이다.</p>
<p><br /><br />
따라서, ** HTML구조를 확인<strong>하거나 ** 코드 실행 상태를 확인할 때</strong>등  <code>console.log</code> 를 사용하고
<strong>객체의 속성/메서드 탐색</strong>이 필요하면 <code>console.dir</code>을 사용한다.</p>