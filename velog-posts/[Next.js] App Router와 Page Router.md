<p>이해가 쏙쏙되게 설명해주신 좋은글이 있어서 읽고 다시 정리해본다.</p>
<h2 id="nextjs란">Next.js란?</h2>
<ul>
<li>프리렌더링을 위한 프레임워크
SSR의 장점은 SEO(Search Engine Optimization: 검색 엔진 최적화)이다.</li>
</ul>
<h2 id="page-router의-라우팅-방식">Page Router의 라우팅 방식</h2>
<p>파일 시스템 기반의 라우팅을 제공한다. 
즉, pages 폴더 안에 있는 파일들이 자동으로 라우트로 변환된다. 
예를 들어, pages/about.js 파일은 /about 경로로 접근할 수 있게 된다.
이 방법은 꽤 직관적이지만 관리와 유지보수에서 큰 단점이 존재한다.</p>
<h2 id="page-router의-렌더링-방식">Page Router의 렌더링 방식</h2>
<p>Page Router는 렌더링 방식과 밀접한 관계가 있다.
Page Router 로 이루어져 있는 페이지는 반드시 동적 렌더링이거나, 정적 렌더링 중 하나를 선택하여 렌더링해야 한다.</p>
<h2 id="app-router">App Router</h2>
<p>App Router도 파일 기반 라우팅이긴 하지만 기존 Page Router방식의 단점을 보완했다.
기존 Page Router 에선 모든 파일이 route 될 수가 있기 때문에  실제 route 경로와 component 요소 간의 구분이 어려워 pages 외부에 디렉토리로 구분하는 방식의 directory structure 를 가져가야 했던 점이 있었지만, </p>
<p>*<em>App Router 에선 app/ 디렉토리내에 어떤 폴더 구조를 가졌더라도 page.ts 라는 예약된 파일만 route가 생성된다. *</em></p>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/937c48b7-0433-4c0e-8fa1-ebcf5d68b5c6/image.png" /></p>
<p>또 기존 최상위 애플리케이션 레벨에서만 공통 레이아웃이나 메타데이터 등을 설정할 수 있었지만, <strong>앱 라우팅은 경로 별 중첩 라우팅을 통해 복잡한 레이아웃을 구현할 수 있게된다.</strong></p>
<h2 id="app-router의-렌더링-방식">App Router의 렌더링 방식</h2>
<p>기존의 Page Router와는 달리 <strong>컴포넌트 중심의 라우팅</strong>을 제공한다. 위 글을 써주신 분은 page router와는 개념부터 완전히 다르기 때문에 next.js를 다시 배운다는 마음 가짐으로 접근해야 쉽다고 한다.
다행히(?) 나는 next를 아예 처음 접했다.</p>
<p>App Router의 주요 키워드는</p>
<ul>
<li>서버 중심</li>
<li>유연</li>
<li>성능</li>
<li>서버 컴포넌트</li>
<li>레이아웃</li>
<li>복잡</li>
</ul>
<h3 id="서버-컴포넌트server-component란">서버 컴포넌트(Server Component)란?</h3>
<p>서버 컴포넌트의 주요 키워드는 </p>
<ul>
<li>성능 </li>
<li>보안</li>
<li>상태 관리</li>
<li>데이타의 가공</li>
<li>SEO(Search Engine Optimization)</li>
</ul>
<p>서버 컴포넌트는 말그대로 서버에서 렌더링되는 React 컴포넌트를 의미하며, 클라이언트로 전송되기전에 서버에서 DOM Element(JSON)들이 string상태로 클라이언트에 도착하고, 클라이언트는 바로 HTML로 변환하여 렌더링된다.</p>
<p>이를 통해서 ** 초기 로딩 시간을 단축하고, 클라이언트에서 복잡한 상태관리를 줄일 수 있다. **</p>
<br />


<br />


<p>*<em>참고/인용한 글 *</em>
<a href="https://blog.kmong.com/next-js-app-router-%EC%9D%B4%EC%A0%9C%EB%8A%94-%EC%95%B1%EB%9D%BC%EC%A0%81-%EC%82%AC%EA%B3%A0%EA%B0%80-%ED%95%84%EC%9A%94%ED%95%98%EB%8B%A4-deep-dive-%EC%8B%9C%EC%9E%91%EB%B6%80%ED%84%B0-%ED%8C%8C%ED%97%A4%EC%B9%98%EA%B8%B0-part-1-6399cea5f11d">Next.js App Router로 프론트엔드 개발 혁신하기 Part.1</a>
<a href="https://blog.kmong.com/react-server-component%EB%A1%9C-%ED%94%84%EB%A1%A0%ED%8A%B8%EC%97%94%EB%93%9C-%EA%B0%9C%EB%B0%9C-%ED%98%81%EC%8B%A0%ED%95%98%EA%B8%B0-part-2-5cf0bf4416b0">React 서버 컴포넌트 작동원리를 아주 쉽게 알아보자</a>
<a href="https://nextjs.org/docs/app/getting-started/project-structure">[공식 문서] Project structure and organization</a>
<a href="https://yozm.wishket.com/magazine/detail/2271/">새로 등장한 '리액트 서버 컴포넌트'이해하기</a></p>