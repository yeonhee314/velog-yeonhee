<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/4ef306cf-805b-48d4-a8c0-19a304946838/image.png" /></p>
<h2 id="💡-화살표-함수-구문">💡 화살표 함수 구문</h2>
<h3 id="익명-함수">익명 함수</h3>
<pre><code class="language-javascript">export default function(){
    console.log(&quot;Hello&quot;);
}</code></pre>
<p>위와 같이 함수를 모듈화해서 <code>default</code>로 내보낼 수 있다.</p>
<h3 id="화살표-함수는-function-키워드를-작성하지-않는다">화살표 함수는 function 키워드를 작성하지 않는다.</h3>
<pre><code class="language-javascript">export default (userName, message) =&gt;{
    return userName + message;
}</code></pre>
<h3 id="하나의-매개변수만-사용하는-경우-묶는-괄호를-생략할-수-있다">하나의 매개변수만 사용하는 경우 묶는 괄호를 생략할 수 있다.</h3>
<pre><code class="language-javascript">(uerName) =&gt; { return `Hello ${userName}`; }
userName =&gt; { return `Hello ${userName}`; }</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/c3abfab5-f7f0-45fa-9423-6e87fa6813a4/image.png" /></p>
<blockquote>
<ul>
<li>하지만 함수에 <strong>매개변수가 없는 경우</strong>에는 <strong>괄호를 생략해서는 안된다</strong>.</li>
<li>함수가 <strong>둘 이상의 매개변수</strong>를 받는 경우에도 <strong>괄호를 생략해서는 안된다</strong>.
() =&gt; {...};</li>
</ul>
</blockquote>
<h3 id="함수-본문-중괄호-생략하기">함수 본문 중괄호 생략하기</h3>
<p>화살표 함수에 <strong>반환문 외에 다른 로직이 없는 경우</strong>, <code>return</code>키워드와 중괄호를 생략할 수 있다.</p>
<pre><code class="language-javascript">(number) =&gt; { return number * 3; }  // 생략 하지 않고 작성한 구문
number =&gt; number * 3;          // return 키워드와 중괄호 생략
number =&gt; return number * 3; // 이 경우 return 키워드는 생략되어야 하므로 오류 발생
number =&gt; if(number === 2) { return 5; };    // 이 경우 if문은 반환될 수 없으므로 오류 발생</code></pre>
<p>만약 위와 같은 대안으로 자바스크립트 객체를 반환하려고 한다면 <strong>유효하지 않은 코드</strong>가 나올 수 있다.</p>
<pre><code class="language-javascript">number =&gt; { age : number };</code></pre>
<p>이는 객체를 반환하려고할 때 객체 리터럴이 중괄호 <code>{}</code> 안에 바로 반환되는 값으로 해석되기 때문에, 반환을 명시적으로 하려면 <code>return</code>키워드를 사용해야 한다.
여기서 발생하는 문제를 해결하려면 두가지 방법이 있다.</p>
<h4 id="1-return키워드를-사용">1. <code>return</code>키워드를 사용</h4>
<pre><code class="language-javascript">    const getAge = (numger) =&gt;{
         return { age: number }; 
    };

console.log(getAge(29));    // { age: 29 }</code></pre>
<p>위 방법은 <code>return</code> 키워드를 명시적으로 사용하는 방법이다.</p>
<h4 id="2-객체를-반환하는-구문을-한-줄로-쓰고싶다면-객체-리터럴-앞에-괄호를-추가">2. 객체를 반환하는 구문을 한 줄로 쓰고싶다면 객체 리터럴 앞에 괄호<code>()</code>를 추가</h4>
<pre><code class="language-javascript">const getAge = (number) =&gt; ({ age : number});
// const getAge = number =&gt; ({ age : number }); 

console.log(getAge(29));    // { age : 29 }</code></pre>
<p>위 방법은 객체 리터럴을 반환할 때 중괄호를 괄호로 감싸서 한 줄로 반환할 수 있게 하는 방법이다.</p>