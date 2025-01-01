<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/cc0e863e-d158-4ff3-9381-a03c53574cf2/image.png" /></p>
<p>대부분의 언어들이 <code>==</code> 연산자를 사용하는 것과 달리 
자바스크립트는 <code>==</code>연산자와 <code>===</code> 연산자 2개가 존재한다.</p>
<p>JavsScript에서 <code>===</code>와 <code>==</code>는 <strong>비교 연산자</strong>로, 두 값이 같은지를 비교한다.
그러나 동작 방식에 중요한 차이가 있다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/8a3622de-9c08-49d6-abdc-dde2c6bf817e/image.png" />
첫번째 비교는 <code>true</code>가 정수 타입의 1로 변환되어 비교 결과가 <code>true</code>로 출력 했다.
두번째 비교에서는 타입변환이 이뤄지지 않아서 <strong>정수형과 논리형이 타입비교</strong>를 해 결과를 <code>false</code>로 출력했다.</p>
<hr />
<br />

<h2 id="💡--느슨한-동등비교loose-equality">💡 <code>==</code> 느슨한 동등비교(Loose Equality)</h2>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/8ab306a7-ae47-4103-9dad-abe736d334ab/image.png" /></p>
<blockquote>
<ul>
<li><strong>값만 비교</strong>하며, 필요하면 JavaScript가 <strong>타입변환</strong>을 수행한다.</li>
</ul>
</blockquote>
<ul>
<li>타입이 다르면 내부적으로 값을 변환한 뒤 비교한다.</li>
</ul>
<pre><code class="language-javascript">console.log(5 == '5');            // true (문자열 '5'가 숫자 5로 변환)
console.log(null == undefined);    // true (특별 규칙으로 둘을 같다고 판단)
console.log(false == 0);        // true (false가 0으로 변환)
console.log('' == false);        // true (빈 문자열이 false로 변환)
</code></pre>
<p><code>==</code>연산자는 두 대상의 타입이 다를 경우 타입 변환 후 값의 비교를 수행한다.</p>
<br />

<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/07be0ec4-b6a7-4db1-87e9-cf49d15799e6/image.png" />
광선맨이 뚱이한테 <code>0 == []</code>를 들이밀었는데 뚱이는 <code>true</code>를 반환한다.
이유는 <code>==</code>(느슨한 동등 비교)가 타입 변환을 수행했기 때문이다.</p>
<p><code>[].toString()</code>은 빈 문자열(<code>&quot;&quot;</code>)을 반환하고, 
이 빈 문자열을 숫자로 변환하면 <code>0</code>이 된다.</p>
<p>결과적으로 <code>0 == 0</code>이 되므로 <code>true</code>를 리턴했다.
<br /></p>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/dd62786b-22af-4584-882f-04b4d58e6c48/image.png" /></p>
<p>그렇다면 광선맨은 <code>0 == []</code> 는 <code>0 == &quot;0&quot;</code>이니 <code>&quot;0&quot; == []</code> 를 들이민다.
뚱이는 <code>false</code>를 반환한다.</p>
<p>이는 왜 <code>false</code>일까?
타입 변환을 수행할 때 두 값의 타입에 따라 다른 변환 과정을 거치기 때문이다.</p>
<blockquote>
<h3 id="1-비교대상">1. 비교대상</h3>
</blockquote>
<ul>
<li><code>&quot;0&quot;</code>은 문자열</li>
<li><code>[]</code> 는 객체<blockquote>
<h3 id="2-객체를-비교할-때의-규칙">2. 객체(<code>[]</code>)를 비교할 때의 규칙</h3>
</blockquote>
</li>
<li><code>==</code>에서 <strong>객체가 숫자나 문자열과 비교되면,</strong> 객체는 먼저 <strong>원시 값(primitive value)</strong>으로 변환된다.</li>
<li><code>[].toString()</code>은 빈 문자열(<code>&quot;&quot;</code>)을 반환한다.<blockquote>
<h3 id="3-비교-결과">3. 비교 결과</h3>
</blockquote>
<ul>
<li><code>&quot;0&quot;</code>과 <code>[].toString()</code>은 → <code>&quot;0&quot; == &quot;&quot;</code> 으로 변환 된다.<blockquote>
<h3 id="4-문자열-비교">4. 문자열 비교</h3>
</blockquote>
</li>
<li><code>&quot;0&quot;</code>은 문자열 <code>&quot;0&quot;</code>, <code>&quot;&quot;</code> 은 빈 문자열이므로 서로 다르기 때문에 <code>false</code>를 반환한다.</li>
</ul>
</li>
</ul>
<br />

<hr />
<h2 id="💡--엄격한-동등비교strict-equality">💡 <code>===</code> 엄격한 동등비교(Strict Equality)</h2>
<p>엄격한 동등 비교는 타입을 변환하지 않는다.<img src="https://velog.velcdn.com/images/yeonhee314/post/56372243-cdf6-40f4-9518-31b2ab481900/image.png" width="500px;" /></p>
<blockquote>
<ul>
<li>** 타입과 값** 모두 같아야 <code>true</code>를 반환한다.</li>
</ul>
</blockquote>
<ul>
<li><strong>타입변환(type coercion)</strong>을 하지 않는다.</li>
</ul>
<pre><code class="language-javascript">console.log(5 === 5);                // true    (값과 타입이 같음)
console.log(5 === '5');                // false (값은 같지만, 타입이 다름)
console.log(null === null);            // true    (값과 타입이 같음)
console.log(null === undefined);     // false(값의 타입이 다름)
console.log(Nan === Nan);            // false (NaN은 자기 자신과 같지 않다는 특성이 있다.)</code></pre>
<p><code>===</code>는 엄격한 Equal Operator로써, 엄격하게 같음을 비교할 때 사용하는 연산자이다.
일반적으로는 <code>===</code>를 사용하는 것을 권장한다.</p>
<p><code>===</code>는 명확하고 예측 가능한 결과를 제공하고, <strong>의도하지 않은 타입 변환으로 인한 버그를 방지</strong>할 수 있다.</p>