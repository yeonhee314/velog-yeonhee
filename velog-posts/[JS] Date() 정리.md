<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/9bdbb7f5-87a3-405f-99dc-da538a735f2f/image.png" /></p>
<p>자바스크립트에서 <code>Date</code> 객체를 사용해서 시간과 날짜 정보를 얻어올 수 있다.
<code>Date</code>객체는 1970년 1월 1일 UTC(협정 세계시) 자정과의 시간 차이를 밀리초로 나타내는 정수 값을 담는다.</p>
<blockquote>
<p>자바스크립트에서 월(month)을 나타낼 때는 <strong>1월이 0으로 표현되고, 12월이 11로</strong> 표현된다.</p>
</blockquote>
<p><code>Date</code>객체는 생성자 함수인데, 이는 날짜와 시간을 가지는 인스턴스를 생성한다.</p>
<p>생성된 인스턴스는 <strong>현재 날짜와 시간을 나타내는 값</strong>을 가진다.</p>
<p>만약 현재 날짜와 시간이 아닌 다른 날짜와 시간을 가지고 싶은 경우 <code>Date</code>생성자 함수에 날짜와 시간 정보를 인수로 지정해야한다.</p>
<hr />

<h2 id="1-date-객체-생성">1. Date 객체 생성</h2>
<h3 id="1-1-현재-날짜와-시간-가져오기">1-1. 현재 날짜와 시간 가져오기</h3>
<pre><code class="language-javascript">const now = new Date();
console.log(now);</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/8c11c089-2da1-4ab8-8981-777c4cb87e05/image.png" />
인수를 전달하지 않고 사용하는 경우 <strong>현재 날짜와 시간</strong>을 가지는 인스턴스를 반환한다.
<br /></p>
<h3 id="1-2-날짜와-시간-구성">1-2. 날짜와 시간 구성</h3>
<pre><code class="language-javascript">let customDate = new Date(2025, 0, 16, 16, 30, 0);
console.log(customDate);</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/b0d7dcf3-5685-40cc-8f81-d01b1100a430/image.png" /></p>
<br />

<h3 id="1-3-특정-날짜와-시간-생성">1-3. 특정 날짜와 시간 생성</h3>
<pre><code class="language-javascript">let specificDate = new Date('2025-01-17');
console.log(specificDate);</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/0acc41b8-a2aa-454f-815d-bd2b5fe27627/image.png" /></p>
<br />

<h3 id="1-4-타임스탬프ms로-생성">1-4. 타임스탬프(ms)로 생성</h3>
<pre><code class="language-javascript">let timestampDate = new Date(1609459200000);
console.log(timestampDate);</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/bd7e66cc-62c6-44e6-9127-389bd84067dc/image.png" /></p>
<p>인수로 숫자타입의 밀리초를 전달하면 1970년 1월 1일 00:00(UTC)을 기점으로 <strong>인수로 전달된 밀리초만큼 경과한 날짜와 시간</strong>을 가지는 인스턴스를 반환한다.</p>
<blockquote>
<ul>
<li>86400000ms 는 하루를 의미한다.</li>
</ul>
</blockquote>
<ul>
<li>1s = 1,000ms</li>
<li>1m = 60s * 1,000ms = 60,000ms</li>
<li>1h = 60m * 60,000ms = 3,600,000ms</li>
<li>1d = 24h * 3,600,000ms = 86,400,000ms</li>
</ul>
<br />

<h3 id="1-4-문자열로-날짜-생성">1-4. 문자열로 날짜 생성</h3>
<pre><code class="language-javascript">const dateFromString = new Date('2025-01-16T15:30:00');
console.log(dateFromString);</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/551dc345-14c8-4412-a166-5ab3cdf38e06/image.png" /></p>
<p>ISO 8601은 날짜와 시간을 표현하는 국제 표준으로 ISO 8601 형식을 사용한다.</p>
<br />

<h2 id="2-date-메소드">2. Date 메소드</h2>
<h3 id="2-1-getfullyear">2-1. getFullYear()</h3>
<pre><code class="language-javascript">let date = new Date();
console.log(date.getFullYear());</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/1fdca9e7-b28e-4185-a4d9-04cffca38bc6/image.png" /></p>
<p><code>getFullYear()</code>는 4자리 연도를 반환한다.
인자를 따로 전달해주지 않았기 때문에 현재 연도를 반환한다.
<br /></p>
<h3 id="2-2-getmonth">2-2. getMonth()</h3>
<pre><code class="language-javascript">let date = new Date();
console.log(date.getMonth());</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/7d6c2454-ca3e-492e-90f1-32c72cdd7047/image.png" />
<strong>0~11</strong>까지의 월을 반환한다.
현재는 25년 1월이기 때문에 0이 반환되었다.</p>
<br />

<h3 id="2-3-getdate">2-3. getDate()</h3>
<pre><code class="language-javascript">let date = new Date();
console.log(date.getDate());</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/34c630e2-c16f-4fd9-b5ad-1c4fa9a002c7/image.png" />
1~31까지의 날짜(일)을 반환한다.</p>
<br />

<h3 id="2-4-getday">2-4. getDay()</h3>
<pre><code class="language-javascript">let date = new Date();
console.log(date.getDay());</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/5008fb07-0fc8-4028-a786-66da5c747f05/image.png" />
0부터 6까지 요일을 반환한다.
현재 글을 쓰는 시점은 목요일이므로 4를 반환했다.</p>
<blockquote>
<p><strong>0</strong> : 일요일
<strong>1</strong> : 월요일
<strong>2</strong> : 화요일
<strong>3</strong> : 수요일 
<strong>4</strong> : 목요일
<strong>5</strong> : 금요일
<strong>6</strong> : 토요일</p>
</blockquote>
<br />

<h3 id="2-5-gethours">2-5. getHours()</h3>
<pre><code class="language-javascript">let date = new Date();
console.log(date.getHours());</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/1a5d2345-798b-484f-a02e-4dae11c4fc54/image.png" /></p>
<p><strong>0 부터 23까지</strong>의 시간을 반환한다.</p>
<br />

<h3 id="2-6-getminutes">2-6. getMinutes()</h3>
<pre><code class="language-javascript">let date = new Date();
console.log(date.getMinutes());</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/242f2afb-cfe9-4db9-8688-bda0e1d6f8c2/image.png" />
<strong>0부터 59</strong>까지 분을 반환한다.</p>
<br />

<h3 id="2-7-getseconds">2-7. getSeconds()</h3>
<pre><code class="language-javascript">let date = new Date();
console.log(date.getSeconds()); </code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/42f4f49e-3383-45d5-98eb-78fe6b76ad0f/image.png" />
<strong>0부터 59까지</strong> 초를 반환한다.</p>
<br />

<h3 id="2-8-getmilliseconds">2-8. getMilliseconds()</h3>
<pre><code class="language-javascript">let date = new Date();
console.log(date.getMilliseconds());</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/8d7de7ca-7644-4b43-805c-9cbbfc7a9520/image.png" />
<strong><em>0부터 999까지</em></strong> 밀리초(ms)를 반환한다.</p>
<br />

<h3 id="2-9-gettime">2-9. getTime()</h3>
<pre><code class="language-javascript">let date = new Date();
console.log(date.getTime());</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/7b2874af-276c-463b-a2c6-4aa0df063b7f/image.png" /></p>
<p><strong>1970년 1월 1일부터 현재까지의 밀리초</strong>를 반환한다.</p>
<br />

<h2 id="3-날짜와-시간-설정하기">3. 날짜와 시간 설정하기</h2>
<pre><code class="language-javascript">const date = new Date();
date.setFullYear(2026);
date.setMonth(5); 
date.setDate(20);
console.log(date);
</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/83e23b8f-56ec-4663-baea-351c2ce1ebb7/image.png" />
<code>setFullYear()</code>, <code>setMonth()</code>, <code>setDate()</code> 등을 사용하여 날짜를 변경할 수 있다.</p>
<br />

<h2 id="4-날짜-포맷팅하기">4. 날짜 포맷팅하기</h2>
<pre><code class="language-javascript">let now = new Date();
console.log(now.toLocaleString());
console.log(now.toLocaleDateString());
console.log(now.toLocaleTimeString());
</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/0e479367-5b56-4c05-b656-6e200e32dfc1/image.png" />
<code>toLocaleString()</code>을 사용해서 날짜를 보기 좋게 포맷팅할 수도 있다.</p>
<br />
<hr />

<p><code>Date</code> 객체는 자주 쓰이는데 형식이 가끔 기억이 안나서 정리해두고 싶었다.</p>
<p>그리고 chrome console창에서 코드 복사 붙여넣기가 안되길래 일일히 쳐서 테스트해보다가 이거 방법이 있을텐데.. 하고 찾아보니까 console 창에 <code>allow pasting</code>이라고 입력하니 복사/붙여넣기가 가능해졌다.</p>
<p>그리고 콘솔창에서 <code>Shift + Enter</code>하면 줄바꿈이 된다.
이런 기본적인 것들을 이제서야 알아버렸다.</p>
<p>이제라도 알았으면 됐지! 😂
<br /></p>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/dc1366bb-326a-41d0-b21f-f05199acbfa7/image.png" /></p>
<p><br /><br /></p>
<p><strong>참고한 글</strong>
<a href="https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Date">mdn web docs</a>
<a href="https://inpa.tistory.com/entry/JS-%F0%9F%93%9A-Date-%EB%A9%94%EC%86%8C%EB%93%9C-%EC%A0%95%EB%A6%AC">[JS] 📚 자바스크립트 Date 메소드 💯 총정리</a></p>