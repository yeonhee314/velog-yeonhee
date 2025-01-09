<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/452b20d6-513a-4ea9-8b69-00456d2db52b/image.png" /></p>
<p><strong>객체</strong>와 <strong>객체 리터럴</strong>은 밀접하게 관련된 개념이지만 같은 말은 아니다.</p>
<h2 id="💡-객체란">💡 객체란?</h2>
<blockquote>
<ul>
<li>객체는 <strong>키-값 쌍</strong>으로 이루어진 데이터 구조이다.</li>
</ul>
</blockquote>
<ul>
<li>객체는 자바스크립트에서 데이터를 저장하고, 조작하며, 상호작용하는 데 사용되는 기본적인 자료형이다.</li>
<li>객체는 속성(property)과 메서드(method)를 가질 수 있다.</li>
</ul>
<p>객체는 자바스크립트의 핵심 데이터 타입 중 하나로, 다양한 타입의 데이터를 한 단위로 묶을 수 있는 복합 데이터 구조이다.</p>
<pre><code class="language-javascript">const person = {
     name: 'hee',
      age = 28,
      greet: function(){
        console.log('Hello World');
    }
}</code></pre>
<p>이 예제에서 <code>name</code>과 <code>age</code>는 속성(property)이고,
<code>greet</code>는 메서드(method)이다.</p>
<br />

<h2 id="💡-객체-리터럴이란">💡 객체 리터럴이란?</h2>
<blockquote>
<ul>
<li>객체 리터럴(object literal)은 <strong>객체를 생성하는 한 가지 방법</strong>이다.</li>
</ul>
</blockquote>
<ul>
<li>중괄호<code>{}</code>안에 <strong>키-값 쌍</strong>을 나열하여 객체를 정의한다.</li>
</ul>
<pre><code class="language-javascript">const car = { brand: 'Kia', model: 'K9' };</code></pre>
<p>위 코드에서 <code>car</code>는 객체이고, 이 객체는 <strong>리터럴 표기법</strong>을 사용해서 생성되었다.
자바스크립트는 다양한 방법(객체 리터럴, 생성자 함수, ...)으로 객체를 생성할 수 있지만 가장 간단하게 자주 사용되는 방법은 객체 리터럴을 사용하는 것이다.</p>
<p>정의할 때 키와 값은 <code>:</code>으로 구분하고, <code>,</code>로 여러 프로퍼티를 정의할 수 있다.</p>
<br />

<p>결론적으로 <strong>객체 리터럴</strong>은 <strong>객체를 생성하는 방법</strong>이고,
<strong>객체</strong>는 <strong>생성된 데이터 구조 자체</strong>이다.</p>