<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/23ab1604-fa3e-411a-99e7-7babd6bed37c/image.png" /></p>
<h2 id="💡-자바스크립트의-동기와-비동기">💡 자바스크립트의 동기와 비동기</h2>
<p>자바스크립트는 싱글 스레드 언어이므로 한 번에 하나의 작업만 수행할 수 있다.
즉, 이전 작업이 완료되어야 다음 작업을 수행할 수 있다.</p>
<h3 id="동기synchronous">동기(Synchronous)</h3>
<p>각 함수와 코드들이 <strong>위에서 아래로 차례로 동작하는 방식</strong>이라고 할 수 있는데 이러한 코드 순차 실행이 <strong>동기(Synchronous)</strong>이다.
동기적 제어 흐름은 싱글 스레드 환경에서 메인 스레드를 긴 시간 점유하면 프로그램을 멈추게 한다. 동기식 제어는 사용자의 요청을 실시간으로 처리할 수 없으므로 사용자가 여러명이라면 매우 비효율적이다. </p>
<h3 id="비동기asynchronous">비동기(Asynchronous)</h3>
<p>자바스크립트로 여러 작업을 동시에 처리하기 위해 <strong>비동기(Asynchronous)</strong>라는 개념을 도입하여 <strong>특정 작업의 완료를 기다리지 않고 다른 작업을 동시에 수행</strong>할 수 있도록 했다.
비동기는 메인 스레드가 작업을 다른 곳에 인가하여 처리되게 하고, 그 작업이 완료되면 콜백 함수를 받아 실행하는 방식으로, 쉽게 말해 작업을 백그라운드에 요청하여 처리하게 하여 <strong>멀티로 작업을 동시에 처리하는 것</strong>으로 보면된다.</p>
<p>서버에 데이터를 요청하고 응답을 받아야하는 작업이 있다면 응답이 오는 것과 상관없이 다른 작업을 계속 이어나가 병렬로 작업을 동시 처리가 가능해져 프로그램의 흐름이 멈추거나 지연되지 않게 된다. 
따라서 작업이 <strong>병렬적으로 동시에 처리</strong>되고 코드 실행시간이 줄어들게된다.</p>
<h3 id="비동기-예제">비동기 예제</h3>
<blockquote>
<ul>
<li>DOM Element의 이벤트 핸들러 : 마우스, 키보드 입력, 페이지 로딩, ...</li>
</ul>
</blockquote>
<ul>
<li><p>타이머 : 타이머 API(setTimeout, ...), 애니메이션 API(requestAnimationFrame)</p>
</li>
<li><p>서버에 자원 요청 및 응답 : fetch API, AJAX, ...</p>
<p>백그라운드 실행, 로딩창 실행, 서버로 요청을 보내고 응답을 기다리는 작업이나 큰 용량의 파일을 로딩하는 작업은 비동기적이어야 효율적이다.</p>
<br />

</li>
</ul>
<h2 id="자바스크립트의-이벤트루프event-loop">자바스크립트의 이벤트루프(Event Loop)</h2>
<blockquote>
<ul>
<li>자바스크립트 엔진은 비동기 처리를 제공하지 않는다.</li>
</ul>
</blockquote>
<ul>
<li>대신 비동기 코드는 정해진 '함수'를 제공하여 활용할 수 있다.</li>
<li>이 함수들을 API(Application Programming Interface)라 한다.</li>
<li>비동기 API의 예시로 <code>setTimeout</code>, <code>XMLHttpRequest</code>, <code>fetch</code>등의 <strong>Web API</strong>가 있다.</li>
<li>node.js의 경우 파일 처리 API, 암호화 API등을 제공한다.</li>
</ul>
<p>비동기로 동작하는 핵심요소는 자바스크립트 언어가 아니라 브라우저라는 소프트웨어가 가지고 있다고 보면 된다.
Node.js에서는 libuv 내장 라이브러리가 처리한다.</p>
<br />

<h3 id="💡-이벤트-루프는-브라우저-동작을-제어하는-관리자다">💡 이벤트 루프는 브라우저 동작을 제어하는 관리자다.</h3>
<p>!youtube[eiC58R16hb8?si=onRkNmhTaNBw4u1M]
자바스크립트 내부의 비동기 동작을 이해하기 위해서는 이벤트 루프등의 개념을 알아야한다.</p>
<p>싱글 스레드인 <strong>자바스크립트의 작업을 멀티 스레드로 돌려 작업을 동시에 처리</strong>시키게 하거나 <strong>여러 작업 중 어떤 작업을 우선으로 동작시킬 것인지 결정</strong>하는 컨트롤을 하기 위해 존재하는 것이 <strong>이벤트 루프(Event Loop)</strong>이다.</p>
<p>이벤트 루프는 브라우저 내부의 Call Stack, Callback Queue, Web APIs 등의 요소들을 모니터링하면서 비동기적으로 실행되는 작업들을 관리하고, 이를 순서대로 처리하여 프로그램의 실행 흐름을 제어한다. </p>
<p>간단히 표현하자면 ** 브라우저의 동작 타이밍을 제어하는 관리자 **라고 볼 수 있다. </p>
<blockquote>
<p>그래서 자바스크립트는 싱글 스레드 언어임에도 불구하고 이벤트 루프를 통해 논블로킹 방식의 비동기적인 동시성 언어로 동작할 수 있다.</p>
</blockquote>
<h2 id="💡-비동기를-처리하기-위한-기법">💡 비동기를 처리하기 위한 기법</h2>
<h3 id="📑-콜백callback--가장-원초적인-비동기-방식">📑 콜백(callback) : 가장 원초적인 비동기 방식</h3>
<p>비동기를 다룰 때 자주 등장하는 개념이(callback)함수이다. 콜백 함수는 자바스크립트의 일급 객체 특성을 이용해서 함수의 매개변수에 함수 자체를 넘겨, 함수 내에서 매개변수 함수를 실행하는 기법을 말한다. </p>
<p><strong>비동기 방식은 요청과 응답의 순서를 보장하지 않기</strong> 때문에 응답의 처리 결과에 의존하는 경우에는 콜백 함수를 이용하여 작업 순서를 간접적으로 끼워 맞출 수 있다.</p>
<pre><code class="language-javascript">function getDB(callback){
    // dB로부터 3초 후에 데이터 값을 받아온 후 콜백함수 호출
  setTimeout(() =&gt; {
      const value = 100;
    callback(value);
  }, 3000);
}

function main(){
     // 호출할 작업에 콜백 함수를 넘긴다. 
  getDB(function(value) {
      let data = value * 2;
    console.log('data의 값 : ', data);
  });
}

main();</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/f6bfcec7-0b49-43de-8b70-f1de8c22cae4/image.png" />
위의 코드는 콜백 함수 내에서 <code>data</code>변수의 값을 받아 출력하므로, 비동기 작업이 완료된 후에 출력되게 된다.</p>
<p><strong>즉, 콜백함수는 비동기 함수에서 작업 결과를 전달받아 처리하는데 사용되어 작업 순서를 맞출 수 있게 되는 것</strong>이다.
따라서 비동기 함수와 콜백 함수는 서로 밀접한 관계를 가지고 있다고 말하는 것이다.</p>
<p>다만 너무 복잡하게 얽힌 비동기 처리 때문에 콜백 함수 방식은 <strong>코드 복잡도를 증가</strong>시켜, 개발자가 어플리케이션의 흐름을 읽기 어려워지는 등의 문제가 있어 잘못하면 <strong>콜백 지옥(callback hell)</strong>에 빠질 수 있다는 단점이 있다.</p>
<br />

<h3 id="📑-프로미스promise--콜백을-체이닝으로-개선한-방식">📑 프로미스(Promise) : 콜백을 체이닝으로 개선한 방식</h3>
<p>콜백함수는 엄연히 말하자면 비동기를 순차적으로 처리하기 위한 일종의 '편법'같은 것이지 정식으로 지원하는 비동기 전용 함수가 아니다.
콜백함수의 코드 형태는 콜백 함수가 중첩되면서 들여쓰기 수준이 깊어져서 코드의 가독성을 떨어트리고 코드 흐름을 파악하기 힘들어진다. 
또한 콜백 함수마다 에러 처리를 따로 해줘야하고 에러가 발생한 위치를 추적하기 힘들게 된다.</p>
<p>따라서 자바스크립트의 <code>Promise</code>객체는 이러한 한계점을 극복하기 위해 비동기 처리를 위한 전용 객체로 탄생했다.
<code>Promise</code>객체를 이용하면 비동기 작업의 갯수가 많아져도 들여쓰기 코드의 깊이가 깊어지지 않게 된다. </p>
<blockquote>
<p> Promise 객체는 비동기 작업이 맞이할 미래의 완료 또는 실패와 그 결과 값을 나타낸다.
또한, Promise는 세가지 상태를 가질 수 있다.
<strong>1.대기(pending)</strong>: 이행하지도, 거부하지도 않은 초기 상태
<strong>2.이행(fulfilled)</strong>: 연산이 성공적으로 완료됨
<strong>3.거부(rejected)</strong>: 연산이 실패함</p>
</blockquote>
<p><code>Promise</code>를 사용하면 <strong>비동기 연산을 동기 연산처럼 사용</strong>할 수 있다.
<code>async</code>하다는 것은 요청에 대한 결과가 동시에 일어나지 않기 때문에 <strong>완료시점을 예측할 수 없다는 말</strong>인데 <code>Promise</code>는 **비동기 작업이 미래의 어떤 시점에 결과를 제공해줄 것이라고 약속(Promise)`을 해준다.</p>
<pre><code class="language-javascript">function getDB(){
  return new Promise((resolve =&gt; {
      setTimeout(()=&gt; {
        const value = 100;
          resolve(value);
    }, 3000);
  }));
}

function main(){
 getDB()
  .then((value) =&gt; {
   let data = value * 2;
     console.log(`data의 값 : ${data}`);
 })
  .catch((error) =&gt; {
     console.error(error);
 });
}

main();</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/44c668c4-e4f6-478d-874e-f53ba7763d3e/image.png" /></p>
<p><code>Promise</code>객체를 생성하려면 <code>new</code>키워드와 <code>Promise</code>생성자 함수를 이용하면 된다.
이 때 <code>Promise</code>생성자 안에 두개의 매개변수를 가진 콜백 함수를 넣게 되는데,
<strong>첫번째 인수는 작업이 성공했을 때 성공(resolve)임을 알려주는 객체</strong>이며,
<strong>두번째 인수는 작업이 실패했을 때 실패(reject)임을 알려주는 오류 객체</strong> 이다.</p>
<p>일반적으로 <code>Promise</code>는 별도 함수로 감싸서 사용하는 것이 일반적이다.
함수를 만들고 그 함수를 호출하면 <code>Promise</code>생성자를 <code>return</code>함으로써, 곧바로 <strong>생성된 <code>Promise</code>객체를 함수 반환 값</strong>으로 얻어 사용하는 기법이다.</p>
<p>이렇게 <code>Promise</code>를 생성하여 반환하는 함수를 <strong>프로미스 팩토리 함수</strong>라고 불리우기도 한다.</p>
<h4 id="promise객체를-함수로-만드는-이유"><code>Promise</code>객체를 함수로 만드는 이유</h4>
<blockquote>
<p><strong>1. 재사용성</strong> : 프로미스 객체를 함수로 만들면 필요할 때마다 호출하여 사용함으로써, 반복되는 비동기 작업을 효율적으로 처리할 수 있다.
*<em>2. 가독성 *</em>: 프로미스 객체를 함수로 만들면 코드의 구조가 명확해져서 비동기 작업의 정의와 사용을 분리하여 코드의 가독성을 높일 수 있다.
*<em>3. 확장성 *</em> : 프로미스 객체를 함수로 만들면 인자를 전달하여 동적으로 비동기 작업을 수행할 수 있다. </p>
</blockquote>
<br />


<h3 id="📑-asyncawait--promise를-동기-코드-처럼-작성-가능">📑 async/await : Promise를 동기 코드 처럼 작성 가능</h3>
<p>하지만 프로미스도 완벽한 해결책은 아니다. 왜냐면 Callback Hell이 있듯이 지나친 then 핸들러 함수의 남용으로 인한 Promise Hell이 존재하기 때문이다. 즉, 프로미스가 여러개 연결되면 코드가 길고 복잡해질 수 있다. </p>
<p>그래서 자바스크립트는 aync/await이라는 문법이 추가되었다.
async/await은 프로미스를 기반으로 하지만, 마치 동기 코드처럼 작성할 수 있게 해준다.
비동기 작업을 쉽게 읽고 이해할 수 있게 해주기 때문에 비동기 작업을 처리할 일이 있다면 async/await 방식을 쓰는 것이 보통이다. </p>
<pre><code class="language-javascript">function getDB() {
    return new Promise((resolve, reject) =&gt; {
        // 데이터베이스에서 값을 가져오는 3초 걸린다고 가정 (비동기 처리)
        setTimeout(() =&gt; {
            const value = 100;
            resolve(value); // Promise 객체 반환
        }, 3000);
    });
}

async function main() {
    let data = await getDB(); // await 키워드로 Promise가 완료될 때까지 대기
    data *= 2;
    console.log('data의 값 : ', data);
}
main();</code></pre>
<p><code>async</code>와 <code>await</code>은 절차적 언어에서 작성하는 코드와 같이 사용법이 간단한다.
<code>function</code>키워드 앞에 <code>async</code>만 붙여주면 되고 비동기로 처리되는 부분 앞에 <code>await</code>만 붙여주면 된다.</p>
<p><code>async</code> 키워드는 <code>await</code>을 사용하기 위한 선언문 정도로 이해하면 된다.
즉, <code>function</code>앞에 <code>async</code>를 붙여줌으로써, 함수 내에 <code>await</code>키워드를 사용할 수 있게 된다.
이는 반대로 말하면 <code>await</code> 키워드를 사용하기 위해서는 반드시 <code>async function</code>이 정의가 되어 있어야 한다는 말과 같다. </p>
<h4 id="💡-그렇다면-무조건-await이-정답">💡 그렇다면 무조건 await이 정답?</h4>
<p>이렇게 보면 async/await이 비동기를 처리함에 있어 callback이나 Promise방식보다 훨씬 좋아보이지만, 경우에 따라 코드가 복잡해질 수도 있다.
따라서 이 비동기 처리에 대한 3가지 방식은 용도에 맞춰서 적절히 사용해야 한다.</p>
<p>왜냐하면 callback 방식은 별 다른 키워드 없이도 정말 단순하게 구현할 수 있는 문법이기 때문에, 콜백 지옥을 맞이할 정도의 복잡한 상황이 아닐 때면 오히려 사용하면 가독성이 좋다. 대표적인 예로 Node.js의 Express 프레임워크는 서버 라우팅을 콜백 함수로 처리하는 방식을 제공한다.</p>
<p>따라서, 콜백 함수는 복잡하기 않고 비교적 심플한 비동기 작업을 처리해야 할 때 사용하면 오히려 프로미스 방식보다 더 좋을 수 있다. 반면에 비교적 복잡한 비동기 작업을 처리할 때는 Promise 객체를 사용하면 코드를 보다 간결하게 작성할 수 있다.</p>
<h2 id="마치며">마치며...</h2>
<p>내부에서 동기처럼 작동하는데 뭐가 비동기라는지 처음에 의문이 들었다.😥
핵심은 <strong>작업을 기다리는 동안 다른 코드가 실행될 수 있다 *<em>는 점이라는 걸 알았고,
<code>await</code>을 사용하면 코드가 동기처럼 보이지만 실제로는 기다리는 동안 메인 스레드는 다른 작업을 수행(UI 업데이트, 이벤트 처리 등..)할 수 있고, <code>Promise</code>도 마찬가지로 *</em>백그라운드에서 작업이 끝날 때까지 기다리는 동안 다음 코드가 실행</strong> 될 수 있다는 것을 알았다.</p>
<p>비동기의 본질은 작업이 끝날 때까지 기다리지 않고 다음 작업을 실행할 수 있다!!!!</p>
<p><br /><br /></p>
<hr />

<p>** 출처 **
<a href="https://inpa.tistory.com/entry/%F0%9F%8C%90-js-async">자바스크립트의 핵심 '비동기' 완벽 이해</a>
<a href="https://velog.io/@jwo0o0/Javascript-%EB%8F%99%EA%B8%B0%EC%99%80-%EB%B9%84%EB%8F%99%EA%B8%B0">[Javascript] 자바스크립트가 비동기를 처리하는 방법 - callback function, Promise, async/await</a>
<a href="https://velog.io/@mieum/Javascript-%EB%B9%84%EB%8F%99%EA%B8%B0-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0">🚀 Javascript 비동기 확실하게 이해하기! (promise, async/await)+ HTTP, REST API, fetch API</a>
<a href="https://inpa.tistory.com/entry/%F0%9F%94%84-%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%9D%B4%EB%B2%A4%ED%8A%B8-%EB%A3%A8%ED%94%84-%EA%B5%AC%EC%A1%B0-%EB%8F%99%EC%9E%91-%EC%9B%90%EB%A6%AC">🔄 자바스크립트 이벤트 루프 동작 구조 &amp; 원리 끝판왕</a>
<a href="https://yong-nyong.tistory.com/71">[JavaScript] 이벤트 루프(Event Loop)에 대해서 파헤쳐 봅시다.</a>
<a href="https://dev.to/lydiahallie/javascript-visualized-event-loop-3dif">✨♻️ JavaScript Visualized: Event Loop</a>
<a href="https://inpa.tistory.com/entry/JS-%F0%9F%93%9A-%EB%B9%84%EB%8F%99%EA%B8%B0%EC%B2%98%EB%A6%AC-Promise">📚 자바스크립트 Promise 개념 &amp; 문법 정복하기</a>
<a href="https://inpa.tistory.com/entry/JS-%F0%9F%93%9A-%EB%B9%84%EB%8F%99%EA%B8%B0%EC%B2%98%EB%A6%AC-async-await">📚 자바스크립트 Async/Await 개념 &amp; 문법 정복</a></p>