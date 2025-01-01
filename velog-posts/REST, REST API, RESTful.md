<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/cf2e9ae2-f9bb-4c28-a9d6-2f5a0629f001/image.png" /></p>
<p>채용 공고를 보다가 '<strong>RESTful API설계 및 개발 경험을 보유한 분</strong>' 이라는 자격요건/우대사항을 굉장히 많이 볼 수 있었다. 다시 확실히 정리하고 이해하자.</p>
<br />

<p><strong>API(Application Programming Interface)란?</strong></p>
<ul>
<li><p>웹 API는 클라이언트와 웹 리소스 사이의 네트워크 통신을 하기 위한 게이트웨이</p>
</li>
<li><p><em>REST(Representational State Transfer)*</em>
<img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/c8fb35ac-4659-48b7-bf84-fbe6d3620c48/image.png" /></p>
</li>
</ul>
<ul>
<li>자원을 이름으로 구분하여 해당 자원의 상태를 주고받는 모든 것을 의미한다.
자원은 문서, 사진, 그림, 데이터 등 소프트웨어가 관리하는 모든 것을 HTTP URI(Uniform Resource Identifier)를 통해 명시한다.
Ex) DB의 영화 정보가 자원일 때, /movies를 자원의 표현으로 정한다.</li>
</ul>
<p><br /><br /></p>
<h3 id="rest의-특징">REST의 특징</h3>
<blockquote>
</blockquote>
<p><strong>1. Server-Client 구조</strong></p>
<ul>
<li>자원이 있는 쪽이 Server, 자원을 요청하는 쪽이 Client가 된다.<ul>
<li>REST Server : API를 제공하고 비즈니스 로직 처리 및 저장을 책임진다.</li>
<li>Client : 사용자 인증이나 context(세션, 로그인 정보) 등을 직접 관리하고 책임진다.</li>
</ul>
</li>
<li>서로 간 의존성이 줄어든다.<blockquote>
</blockquote>
<strong>2. Stateless (무상태)</strong></li>
<li>HTTP 프로토콜은 Stateless Protocol이므로 REST 역시 무상태성을 갖는다.</li>
<li>Client의 context를 Server에 저장하지 않는다.<ul>
<li>즉, 세션과 쿠키와 같은 context 정보를 신경쓰지 않아도 되므로 구현이 단순해진다.</li>
</ul>
</li>
<li>서버는 각각의 요청을 완전히 별개의 것으로 인식하고 처리한다.<ul>
<li>각 API 서버는 Client의 요청만을 단순 처리한다.<blockquote>
</blockquote>
</li>
</ul>
<ol start="3">
<li>** Cacheable (캐시 처리 가능) **</li>
</ol>
<ul>
<li>대량의 요청을 효율적으로 처리하기 위해 캐시가 요구된다.</li>
<li>캐시 사용을 통해 응답시간이 빨라지고 REST Server 트랜잭션이 발생하지 않기 때문에 전체 응답시간, 성능, 서버의 자원 이용률을 향상시킬 수 있다.</li>
<li>웹 표준 HTTP 프로토콜을 그대로 사용하므로 웹에서 사용하는 기존의 인프라를 그대로 활용할 수 있다.<ul>
<li>즉, HTTP가 가진 가장 강력한 특징 중 하나인 캐싱 기능을 적용할 수 있다.<blockquote>
</blockquote>
</li>
</ul>
</li>
<li><ul>
<li><ol start="4">
<li>Layered System(계층화) **</li>
</ol>
</li>
</ul>
</li>
<li>Client는 REST API Server만 호출한다.</li>
<li>REST Server는 다중 계층으로 구성될 수 있다.<ul>
<li>API Server는 순수 비즈니스 로직을 수행하고 그 앞단에 보안, 로드밸런싱, 암호화, 사용자 인증 등을 추가하여 구조상의 유연성을 줄 수 있다.<blockquote>
</blockquote>
</li>
</ul>
</li>
<li><ul>
<li><ol start="5">
<li>Code-On-Demand(optional) **</li>
</ol>
</li>
</ul>
</li>
<li>Server로부터 스크립트를 받아서 Client에서 실행한다.</li>
<li>반드시 충족할 필요는 없다.<blockquote>
</blockquote>
</li>
<li><ul>
<li><ol start="6">
<li>Uniform Interface(인터페이스 일관성) **</li>
</ol>
</li>
</ul>
</li>
<li>URI로 지정한 Resource에 대한 조작을 통일되고 한정적인 인터페이스로 수행한다. </li>
<li>HTTP 표준 프로토콜에 따르는 모든 플랫폼에서 사용이 가능하다.<ul>
<li>특정 언어나 기술에 종속되지 않는다.</li>
</ul>
</li>
</ul>
</li>
</ul>
<p>무상태성(Stateless)은 서버에서 클라이언트의 상태를 저장하지 않는 것을 말한다.</p>
<p><br /><br /></p>
<p><strong>REST API</strong> 
<img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/865f74a7-0ba9-4689-9ce7-b68c158e09c2/image.png" /></p>
<ul>
<li>클라이언트와 서버 간의 두 컴퓨터 시스템이 인터넷을 통해 정보를 안전하게 교환하기 위해 사용하는 인터페이스</li>
</ul>
<p><br /><br /></p>
<h3 id="crud-operation"><strong>CRUD Operation</strong></h3>
<blockquote>
<p>Create : 데이터 생성(POST)
Read : 데이터 조회(GET)
Update : 데이터 수정(PUT, PATCH)
Delete : 데이터 삭제(DELETE)</p>
</blockquote>
<p>💡 Patch 는 데이터를 갱신하는 메서드인데, 
&amp;nbsp&amp;nbsp&amp;nbsp&amp;nbsp&amp;nbsp&amp;nbsp전체 데이터를 수정하는게 PUT이라면 PATCH는 특정 하나의 내용을 수정할 때 사용된다.</p>
<br />
<br />


<h2 id="-rest-api-설계-규칙-">** REST API 설계 규칙 **</h2>
<blockquote>
</blockquote>
<p><strong>1) 동사 표현이 들어가면 안된다.</strong>
&amp;nbsp&amp;nbsp&amp;nbsp&amp;nbsp(즉, CRUD 기능을 나타내는 것은 URI에 사용하지 않는다.)
  &amp;nbsp&amp;nbsp&amp;nbsp&amp;nbspEx)<code>GET /members/show/1</code> -&gt; <code>GET /members/1</code>
  &amp;nbsp&amp;nbsp&amp;nbsp&amp;nbspEx) <code>GET /members/insert/2</code> -&gt; <code>POST /members/2</code>
<strong>2) 소문자를 사용하고, 명사는 복수 명사를 사용해야 한다.</strong>
 &amp;nbsp&amp;nbsp&amp;nbsp&amp;nbspEx) <code>GET /Member/1</code> -&gt; <code>GET /members/1</code>
<strong>3) URI의 마지막엔 슬래시(/) 를 포함하지 않는다.</strong>
    -&gt; REST API는 분명한 URI를 만들어 통신을 해야 하기 때문에 혼동을 주지 않도록 URI 경로의 마지막에는 슬래시(/)를 포함하지 않아야 한다.
<strong>4) URI에는 언더바를 사용하지 않고 하이픈을 사용한다.</strong>
<strong>5) 파일의 확장자를 표시하지 않는다.
6) 경로 부분 중 변하는 부분은 유일한 값으로 대체한다.</strong>
&amp;nbsp&amp;nbsp&amp;nbsp&amp;nbsp(즉, :id는 하나의 특정 resource를 나타내는 고유 값이다.)
&amp;nbsp&amp;nbsp&amp;nbsp&amp;nbsp EX) student를 생성하는 <code>route: POST/students</code>
&amp;nbsp&amp;nbsp&amp;nbsp&amp;nbsp EX) id=11인 student를 삭제하는 <code>route: DELETE/students/11</code></p>
<p><br /><br /></p>
<h2 id="restful"><strong>RESTful</strong></h2>
<p>REST의 원리를 따르는 시스템은 RESTful이란 용어로 지칭한다.
=&gt; 'REST API'를 제공하는 웹 서비스를 'RESTful'하다고 할 수 있다.
<br />
URI 규칙을 올바르게 지키지 않은 API는 REST API의 설계 규칙을 올바르게 지키지 못한 시스템으로 REST API를 사용하였지만 RESTful하지 못한 시스템이라고 할 수 있다.
<br /><br /></p>
<h2 id="-path-parameterquery-parameter-">** Path Parameter/Query Parameter **</h2>
<p>RESTful API는 Path Parameter 또는 Query Parameter로 통신할 수 있다.
<br /></p>
<h3 id="-path-parameter-">** Path Parameter **</h3>
<p>전체 데이터 또는 특정 하나의 데이터를 다룰 때 사용한다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/4f1ac8be-de13-412c-b969-10214a219b97/image.png" />
** response 200은 성공적으로 처리했을 때 쓰인다. 
&amp;nbsp&amp;nbsp&amp;nbsp&amp;nbsp가장 일반적으로 볼 수 있는 HTTP상태이다.</p>
<p>Product를 받아오는 GET 요청이다.
특정한 하나의 데이터 또는 정제되지 않은 데이터가 필요한 경우에 사용될 수 있다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/5dccafa5-d2a4-42fd-af60-2891952e9107/image.png" />
클라이언트가 원하는 요청에 대한 데이터를 Request body로 보내면 서버는 이를 받아 처리한다.</p>
<h3 id="-query-parameter-">** Query Parameter **</h3>
<p>filtering, ordering, searching에 많이 사용한다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/f091e068-7339-4359-92b7-61583580671d/image.png" />
특정 조건에 맞는(Filtering) 데이터를 받아오는 GET 요청이다.
이와 같이 조건에 맞게 데이터를 정제하여 불러올 때 사용할 수 있다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/529c1a77-a9ed-48e0-85bf-9ab1340d4999/image.png" />
역순으로 데이터를 ordering 하여 보내줄 것을 요청하는 GET메서드이다.
서버는 Query String을 받아 클라이언트가 원하는 방식으로 데이터를 보여주고있다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/299d2f17-ba19-4fdb-a1e0-a0c090621664/image.png" />
원하는 만큼 데이터를 불러오는 Pagination이다.
<br />
이렇게 Query String은 원하는 조건을 주어 데이터를 정제하여 가져오는 경우에 사용할 수 있다.</p>
<br />
<br />

<p>** 참고한 글/출처**
<a href="https://gmlwjd9405.github.io/2018/09/21/rest-and-restful.html">[Network] REST란? REST API란? RESTful이란?</a>
<a href="https://velog.io/@newdana01/TIL-RESTful-API">[TIL] RESTful API 개념, Path Parameter, Query Parameter</a></p>