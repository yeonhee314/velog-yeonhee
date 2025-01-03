<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/7f3cf5e2-1b15-4e45-bc92-e7186951b8b4/image.png" /></p>
<p><code>JSON</code>은 일반적으로 <strong>웹 서버와 데이터를 교환하는데 사용</strong>된다.
웹 서버로 데이터를 보낼 때, JavaScript 객체, 배열등은 서버와 교환할 수 없기 때문에 데이터는 문자열이어야 한다.</p>
<p>그래서 이를 문자열로 변환하는 <strong>직렬화(Serialization)</strong>가 필요하다.</p>
<p><code>JSON.stringify()</code>는 JavaScript 객체를 <code>JSON</code>문자열로 직렬화할 때 사용한다.</p>
<pre><code class="language-javascript">const obj = {name: &quot;연희&quot;, age: 28}
const jsonstring = JSON.stringify(obj);
console.log(jsonString); // '{&quot;name&quot;:&quot;연희&quot;,&quot;age&quot;:28}'</code></pre>
<p>위의 코드에서는 객체 <code>obj</code>가 <code>JSON.stringify(obj)</code>로 문자열로 변환된 것을 확인할 수 있다.
<br /></p>
<h3 id="💡-문자열화-시-제한-사항">💡 문자열화 시 제한 사항</h3>
<h4 id="순환-참조가-있을-때-에러-발생">순환 참조가 있을 때 에러 발생</h4>
<pre><code class="language-javascript">const obj = {};
obj.self = obj;
JSON.stringify(obj); // TypeError: Converting circular structure to JSON</code></pre>
<p>위의 코드에서 <code>obj.self= obj</code>로 인해 <code>obj</code>의 <code>self</code> 속성이 자기 자신을 참조한다.
이럴 경우 <code>obj</code>내부의 <code>self</code>가 <code>obj</code>를 참조하면서 무한 루프가 만들어진다.</p>
<p><code>obj</code>의 <code>self</code>속성을 직렬화하려고 보니 <code>obj</code>를 다시 참조하는 순환 구조를 발견하고 
직렬화를 중단한 뒤 <code>typeError</code>를 발생시킨다.</p>
<h4 id="함수-및-symbol은-무시">함수 및 Symbol은 무시</h4>
<pre><code class="language-javascript">const obj = {name : &quot;연희&quot;, greet: () =&gt; &quot;Hello, id:Symbol(&quot;id&quot;) };
console.log(JSON.stringify(obj)); // '{&quot;name&quot;:&quot;연희&quot;}'</code></pre>
<h2 id="javascript-배열을-문자열화하기">JavaScript 배열을 문자열화하기</h2>
<p>배열도 마찬가지로 문자화가 가능하다.</p>
<pre><code class="language-javascript">const arr = [&quot;hee&quot;, &quot;kim&quot;, &quot;lee&quot;];
const myJSON = JSON.stringify(arr);
console.log(myJSON); // [&quot;hee&quot;,&quot;kim&quot;,&quot;lee&quot;]</code></pre>
<p><code>JSON.stringify(arr)</code>로 JSON 형식의 문자열로 변환한다.
배열의 요소가 이미 문자열이므로 그대로 유지된다.</p>
<p><br /><br /></p>
<p>** 참고한 글 **
<a href="https://www.w3schools.com/js/js_json_stringify.asp">https://www.w3schools.com/js/js_json_stringify.asp</a>
<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify">https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify</a></p>