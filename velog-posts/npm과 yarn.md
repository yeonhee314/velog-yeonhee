<h2 id="npm과-yarn">npm과 yarn</h2>
<blockquote>
<p>npm과 yarn은 자바스크립트 런타임 환경인 노드(Node.js)의 패키지 관리자이다.</p>
</blockquote>
<p>명령 줄 인터페이스(Command-line interface, CLI)를 통해 패키지 설치 및 삭제뿐 아니라 
패키지 버전 관리, 의존성 관리도 편리하게 할 수 있다.</p>
<h2 id="npm">npm</h2>
<p>npm은 자바스크립트 언어를 위한 패키지 관리자로 Node.js의 기본 패키지 관리자이다.
npm은 Node.js를 설치하기만 하면 명령어 한 줄로 기능의 추가가 가능하다.
기본적으로 npm은 Node.js에 내장되어 있다.</p>
<h2 id="npm-명령어">npm 명령어</h2>
<p>npm을 사용하기 위해서 사용하는 대표적인 명령어</p>
<blockquote>
<p><strong>npm init</strong> : package.json 생성
<strong>npm install</strong> : package.json 파일 및 해당 종속성에 나열된 모든 모듈을 설치
<strong>npm install package_name@버전</strong> : 특정 패키지의 특정 버전 설치
<strong>npm install 주소</strong> : 특정 저장소 내 패키지 설치. 주로 github을 이와 같이 설치
<strong>npm install package_name -g</strong> : 옵션. 글로벌로 설치. 로컬의 다른 프로젝트도 이 패키지를 사용 가능
<strong>npm uninstall</strong> : 패키지 삭제 명령어
<strong>npm update</strong> : 설치한 패키지들을 업데이트
<strong>npm dedupe</strong> : 중복 설치된 패키지들을 정리해주는 명령어</p>
</blockquote>
<h3 id="packagejson이란">package.json이란?</h3>
<p><code>package.json</code>은 프로젝트 정보와 의존성(dependencies)을 관리하는 문서이다.
어떤 패키지(오픈소스)를 사용하는지, 어떤 버전을 사용하는지 등을 기록함으로써 어느 곳에서도 동일한 개발 환경을 구축할 수 있게 해준다.</p>
<hr />

<h2 id="yarn">yarn</h2>
<p>yarn은 2016년 페이스북에서 개발한 패키지 관리자이다.
npm과 같은 기능을 수행하나, npm 레지스트리와 호환하면서 속도나 안정성 측면에서 npm보다 향상되었다.</p>
<h3 id="yarn은-왜-등장">yarn은 왜 등장?</h3>
<h4 id="속도">속도</h4>
<p>yarn은 다운 받은 패키지를 데이터를 캐시(cache)에 저장하여, 중복된 데이터는 다운로드하지않고, 캐시에 저장된 파일을 활용함으로써 이론적으로 npm에 비해 패키지 설치속도가 매우 빠르다.</p>
<h4 id="안정성보안성">안정성/보안성</h4>
<p>npm은 패키지가 설치될 때 자동으로 코드와 의존성을 실행할 수 있도록 허용했다. 이 특징은 편리한 기능이지만 안정성을 위협할 수 있다. 특히나 보장된 정책 없이 등록한 패키지가 존재할 수 있다는 점에서 더욱 위험도가 높다.
반면 yarn은 yarn.lock이나 package.json으로 부터 설치만 하며, yarn.lock은 모든 디바이스에 같은 패키지를 설치하는 것을 보장하기 때문에 버전의 차이로 인해 생기는 버그를 방지해줄 수 있다.</p>
<h2 id="yarn-명령어">yarn 명령어</h2>
<blockquote>
<p><strong>yarn init</strong> : package.json 생성
<strong>yarn or yarn install</strong> : package.json 파일 및 해당 종속성에 나열된 모든 모듈을 설치
<strong>yarn add package_name@버전</strong> : 특정 패키지의 특정 버전 설치
<strong>yarn add 주소</strong> : 특정 저장소 내 패키지 설치. 주로 github을 이와 같이 설치
<strong>yarn global add package_name</strong> : 옵션. 글로벌로 설치. 로컬의 다른 프로젝트도 이 패키지를 사용 가능
<strong>yarn remove</strong> : 패키지 삭제 명령어
<strong>yarn upgrade</strong> : 설치한 패키지들을 업데이트
<strong>npm dedupe</strong> : 중복 설치된 패키지들을 정리해주는 명령어</p>
</blockquote>
<br />

<h4 id="마치며">마치며...</h4>
<p>리액트로 프로젝트 초기 세팅을 하려고 하는데 어디서는 yarn을 사용하고, 어디서는 npm을 사용해서 헷갈려서 알아보았다.
우선 나는 npm을 직접 사용해보아야 yarn의 필요성을 알 수 있을 것 같아서 나는 프로젝트 설치 모듈로 npm을 사용해보아야할 것 같다.</p>
<br />

<hr />

<p>** 참고한 글 **
<a href="https://velog.io/@jma1020/npm-yarn-%EB%AC%B4%EC%97%87%EC%9D%B4%EA%B3%A0-%EC%96%B4%EB%96%A4-%EC%B0%A8%EC%9D%B4">npm yarn 무엇이고 어떤 차이??</a>
<a href="https://velog.io/@kysung95/%EA%B0%9C%EB%B0%9C%EC%83%81%EC%8B%9D-npm%EA%B3%BC-yarn">[개발상식] npm과 yarn</a></p>