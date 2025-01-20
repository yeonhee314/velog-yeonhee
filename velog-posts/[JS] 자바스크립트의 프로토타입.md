<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/748418c4-af64-4d43-8c1b-b17dda92053e/image.png" /></p>
<p><strong>C++과 Java</strong>는 클래스를 이용해서 객체를 생성하는 <strong>클래스 기반 객체 지향 언어</strong>이다.
반면, <strong>JavaScript</strong>는 클래스가 아닌 프로토타입을 상속하는 <strong>프로토타입 기반 객체지향 언어</strong>이다.
<br /></p>
<img src="https://velog.velcdn.com/images/yeonhee314/post/723f9492-b781-479b-9f3a-e9711736a36c/image.png" />
<span style="font-size: 14px;">조코딩님 영상보다가 댓글이 비유가 너무 찰떡이라 가져왔다.</span>

<br />

<hr />

<h2 id="프로토타입-개념">프로토타입 개념</h2>
<p><strong>프로토 타입은 디자인 패턴</strong>이다.</p>
<blockquote>
<p>프로토타입은 객체를 효율적으로 생성하는 방법을 다루는 패턴 중 하나인데,
주로 객체를 생성하는 비용이 클 때 이를 회피하기 위해 사용된다.</p>
</blockquote>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/b9069be0-4c97-412e-acdb-544919a594a5/image.png" /></p>
<p><strong>프로토타입은 원본 객체가 존재하고, 그 객체를 복제해서 새로운 객체를 생성하는 방법</strong>이다.</p>
<p>즉, <strong>프로토타입 패턴이란 객체를 생성할 때 원본이 되는 객체를 복사해서 생성하는 패턴</strong>이라고 할 수 있다.
<br /></p>
<h2 id="자바스크립트의-프로토타입">자바스크립트의 프로토타입</h2>
<p>프로토타입을 지원하는 자바스크립트의 경우 모든 객체를 생성할 때 프로토타입을 사용하기 때문에
객체를 생성하기만 해도 프로토타입 패턴이 적용된다.</p>
<p>자바스크립트는 객체를 생성할 때 함수를 사용해서 생성한다.</p>
<pre><code class="language-javascript">console.log(Object);
console.log(typeof Object);</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/7f1802e1-c6e7-4418-a6e8-3c5a66012bbe/image.png" /></p>
<p>자바스크립트에서의 생성자는 클래스가 아니라 함수가 가지고 있다는 것을 확인할 수 있다.
만약 클래스기반 언어라면 Object는 클래스겠지만, 자바스크립트에서는 클래스가 아닌 함수이다.
<br /></p>
<blockquote>
<ol>
<li>프로토타입 패턴은 객체를 생성할 때 원본 객체를 복제하여 생성하는 방법이다.</li>
<li>자바스크립트는 객체를 생성할 때 프로토타입 패턴을 사용한다.</li>
<li>자바스크립트는 객체를 생성할 때 함수를 사용한다.</li>
</ol>
</blockquote>
<pre><code class="language-javascript">function Person() {}
const hee = new Person();

console.log(hee);
console.log(typeof hee);
</code></pre>
<p>자바스크립트는 함수를 사용해서 객체를 생성하기 때문에 객체와 유사한 느낌으로 객체 생성이 가능하다.
위의 예제에서 <code>hee</code> 객체는 <code>Person</code>함수를 복제한 것이 아니라 <strong><code>Person</code>함수의 프로토타입 객체를 복제</strong>했다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/450a00c5-c62c-4fbc-a7d2-88d9d6c94c78/image.png" /></p>
<p>객체를 생성하면서 함수를 복제했다면, 생성된 객체는 <code>object</code>타입이 아니라 <code>function</code>이어야 하는데 <code>hee</code>객체는 <code>object</code>타입을 가지고 있다.</p>
<p>즉, 이 함수 자체가 아니라 다른 객체 타입의 무언가를 복제했다는 것이고,
그 <strong>원본 객체가 <code>Person</code> 함수의 프로토타입 객체</strong>인 것이다.</p>
<blockquote>
<p><code>Person</code>함수의 프로토타입을 명시적으로 선언하지 않았지만,
<strong>자바스크립트는 함수가 생성될 때 자동으로 그 함수의 프로토타입 객체도 함께 생성하고 해당 함수의 <code>prototype</code> 프로퍼티에 연결</strong>해둔다.</p>
</blockquote>
<pre><code class="language-javascript">function Person() {}

console.log(Person.prototype);
console.log(typeof Person.prototype);</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/edda40f0-7eab-4f6f-97aa-db43c91a99ed/image.png" /></p>
<p>위 코드에서 확인할 수 있는 점은 함수 <code>Person</code>만 선언했는데 <code>console.log</code>로 <code>Person.prototype</code>을 찍어보았을 때 프로퍼티에 뭔가 잔뜩 가지고 있는 객체가 같이 붙어서 나왔다.
여기서 알 수 있는 점은, <strong>함수를 생성하면 무조건 그 함수의 프로토타입 객체도 함께 생성</strong>된다는 것이다.
그리고 이 프로토타입 객체는 함수를 사용해서 새로운 객체를 생성할 때 원본 객체 역할을 해줄 객체를 의미한다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/117b0ecc-1463-413f-98cc-6dfdb75cc603/image.png" /></p>
<p>즉, <code>new Person()</code>라는 문법을 사용해서 새로운 객체를 만들면 <code>Person</code>함수 자체가 아니라 <code>Person</code>함수가 생성될 때 함께 생성된 <code>Person</code>함수의 프로토타입 객체를 복제해서 새로운 객체를 만든다.</p>
<p>여기서 그럼 <code>constructor</code>과 <code>__proto__</code>는 뭘까?</p>
<h3 id="constructor">constructor</h3>
<p>함수가 생성되며 생성된 프로토타입 객체는 모두 <code>constructor</code>라는 프로퍼티를 가지고 있다.
그리고 이 프로퍼티에는 프로토타입 객체가 생성될 때 선언했던 함수가 들어있다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/c0b3cf80-1e9a-4bf8-a68b-b2feb7e017b9/image.png" /></p>
<p>함수를 선언하면 함수와 함께 해당 함수의 프로토타입 객체도 함께 생성되고 이 둘을 연결한다.
<img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/284430c9-3697-4d55-868c-4c9ffc9fa33e/image.png" /></p>
<p>이 때 함수는 프로토타입 객체의 <code>constructor</code>프로퍼티로 연결되고, 프로토타입 객체는 함수의 <code>prototype</code>프로퍼티로 연결된다.
함수와 프로토타입 객체는 서로 연결되어있다.</p>
<h3 id="proto"><strong>proto</strong></h3>
<p>함수를 통해 새롭게 생성된 객체는 원본 객체와의 연결을 가지고 있다.
이때 이 연결을 <strong>프로토타입 링크(Prototype Link)</strong>라고 한다.</p>
<blockquote>
<p>자바스크립트에서 단순 원시 타입(simple primitive)인 문자열, 숫자, 불리언, null, undefined를 제외한 모든 타입은 객체다.</p>
</blockquote>
<p>자바스크립트에서 객체는 원형 객체로부터 생성되며, 생성된 객체는 원형에 대한 프로토타입 링크 <code>__proto__</code>를 갖게 된다.</p>
<p><code>Object.prototype</code>을 제외한 자바스크립트 내의 모든 객체는 원본 객체를 기반으로 복사되어 생성되었기 때문에, 자신의 원본 객체로 연결되어 있는 프로토타입 링크 또한 모든 객체가 가지고있다. 이 때 이 링크가 담기는 프로퍼티가 <code>__proto__</code>프로퍼티이다.</p>
<p>즉, <code>Person</code>함수를 사용하여 생성한 객체는 <code>Person.prototype</code>객체를 복사하여 생성된 객체이므로, 이 객체들은 원본인 <code>Person.prototype</code> 객체를 자신의 <code>__proto__</code>프로퍼티에 연결해두는 것이다.</p>
<p><code>Object.protype.__proto__</code>는 존재하지 않는다.</p>
<pre><code class="language-javascript">function Person() {}
const hee = new Person();
console.log(hee.__proto__ === Person.prototype);
</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/9ff8f586-38bb-47df-a20e-f533ec0f9c92/image.png" /></p>
<h3 id="프로토타입-체인">프로토타입 체인</h3>
<p>String, Boolean, Array, ... 자바스크립트 내 존재하는 모든 객체는 바로 <code>Object</code>함수의 프로토타입인 <code>Object.prototype</code>을 시작으로 해서 복제된다.</p>
<p>위의 <code>__proto__</code>설명에서 <code>Object.protype.__proto__</code>는 존재하지 않는다고 했는데(프로토타입링크, 즉 원본 객체로 통하는 링크가 없다.) 그 이유는 바로 <code>Object.prototype</code>이 모든 객체들의 조상이기 때문이다.</p>
<p>자바스크립트의 모든 함수는 자신의 원본으로 <code>Function.prototype</code>객체를 원본으로 가진다.
그리고 <code>Function.prototype</code>은 결국 객체이기 때문에, 당연히 원본으로 <code>Object.prototype</code>객체를 원본으로 가진다.</p>
<p>만약 여기서 한번 더 올라간다면 <code>TypeError</code>가 발생한다.
<code>Object.prototype</code>객체의 원본 객체인 <code>Object.prototype.__proto__</code>는 <code>null</code>이기 때문이다.</p>
<p>즉, <code>Object</code>의 위로는 조상이 없다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/ea1d3cbd-56e0-45d5-aad8-2d10d265f85a/image.png" />
<a href="https://evan-moon.github.io/2019/10/23/js-prototype/">출처</a></p>
<p>이 관계를 다이어그램으로 살펴보면 위와 같다.</p>
<br />
<hr />

<p><strong>참고,인용한 글/출처</strong>
<a href="https://evan-moon.github.io/2019/10/23/js-prototype/">[JS 프로토타입] 자바스크립트의 프로토타입 훑어보기</a>
<a href="https://ui.toast.com/weekly-pick/ko_20160603">프로토타입 기반 언어, 자바스크립트</a></p>