<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/05896cee-5c38-4481-bd23-3c1ce4df841c/image.png" /></p>
<p>바닐라JS를 공부하면서 작은 프로젝트를 하나 개발해보려고 한다.
역시 가장 무난한건 TODO List일 것이다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/b211ca7a-69fe-4210-9827-af9c82c24a49/image.png" />
이런 느낌으로 간단하게 구현해보려고 한다. 
개발 환경은 <code>Visual Studio Code</code>를 사용했고, <code>HTML</code>, <code>CSS</code>, <code>JavaScript</code>로 개발할 예정이다.
<br /></p>
<h2 id="💡-기능-구현-목록">💡 기능 구현 목록</h2>
<blockquote>
<ul>
<li><a href="https://openweathermap.org/api">OpenWeather</a>에서 날씨 API를 받아와서 날씨를 상단에 띄우기</li>
</ul>
</blockquote>
<ul>
<li>현재 시간 띄우기</li>
<li>인사말 문구를 랜덤으로 띄우고 사용자의 이름을 <code>localStorage</code>에 저장해 띄우기</li>
<li>할 일 입력 폼에 할일을 입력하면 자동으로 할일이 등록</li>
<li>할 일 삭제 버튼을 누르면 할 일이 삭제 된다.</li>
</ul>
<hr />

<h2 id="구현-화면">구현 화면</h2>
<p>** <a href="https://github.com/yeonhee314/vanila-js-todolist.git">코드 GitHub 주소</a> ** 
<img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/12f3bcc5-9a6d-4800-b36b-1f493350d1ee/image.gif" /></p>
<h3 id="indexhtml">index.html</h3>
<pre><code class="language-html">&lt;!DOCTYPE html&gt;
&lt;html lang=&quot;ko&quot;&gt;
&lt;head&gt;
    &lt;meta charset=&quot;UTF-8&quot;&gt;
    &lt;meta name=&quot;viewport&quot; content=&quot;width=device-width, initial-scale=1.0&quot;&gt;
    &lt;link rel=&quot;stylesheet&quot; href=&quot;../css/style.css&quot;&gt;
    &lt;title&gt;TODO List&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
    &lt;div id=&quot;container&quot;&gt;
        &lt;!-- Contents --&gt;
        &lt;div id=&quot;contents&quot; class=&quot;hidden&quot;&gt;
            &lt;p id=&quot;weather&quot; class=&quot;small-text&quot;&gt;날씨&lt;/p&gt;
            &lt;h1 id=&quot;clock&quot;&gt;00:00:00&lt;/h1&gt;
            &lt;p id=&quot;greeting&quot;&gt;&lt;/p&gt;
            &lt;form onsubmit=&quot;onTodoSubmit()&quot;&gt;
                &lt;input type=&quot;text&quot; id=&quot;input-task&quot; placeholder=&quot;Enter tasks...&quot; pattern=&quot;[A-Za-z\s]+$&quot; autocomplete=&quot;off&quot; autofocus&gt;
            &lt;/form&gt;
            &lt;ul id=&quot;task-list&quot;&gt;&lt;/ul&gt;
        &lt;/div&gt;
        &lt;!-- Login --&gt;
        &lt;div id=&quot;login_form&quot;&gt;
            &lt;h1&gt;Welcome TODO App&lt;/h1&gt;
            &lt;form onsubmit=&quot;onLoginSubmit(event)&quot;&gt;
                &lt;input type=&quot;text&quot; id=&quot;username&quot; placeholder=&quot;Enter your nickname.&quot; pattern=&quot;[A-Za-z\s]+$&quot; autocomplete=&quot;off&quot; autofocus&gt;
            &lt;/form&gt;
        &lt;/div&gt;
    &lt;/div&gt;
    &lt;script src=&quot;../scripts/util.js&quot; type=&quot;module&quot;&gt;&lt;/script&gt;
    &lt;script src=&quot;../scripts/app.js&quot;&gt;&lt;/script&gt;
    &lt;script src=&quot;../scripts/weather.js&quot; type=&quot;module&quot;&gt;&lt;/script&gt;
&lt;/body&gt;
&lt;/html&gt;</code></pre>
<p>클래스를 지정해서 숨기고 싶은 컨텐츠에 <code>hidden</code> 클래스를 지정했다.
<code>css</code>에서 <code>hidden</code>클래스의 경우 <code>display: none</code>으로 설정해 해당 컨텐츠를 숨겼다.</p>
<br />

<h4 id="📑-사용자-이름-할-일-입력">📑 사용자 이름, 할 일 입력</h4>
<p>첫 화면에서 사용자 이름을 <strong>영어와 공백만</strong> 입력 가능하도록 <code>input</code>에 정규 표현식을 사용했다.
영어와 공백만 입력이 가능하도록 정규표현식을 사용했다. (<code>[A-Za-z\s]+$</code>)</p>
<blockquote>
<ul>
<li><code>[A-Za-z]</code> : 대소문자 알파벳을 의미한다.</li>
</ul>
</blockquote>
<ul>
<li><code>\s</code> : 공백 문자(스페이스, 탭, 줄바꿈 등)을 의미한다.</li>
<li><code>+</code> : 앞의 문자 클래스 <code>[A-Za-z\s]</code>가 하나 이상 나올 수 있다는 것을 의미한다.</li>
<li><code>$</code> : 문자열의 끝을 의미한다.</li>
</ul>
<br />


<h4 id="📑-api-키-관리-방법">📑 API 키 관리 방법</h4>
<p>날씨는 현재 사용자의 위치 정보를 받아와서 <strong>OpenWeather API</strong>에서 API키를 가져올 수 있도록 구현했다. 
코드는 <code>GitHub</code>에 업로드하기 때문에 보안상 따로 관리가 필요하다고 생각했다.
<code>GitHub</code>에 커밋하지 않을 스크립트를 따로 모듈화해서 관리하기 위해 <code>util.js</code>를 생성했다. 
<code>util.js</code>에서 <code>export</code>해서 <code>weather.js</code>에 <code>import</code>해서 키를 가져다 쓰는 방식이다.</p>
<br />


<h3 id="stylecss">style.css</h3>
<pre><code class="language-css">@charset &quot;utf-8&quot;;
@import url('https://fonts.googleapis.com/css2?family=Jersey+15&amp;family=Josefin+Sans:ital,wght@0,100..700;1,100..700&amp;display=swap');

*{
    font-family: Josefin Sans;
}
#container{
    width: 600px;
    margin: auto;
}
#contents{
    text-align: center;
}
#clock{
    font-size: 70px;
    color: orange;
}
.small-text{
    font-size: small;
    color: silver;
    margin-top: 30px;
}
.hidden{
    display: none;
}
/* contents : 랜덤 인사 문구 */
#greeting{
    font-weight: bold;
    font-size: 30px;
    margin-top: -25px;
    color: rgb(88, 58, 0);
}
/* 로그인 시 이름 입력 폼 */
#login_form{
    text-align: center;
}

#username{
    border: 2px solid gray;
    width: 100%;
    height: 100px;
    font-size: 30px;
    text-align: center;
}
/* 할 일 입력폼 */
input:focus{
    outline: none;
}
#input-task{
    border: 2px dashed rgba(128, 128, 128, 0.26);
    padding: 15px;
    text-align: center;
    font-size: 20px;
    width: 100%;
}
#task-list &gt; li{
    padding: 20px;
    text-align: left;
    font-size: 20px;
    display: flex;
    justify-content : space-between;
    height: 30px;
}
.delBtn{
    all: unset;
    transition: all 0.3s;
    transform-origin: center;
}
.delBtn:hover{
    transform: scale(1.2);
}</code></pre>
<br />


<h3 id="appjs">app.js</h3>
<pre><code class="language-javascript">let contents = document.querySelector(&quot;#contents&quot;);
let login_form = document.querySelector(&quot;#login_form&quot;);
let greeting = document.querySelector(&quot;#greeting&quot;);
const clock = document.querySelector('#clock');
let task_array = [];

const HIDDEN_CLASSNAME = &quot;hidden&quot;;
const USER_NAME = &quot;userName&quot;
const TASKS = &quot;tasks&quot;;

const greeting_arr = [
    &quot;Hello&quot;,
    &quot;Good day&quot;,
    &quot;Hey there&quot;,
    &quot;How are things&quot;,
    &quot;What's happening&quot;,
    &quot;Yo&quot;,
    &quot;What's the story&quot;
];

// 프로그램이 시작되자마자 유효성 검사를 실시 한다.
// 유저 네임이 있는 경우
if(localStorage.getItem(USER_NAME)){
    setClock();
    setUserName(localStorage.getItem(USER_NAME));
    const savedTasks = localStorage.getItem(TASKS);   // 저장되어있는 할 일 목록
    // console.log(`savedTasks : ${savedTasks}`);
    if(savedTasks){
        task_array = JSON.parse(savedTasks);    // JSON.parse() : JSON을 객체로 변경한다. 
        displayTasks(task_array);
    } 
}

// 현재 시간
function setClock(){
    const date = new Date();
    const hour = String(date.getHours()).padStart(2, '0');
    const minute = String(date.getMinutes()).padStart(2, '0');
    const seconds = String(date.getSeconds()).padStart(2, '0');
    clock.innerText = `${hour}:${minute}:${seconds}`;    
}
setInterval(setClock, 1000);


// 로그인 Submit
function onLoginSubmit(event){
    let userName = document.querySelector(&quot;#username&quot;).value;
    localStorage.setItem(USER_NAME, userName);
    event.preventDefault();
    setUserName(userName);
}

// 'userName'이 있는 경우 로그인 화면이 아닌 컨텐츠 화면을 바로 보여준다.
function setUserName(userName){
    login_form.classList.add(HIDDEN_CLASSNAME);
    contents.classList.remove(HIDDEN_CLASSNAME);
    greeting.innerHTML = `${randomGreeting()} ${userName}!`;
}

// 페이지가 로드될 때마다 출력되는 랜덤 인삿말
function randomGreeting(){
    let randomIndex = Math.floor(Math.random() * greeting_arr.length);
    return greeting_arr[randomIndex];
}

// Todo 입력 Submit
function onTodoSubmit(){
    let task = document.querySelector('#input-task').value;
    task_array.push(task);
    localStorage.setItem(TASKS, JSON.stringify(task_array));
    displayTasks(task_array);
}

// 할 일 목록을 화면에 출력한다.
function displayTasks(task_array){
    let taskList = document.querySelector('#task-list');
    taskList.innerHTML = '';    // 기존 목록 비우기
    for(let i = 0; i &lt; task_array.length; i++){
        let li = document.createElement('li');
        let delBtn = document.createElement('button');
        li.setAttribute('data-index', i);
        delBtn.innerHTML = '❌';
        delBtn.setAttribute('class', 'delBtn');
        delBtn.setAttribute('type', 'button');
        li.innerHTML = `&lt;span&gt;${task_array[i]}&lt;/span&gt;`;
        li.appendChild(delBtn);
        taskList.append(li);

        // 삭제버튼 눌렀을 때
        delBtn.addEventListener('click', function(){
            // console.log(`클릭한 항목의 인덱스 : ${li.getAttribute('data-index')}`);
            let index = li.getAttribute('data-index');
            let tasks = JSON.parse(localStorage.getItem(TASKS));
            tasks.splice(index, 1);
            localStorage.setItem(TASKS, JSON.stringify(tasks));
            taskList.removeChild(li);
        });
    }
}</code></pre>
<h4 id="📑-사용자-이름-저장">📑 사용자 이름 저장</h4>
<p>사용자의 이름을 입력하는 경우 <code>localStorage</code>에 <code>userName</code>으로 저장한다.
저장 하면 페이지를 껐다가 켜도 <code>localStorage</code>의 <code>userName</code>을 삭제하지 않는 한 사용자의 정보가 저장된다. 
화면을 켰을 때 <code>userName</code>이 있는지 검사하고, 만약 있다면 현재 시간 정보를 출력한다.
로그인 화면은 <code>hidden</code>클래스를 추가하여 숨기고, 컨텐츠 화면은 <code>hidden</code>클래스를 삭제하여 화면에 띄운다.</p>
<br />

<h4 id="📑-할-일-목록-추가">📑 할 일 목록 추가</h4>
<p>할 일을 입력하면 해당 <code>value</code>를 <code>task_array</code> 배열에 저장한다.
<code>JSON.stringify(task_array)</code>는 <strong>배열을 문자열로 변환하는 메서드</strong>이다.
<code>localStorage</code>는 문자열만 저장할 수 있기 때문에 배열을 저장하기 위해 <code>JSON.stringify()</code>를 사용해서 문자열로 변환했다.</p>
<p><code>for</code>문을 사용해서 <code>task_array</code>에 저장된 할 일 목록을 순회하며 할 일 갯수 만큼 리스트 항목 요소와 삭제 버튼을 생성한다.</p>
<p>리스트 항목 요소에는 <code>data-index</code>라는 <strong>커스텀 속성</strong>을 추가해서 삭제할 때 어떤 항목을 삭제할 지 알아내기 위해서 해당 항목의 인덱스를 저장한다.</p>
<br />

<h4 id="📑-할-일-목록-삭제">📑 할 일 목록 삭제</h4>
<p><code>splice()</code>는 배열에서 요소를 제거하는 메소드로 <code>task.splice(index, 1)</code>를 사용해서 해당 인덱스의 항목을 배열에서 삭제한다.</p>
<p><code>localStorage.setItem(TASKS, JSON.stringify(tasks));</code> 는 수정된 할 일 목록을 다시 로컬 저장소에 저장한다. 삭제된 항목을 제외한 새로운 목록을 문자열로 반환하여 저장한다.</p>
<br />

<h3 id="weatherjs">weather.js</h3>
<pre><code class="language-javascript">import { WEATHER_API_KEY } from './util.js';

function onGeoSuccess(position){
    let latitude = position.coords.latitude;    // 위도
    let longitude = position.coords.longitude;  // 경도
    const url = `https://api.openweathermap.org/data/2.5/weather?lat=${latitude}&amp;lon=${longitude}&amp;appid=${WEATHER_API_KEY}&amp;units=metric`;
    fetch(url).then(response =&gt; response.json()).then(data =&gt; {
        // console.log(data.name, data.weather[0].main);
        const weather_container = document.querySelector('#weather');
        const name = data.name;
        const weather = data.weather[0].main;
        weather_container.innerHTML = `${name} is ${weather} !`;
    }); 

}
// 사용자의 현재 위치를 요청한다.
navigator.geolocation.getCurrentPosition(onGeoSuccess);</code></pre>
<p><code>navigator.geolocation.getCurrentPosition()</code> 함수를 이용해서 현재 사용자의 위치 정보를 받아온다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/09f4189f-8e7d-44f2-99b2-3dd53ef8c24f/image.png" />
페이지를 실행하면 권한 요청 알람이 뜨는데 허용하는 경우에 <code>onGeoSuccess()</code>함수가 실행된다.
API요청을 위한 <code>url</code>을 생성하고, <code>fetch()</code>함수를 이용해서 위에서 생성한 <code>url</code>에 HTTP 요청을 보내고 반환되는 응답을 비동기 처리한다.</p>
<br />

<h3 id="utiljs">util.js</h3>
<pre><code class="language-javascript">export const WEATHER_API_KEY = &quot;apiKey&quot;;</code></pre>
<p>따로 발급받은 키를 관리하기 위한 <code>util</code> 스크립트를 만들어서 키를 관리한다.</p>
<hr />
<br />

<h3 id="마치며">마치며..</h3>
<p>늘 이론 공부보다 실습하는 것이 더 중요하다고 느낀다. 다 알고 있었던 것들이지만 직접 구현해보니 애로 사항이 은근히 많았다. 바닐라 자바스크립트가 모든 프레임워크, 라이브러리의 근간이 되니 간단한 프로젝트라도 배운 것이 많아서 재미있었다!! </p>