<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/9a89e9ae-fb96-47ce-91ff-a7bcf3762934/image.png" /></p>
<h2 id="i18n이란">i18n이란?</h2>
<p>i18n은 &quot;Internationalization&quot;(국제화)의 약어이다.
&quot;i&quot;와 &quot;n&quot; 사이에 18개의 글자가 있어서 i18n이라고 부른다.</p>
<p>웹사이트나 애플리케이션을 여러 언어와 문화권에서 사용할 수 있도록 만드는 과정이다.
예를 들어, 영어와 한국어를 지원하는 웹사이트를 만든다면, 언어를 쉽게 전환할 수 있어야 한다.</p>
<pre><code class="language-json">// en.json (영어)
{
  &quot;welcome&quot;: &quot;Hello!&quot;,
  &quot;greeting&quot;: &quot;How are you?&quot;
}

// ko.json (한국어)
{
  &quot;welcome&quot;: &quot;안녕하세요!&quot;,
  &quot;greeting&quot;: &quot;잘 지내세요?&quot;
}</code></pre>
<p>이렇게 만들어두고 사용자가 언어를 바꾸면 자동으로 해당 언어로 변경되도록 한다.</p>
<br />


<h2 id="i18n의-주요-개념">i18n의 주요 개념</h2>
<blockquote>
<ul>
<li><strong>번역 (Translation)</strong>
각 언어별 번역 파일(json, yaml, etc.)을 만들어서 적용
en.json, ko.json처럼 파일을 만들고 필요한 문구를 번역함.</li>
</ul>
</blockquote>
<ul>
<li><strong>지역화 (Localization, L10n)</strong>
언어뿐만 아니라 날짜/시간/화폐/단위까지 문화권에 맞게 변경
예) YYYY/MM/DD (한국) vs MM/DD/YYYY (미국)</li>
<li><strong>자동 감지 (Language Detection)</strong>
사용자의 브라우저 언어 감지해서 기본 언어 설정
예) 한국에서 접속하면 자동으로 ko 사용</li>
</ul>
<br />




<br />

<h2 id="i18n-사용하기">i18n 사용하기</h2>
<h3 id="1-설치">1. 설치</h3>
<pre><code class="language-bash">npm i i18next

// Next.js 기준 Redux + i18n 적용
npm install redux react-redux @reduxjs/toolkit react-i18next i18next i18next-browser-languagedetector i18next-http-backend
</code></pre>
<p><a href="https://www.npmjs.com/package/i18next">npm </a> 으로 설치할 수 있다.</p>
<br />

<h3 id="2-redux-설정-storejs">2. Redux 설정 (store.js)</h3>
<pre><code class="language-typescript">import { configureStore, createSlice } from &quot;@reduxjs/toolkit&quot;;

// 초기 언어 상태
const initialState = { language: &quot;en&quot; };

// 언어 상태를 관리하는 slice
const languageSlice = createSlice({
  name: &quot;language&quot;,
  initialState,
  reducers: {
    setLanguage: (state, action) =&gt; {
      state.language = action.payload;
    },
  },
});

// 액션 및 리듀서 내보내기
export const { setLanguage } = languageSlice.actions;
export const store = configureStore({
  reducer: { language: languageSlice.reducer },
});
</code></pre>
<br />

<h3 id="3-i18n-설정i18njs">3. i18n 설정(i18n.js)</h3>
<pre><code class="language-typescript">import i18n from &quot;i18next&quot;;
import { initReactI18next } from &quot;react-i18next&quot;;
import LanguageDetector from &quot;i18next-browser-languagedetector&quot;;
import HttpApi from &quot;i18next-http-backend&quot;;

i18n
  .use(initReactI18next) // React와 연결
  .use(LanguageDetector) // 브라우저 언어 감지
  .use(HttpApi) // 언어 파일 로드 (백엔드 사용 가능)
  .init({
    fallbackLng: &quot;en&quot;, // 기본 언어
    debug: true, // 디버깅 활성화
    interpolation: {
      escapeValue: false, // React에서 XSS 방지 자동 처리
    },
    resources: {
      en: {
        translation: {
          welcome: &quot;Hello!&quot;,
        },
      },
      ko: {
        translation: {
          welcome: &quot;안녕!&quot;,
        },
      },
    },
  });

export default i18n;
</code></pre>
<br />

<h3 id="4-provider-적용-pages_appjs">4. Provider 적용 (pages/_app.js)</h3>
<pre><code class="language-typescript">import { Provider } from &quot;react-redux&quot;;
import { store } from &quot;../store&quot;;
import { I18nextProvider } from &quot;react-i18next&quot;;
import i18n from &quot;../i18n&quot;;

function MyApp({ Component, pageProps }) {
  return (
    &lt;Provider store={store}&gt;
      &lt;I18nextProvider i18n={i18n}&gt;
        &lt;Component {...pageProps} /&gt;
      &lt;/I18nextProvider&gt;
    &lt;/Provider&gt;
  );
}

export default MyApp;
</code></pre>
<p><code>Provider</code>로 Redux와 i18n을 적용한다.</p>
<br />

<h3 id="5-redux와-i18n을-함께-사용하는-컴포넌트">5. Redux와 i18n을 함께 사용하는 컴포넌트</h3>
<pre><code class="language-typescript">import { useDispatch, useSelector } from &quot;react-redux&quot;;
import { setLanguage } from &quot;../store&quot;;
import { useTranslation } from &quot;react-i18next&quot;;

const LanguageSwitcher = () =&gt; {
  const dispatch = useDispatch();
  const { i18n } = useTranslation();
  const language = useSelector((state) =&gt; state.language.language);

  // 언어 변경 함수
  const changeLanguage = (lang) =&gt; {
    i18n.changeLanguage(lang);
    dispatch(setLanguage(lang));
  };

  return (
    &lt;div&gt;
      &lt;p&gt;현재 언어: {language}&lt;/p&gt;
      &lt;button onClick={() =&gt; changeLanguage(&quot;en&quot;)}&gt;English&lt;/button&gt;
      &lt;button onClick={() =&gt; changeLanguage(&quot;ko&quot;)}&gt;한국어&lt;/button&gt;
    &lt;/div&gt;
  );
};

export default LanguageSwitcher;
</code></pre>
<p><code>LanguageSwitcher.js</code> (언어 변경 버튼)</p>
<br />


<h3 id="6-i18n-적용된-텍스트-사용하기">6. i18n 적용된 텍스트 사용하기</h3>
<p><code>Home.js</code></p>
<pre><code>import { useTranslation } from &quot;react-i18next&quot;;
import LanguageSwitcher from &quot;./LanguageSwitcher&quot;;

const Home = () =&gt; {
  const { t } = useTranslation();

  return (
    &lt;div&gt;
      &lt;h1&gt;{t(&quot;welcome&quot;)}&lt;/h1&gt;
      &lt;LanguageSwitcher /&gt;
    &lt;/div&gt;
  );
};

export default Home;
</code></pre><br />
Redux와 i18n을 적용하면, 
> 1. Redux로 현재 선택된 언어를 관리할 수 있다.
2. i18n을 이용해 다국어 지원 가능하다.
3. `useSelector`로 현재 언어를 가져와서 UI 업데이트
4. `dispatch`(setLanguage(lang))으로 Redux 상태 변경

<p><br /><br /></p>
<h3 id="📃-nextjs-i18n-적용-후-hydration-error-발생-원인-에러-발생-원인">📃 Next.js i18n 적용 후 Hydration Error 발생 원인 에러 발생 원인</h3>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/d7616f4b-0433-4c51-8d98-d8ffa6cd0735/image.png" /></p>
<blockquote>
<p>코드에서 default 옵션을 en 으로 변경 &gt; 로컬스토리지에 저장 됨
코드에서 default 옵션 제거
서버와 클라이언트 간 데이터 불일치</p>
</blockquote>
<p>에러 메시지를 보면 서버에서는 <code>&quot;안녕&quot;</code>을 렌더링했는데, 클라이언트에서는 <code>&quot;hello&quot;</code>를 렌더링해서 불일치가 발생했다.</p>
<h3 id="hydration-error-원인">Hydration Error 원인</h3>
<blockquote>
<p>** 서버 사이드 렌더링(SSR)과 클라이언트에서의 값이 다름 **</p>
</blockquote>
<p>Next.js는 기본적으로 서버에서 먼저 HTML을 렌더링한 후, <strong>클라이언트에서 Hydration(상태 동기화)</strong>을 수행한다.
i18n 설정이 클라이언트에서 변경되면서 서버와 클라이언트의 번역값이 달라진다면 이 문제가 발생할 수 있다.
<strong>초기 언어 값이 서버와 클라이언트에서 다르게 설정된 것</strong>이다.</p>
<p>서버에서는 defaultLocale이 적용되었는데, 클라이언트에서는 navigator.language 등을 기반으로 번역값이 다를 수 있다.
<br /></p>
<h4 id="-useeffect에서-클라이언트-측에서-언어를-변경할-경우">* <code>useEffect</code>에서 클라이언트 측에서 언어를 변경할 경우</h4>
<p>클라이언트에서 <code>useEffect</code>로 언어를 바꾸면, 초기 서버 렌더링과 다른 값이 들어가면서 hydration 에러가 발생할 수 있다.</p>
<h3 id="해결-방법">해결 방법</h3>
<h4 id="1-useeffect를-사용해-클라이언트에서-언어-설정-보정하기">1. useEffect를 사용해 클라이언트에서 언어 설정 보정하기</h4>
<pre><code class="language-typescript">import { useEffect, useState } from &quot;react&quot;;
import { useTranslation } from &quot;next-i18next&quot;;

export default function Home() {
  const { t, i18n } = useTranslation();
  const [isClient, setIsClient] = useState(false);

  useEffect(() =&gt; {
    setIsClient(true); // 클라이언트에서 실행됨
  }, []);

  return &lt;div&gt;{isClient ? t(&quot;hello&quot;) : &quot;&quot;}&lt;/div&gt;;
}</code></pre>
<p>서버와 클라이언트의 언어 값이 다를 수 있으므로, 클라이언트에서 한 번 더 동기화하는 방법이 있다.
isClient 상태를 만들어 클라이언트에서만 번역 값을 적용하면 서버와 클라이언트의 값 불일치를 방지할 수 있다.</p>
<br />

<h4 id="2-nextjs-getserversideprops에서-언어-값-설정">2. Next.js getServerSideProps에서 언어 값 설정</h4>
<pre><code class="language-typescript">export async function getServerSideProps({ locale }) {
  return {
    props: {
      locale,
    },
  };
}</code></pre>
<p>Next.js에서 <code>getServerSideProps</code>를 사용해서 서버와 클라이언트의 언어 값을 맞출 수도 있다.</p>
<p>서버에서 locale을 받아오고, 클라이언트에서 이를 기반으로 i18n을 설정하면 서버와 클라이언트의 불일치를 방지할 수 있다.</p>
<br />

<p>어떤 방식이든 서버와 클라이언트의 초기 언어 값을 일치시키는 것이 중요하다.
 <strong>서버와 클라이언트에서 동일한 초기 번역 값을 유지하는 것이 핵심</strong>이다.
 <code>useEffect</code>를 사용해 클라이언트에서 한 번 더 보정하는 방식이 가장 일반적이고, 
<code>getServerSideProps</code>로 서버에서 언어를 가져오는 방법도 있다.</p>