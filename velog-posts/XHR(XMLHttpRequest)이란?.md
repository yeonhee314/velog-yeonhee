<h2 id="💡-xmlhttprequest">💡 XMLHttpRequest</h2>
<blockquote>
<p>브라우저는 주소창이나 HTML의 <code>form</code> 태그 또는 <code>a</code>태그를 통해 HTTP 요청 전송 기능을 기본 제공한다. 
*<em>자바스크립트를 사용하여 HTTP요청을 전송하려면 <code>XMLHttpRequest</code> 객체를 사용 *</em>한다.</p>
</blockquote>
<p>XHR(;XmlHttpRequest)는 Ajax 같이 페이지를 리프레쉬하지 않고서도 서버와 데이터를 받아오는 등의 인터랙션을 하기 위해 사용한다.</p>
<p><strong>Web API인 XMLHttpRequest 객체는 HTTP 요청 전송과 HTTP 응답 수신을 위한 다양한 메서드와 프로퍼티를 제공한다.</strong>
<br /></p>
<h3 id="💡-http">💡 HTTP</h3>
<p><strong>HTTP(;Hyper Text Transfer Protocol)는 서버와 클라이언트가 서로 데이터를 주고받기 위해 사용되는 통신 규약</strong>을 일컫는다.</p>
<p>웹 문서간에 링크를 통해 연결할 수 있는 프로토콜이며, 문서 뿐 아니라 다음과 같은 여러 종류의 데이터를 폭 넓게 전송할 수 있다.</p>
<blockquote>
<ol>
<li>HTML, TEXT</li>
<li>Image, 음성, 영상, 파일</li>
<li>JSON, XML(API)</li>
<li>거의 모든 형태의 데이터가 전송 가능</li>
</ol>
</blockquote>
<br />

<h3 id="📑-xmlhttprequest-객체-생성">📑 XMLHttpRequest 객체 생성</h3>
<p>XMLHttpRequest 객체는 <strong>XMLHttpRequest 생성자 함수를 호출하여 생성</strong>한다.
XMLHttpRequest 객체는 브라우저에서 제공하는 Web API이므로 브라우저 환경에서만 정상적으로 실행된다.</p>
<pre><code class="language-javascript">// XMLHttpRequest 객체 생성
const request = new XMLHttpRequest();
function onLoadListener(){
  console.log(request.responseText);
}
request.addEventListener(&quot;load&quot;, onLoadListener);
// HTTP 요청 초기화
request.open(&quot;GET&quot;, &quot;http://test.com&quot;);
// HTTP 요청 전송
request.send();
</code></pre>
<p>위와 같이 짧은 코드의 경우 <code>GET</code> 메소드를 실행해서 결과 값을 받아올 수 있다.</p>
<p>위 코드에 test.com이 아닌 실제 api의 url주소를 넣어보고 나서, 
chrome의 inspect창을 이용해서 XHR탭을 선택해주면 아래와 같이 정상적으로 <code>GET</code> 방식으로 <code>request</code> 요청을 확인할 수 있다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/12179389-c546-4ec3-98a3-7ec36a98ac00/image.png" />
나는 내 블로그 주소를 넣어서 확인해보았다.</p>
<br />

<h3 id="📑-xhr을-promise로-래핑하기">📑 XHR을 Promise로 래핑하기</h3>
<pre><code class="language-javascript">let request = obj =&gt; {
    return new Promise((resolve, reject) =&gt; {
        let xhr = new XMLHttpRequest();
        xhr.open('GET', obj.url);   // HTTP 요청 초기화

        // HTTP 요청 성공 시(onload 이벤트 핸들러)
        xhr.onload = () =&gt;{
            if(xhr.status === 200){
                console.log(xhr.response);
                resolve(xhr.response);
            }else{
                console.log(xhr.statusText);
                reject(xhr.statusText);
            }
        };
        xhr.send(); // HTTP 요청 전송
    });
}
request({url : &quot;https://velog.io/@yeonhee314/posts&quot;});</code></pre>
<p><code>XMLHttpRequeest</code>를 사용하여 비동기 HTTP GET요청을 보내는 <code>request</code>함수를 작성했다.
이 함수는 <code>Promise</code>를 반환한다. 
<code>Promise</code>는 비동기 작업의 성공(<code>resolve</code>) 또는 실패(<code>reject</code>)을 처리할 수 있게 한다.</p>
<p>처음에 <code>xhr.send(xhr.statusText);</code>라고 사용했는데 수정했다.
<code>xhr.send();</code>는 서버로 요청하는 메서드인데, <strong>GET 요청에서는 보통 파라미터 없이 호출</strong>해야 한다.
왜냐하면 <code>xhr.statusText</code>는 서버의 응답 상태 메시지를 나타내므로, 요청을 보내기 전에 값이 존재하지 않아서 의미가 없다.</p>
<p><br /><br /></p>
<p>** [참고한 글] **
<a href="https://dongribooth.tistory.com/11">1. Promise로 XMLHttpRequest 래핑하기</a>
<a href="https://salix97.tistory.com/179">2. XMLHttpRequest 로 return 값 받기 위해 promise 사용하기</a>
<a href="https://ccoenraets.github.io/es6-tutorial-data/promisify/">3. XMLHttpRequest의 약속</a>
<a href="https://despiteallthat.tistory.com/149">4. XMLHttpRequest란?</a>
<a href="https://springfall.cc/article/2022-11/easy-promise-async-await">5. 비동기, Promise, await, async 확실하게 이해하기</a>
<a href="https://lightcode.tistory.com/37">6.XHR(XMLHttpRequest)에 대해서 알아보도록 하겠습니다.</a>
<a href="https://inpa.tistory.com/entry/HTTP-%F0%9F%8C%90-%EB%B0%B1%EC%97%94%EB%93%9C-%EB%A1%9C%EB%93%9C%EB%A7%B5-HTTP%EB%8A%94-%EB%AC%B4%EC%97%87%EC%9D%BC%EA%B9%8C%EC%9A%94">7. HTTP는 무엇일까요? - 기본 핵심 요약 총정리</a>
<a href="https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest_API/Using_XMLHttpRequest">8. MDN Using XMLHttpRequest</a></p>