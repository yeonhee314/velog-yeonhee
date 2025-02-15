<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/9d85378a-4ec8-4f8b-b73f-b9b8f94e74df/image.png" /></p>
<h2 id="리덕스redux란">리덕스(Redux)란?</h2>
<p>Redux는  React를 비롯한 JavaScript 애플리케이션에서 상태(state)를 효율적으로 관리하고 유지할 수 있도록 도와주는 상태관리(state management) JavaScript 라이브러리이다. 
애플리케이션의 많은 부분에 필요한 전역 상태를 관리하는데 도움이 된다.</p>
<br />

<h3 id="상태관리란-왜-필요한가">상태관리란 왜 필요한가?</h3>
<p>하나의 컴포넌트가 사용하는 데이터 역할을 상태라고 본다.
state는 자주 변화하고 상황에 따라 최상위 루트까지 접근을 해야하는데 매번 <code>props</code>로 계속 내려주는 비효율적인 일을 생략하고, 최단 거리로 사용할 수 있다.
그래서 예측이 가능하고, 예상대로 작동할 것이라는 확신을 갖도록 도와준다.</p>
<p>React에서 상태 관리를 할 때 <code>useState</code>나 <code>useContext</code>를 사용할 수 있지만, 애플리케이션이 커지면 상태를 여러 컴포넌트에서 공유해야 하는 문제가 발생한다.
이 때 Redux를 사용하면 중앙에서 상태를 관리하고, 필요한 곳에서 쉽게 가져다 쓸 수 있다.</p>
<br />

<h3 id="redux를-쓰면-좋은-경우">Redux를 쓰면 좋은 경우</h3>
<blockquote>
<ul>
<li>여러 컴포넌트가 같은 상태를 공유할 때</li>
</ul>
</blockquote>
<ul>
<li>상태를 한 곳에서 관리하면서, 예측 가능한 방식으로 업데이트하고 싶을 때</li>
<li>복잡한 비즈니스 로직이 있을 때</li>
</ul>
<br />

<h3 id="redux의-핵심-개념">Redux의 핵심 개념</h3>
<h4 id="1-store-저장소">1. Store (저장소)</h4>
<p>애플리케이션의 상태(state)를 저장하는 중앙 저장소
상태를 직접 수정하지 않고, 액션(action)과 리듀서(reducer)를 통해서만 변경할 수 있다.</p>
<h4 id="2-action액션">2. Action(액션)</h4>
<p>상태를 변경하기 위한 &quot;요청&quot;을 나타내는 객체이다.
<strong>type 속성을 반드시 포함</strong>하며, 추가적인 데이터를 payload로 전달할 수 있다.</p>
<pre><code class="language-javascript">const increment = { type: &quot;INCREMENT&quot; }; // 카운트를 증가시키는 액션
const decrement = { type: &quot;DECREMENT&quot; }; // 카운트를 감소시키는 액션</code></pre>
<h4 id="3-reducer-리듀서">3. Reducer (리듀서)</h4>
<p>현재 상태(state)와 액션(action)을 받아서 새로운 상태를 반환하는 함수
상태는 &quot;불변성&quot;을 유지하면서 변경해야 함</p>
<pre><code class="language-javascript">const counterReducer = (state = 0, action) =&gt; {
  switch (action.type) {
    case &quot;INCREMENT&quot;:
      return state + 1;
    case &quot;DECREMENT&quot;:
      return state - 1;
    default:
      return state;
  }
};</code></pre>
<p>만약 increment 버튼을 클릭하면 &quot;INCREMENT&quot; 액션이 발생
리듀서가 state + 1 로 업데이트
새로운 상태가 컴포넌트에 반영됨</p>
<br />

<h3 id="redux의-동작-흐름">Redux의 동작 흐름</h3>
<p>컴포넌트에서 액션을 디스패치(dispatch)
↓
Reducer가 액션을 받아 상태를 업데이트
↓
Store가 새로운 상태를 컴포넌트에 전달</p>
<br />

<h2 id="redux-toolkit-환경-세팅">Redux Toolkit 환경 세팅</h2>
<blockquote>
<p><strong>1. 패키지 설치</strong> → @reduxjs/toolkit, react-redux
 <strong>2. store.ts 생성</strong> → configureStore로 store 설정
<strong>3. counterSlice.ts 생성</strong> → createSlice로 Redux 로직 작성
 <strong>4. _app.tsx에서 Provider 설정</strong> → Redux를 전역으로 적용
<strong>5. Redux 상태 사용하기</strong> → useAppSelector, useAppDispatch 활용</p>
</blockquote>
<h3 id="1-redux-관련-패키지-설치">1. Redux 관련 패키지 설치</h3>
<pre><code class="language-bash">npm install @reduxjs/toolkit react-redux</code></pre>
<p>나는 리덕스 toolkit으로 세팅했다.
<code>@reduxjs/toolkit</code> 은 Redux 공식 툴킷으로 Redux 설정을 쉽게 해준다.
<code>react-redux</code>는 React에서 Redux를 사용할 수 있도록 도와준다.</p>
<br />

<h3 id="2-storets-생성-redux-store-설정">2. store.ts 생성 (Redux Store 설정)</h3>
<pre><code class="language-typescript">// store.ts
import { configureStore } from &quot;@reduxjs/toolkit&quot;;
import { useDispatch, useSelector, TypedUseSelectorHook } from &quot;react-redux&quot;;
import counterReducer from &quot;./slices/counterSlice&quot;; // 예제 슬라이스

// Redux Store 설정
export const store = configureStore({
  reducer: {
    counter: counterReducer, // 여기에 다른 reducer도 추가 가능
  },
});

// RootState 및 AppDispatch 타입 지정
export type RootState = ReturnType&lt;typeof store.getState&gt;;
export type AppDispatch = typeof store.dispatch;

// useDispatch, useSelector 타입 지정
export const useAppDispatch = () =&gt; useDispatch&lt;AppDispatch&gt;();
export const useAppSelector: TypedUseSelectorHook&lt;RootState&gt; = useSelector;
</code></pre>
<p><code>store.ts</code> 파일을 프로젝트 루트 또는 store 폴더에 생성한다.</p>
<br />

<h3 id="3-counterslicets-생성-redux-slice-설정">3. counterSlice.ts 생성 (Redux Slice 설정)</h3>
<pre><code class="language-bash">// slices/counterSlice.ts
import { createSlice, PayloadAction } from &quot;@reduxjs/toolkit&quot;;

interface CounterState {
  value: number;
}

// 초기 상태
const initialState: CounterState = {
  value: 0,
};

// Slice 생성
const counterSlice = createSlice({
  name: &quot;counter&quot;,
  initialState,
  reducers: {
    increment: (state) =&gt; {
      state.value += 1;
    },
    decrement: (state) =&gt; {
      state.value -= 1;
    },
    incrementByAmount: (state, action: PayloadAction&lt;number&gt;) =&gt; {
      state.value += action.payload;
    },
  },
});

// 액션과 리듀서 내보내기
export const { increment, decrement, incrementByAmount } = counterSlice.actions;
export default counterSlice.reducer;
</code></pre>
<p><code>slices/counterSlice.ts</code> 파일을 생성하고 아래 코드 추가한다.</p>
<p><strong>Redux Slice는 Redux Toolkit에서 상태(state)와 reducer를 한번에 관리하는 파일</strong>이다.
기존 Redux에서는 action, reducer, store를 따로 관리해야했는데 
ReduxToolkit에서 <code>createSlice</code>를 사용하면 한 파일에서 처리가 가능함.</p>
<br />

<h3 id="4-_apptsx에서-redux-provider-설정">4. _app.tsx에서 Redux Provider 설정</h3>
<pre><code class="language-bash">// pages/_app.tsx
import type { AppProps } from &quot;next/app&quot;;
import { Provider } from &quot;react-redux&quot;;
import { store } from &quot;../store&quot;;

export default function MyApp({ Component, pageProps }: AppProps) {
  return (
    &lt;Provider store={store}&gt;
      &lt;Component {...pageProps} /&gt;
    &lt;/Provider&gt;
  );
}
</code></pre>
<p><code>pages/_app.tsx</code> 파일을 수정해서 Redux Store를 앱에 적용한다.</p>
<p><strong><code>Provider</code>는 번역하면 공급자 라는 뜻으로 Redux Store를 앱에 연결하는 역할</strong>을 한다.
Redux에서 <strong>전역 상태(state)를 관리하려면, 모든 컴포넌트가 store에 접근할 수 있어야하는데, 그 역할을 하는 것이 바로 <code>Provider</code>이다.</strong></p>
<p><code>Provider</code>를 사용하려면 ** Redux Store를 React앱의 최상위 컴포넌트에 등록**해서 하위 컴포넌트들이 <code>useSelector</code>와 <code>useDispatch</code>를 사용해서 상태를 읽고, 업데이트할 수 있다.</p>
<br />

<h3 id="5redux-상태-사용하기-예제">5.Redux 상태 사용하기 (예제)</h3>
<pre><code class="language-bash">// pages/index.tsx
import { useAppDispatch, useAppSelector } from &quot;../store&quot;;
import { increment, decrement, incrementByAmount } from &quot;../slices/counterSlice&quot;;

export default function Home() {
  const count = useAppSelector((state) =&gt; state.counter.value);
  const dispatch = useAppDispatch();

  return (
    &lt;div&gt;
      &lt;h1&gt;Counter: {count}&lt;/h1&gt;
      &lt;button onClick={() =&gt; dispatch(increment())}&gt;+1&lt;/button&gt;
      &lt;button onClick={() =&gt; dispatch(decrement())}&gt;-1&lt;/button&gt;
      &lt;button onClick={() =&gt; dispatch(incrementByAmount(5))}&gt;+5&lt;/button&gt;
    &lt;/div&gt;
  );
}
</code></pre>
<p>Redux상태를 Next.js 페이지에서 사용한다.
<code>pages/index.tsx</code>에서 <code>useAppSelector</code>와 <code>useAppDispatch</code>를 활용</p>
<p><br /><br /></p>
<hr />




<p>** 출처/참고한 글 **
<a href="https://velog.io/@s_soo100/Redux-%EB%A6%AC%EC%95%A1%ED%8A%B8-%EB%A6%AC%EB%8D%95%EC%8A%A4-%EC%8A%A4%ED%84%B0%EB%94%941">[React-Redux] 개념부터 기본 사용법 까지</a>
<a href="https://velog.io/@party3205/Redux-%EA%B0%9C%EB%85%90%EA%B3%BC-%EC%82%AC%EC%9A%A9%EB%B0%A9%EB%B2%95-%EC%A0%95%EB%A6%AC">[Redux] 개념과 사용방법 정리</a></p>