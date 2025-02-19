<h2 id="typescript의-record란">TypeScript의 Record란?</h2>
<blockquote>
<p><code>Record&lt;Key, Value&gt;</code>
키가 Key타입이고, 값이 Value타입인 객체 타입을 생성한다.</p>
</blockquote>
<p>타입스크립트의 <strong>유틸리티 타입(Utility Types)</strong> 중 하나로, 인덱스 시그니처와 유사한 기능을한다.
유틸리티 타입은 타입스크립트에서 <strong>타입 변경을 쉽고 용이</strong>하게 하기 위한 헬퍼 함수같은 것이다.
유틸리티 타입을 쓰지 않더라도 기존의 인터페이스, 제네릭 등의 기본 문법으로 충분히 타입 변환이 가능하지만 유틸리티 타입을 쓰면 훨씬 더 간결한 문법으로 타입을 정의할 수 있다.</p>
<pre><code class="language-typescript">type Score = {
    [name: string] : number; 
}

// Score와 동일한 역할
type ScoreRecord = Record&lt;string, number&gt;;
let scores: ScoreRecord = {
      '축구' : 100, 
      '야구' : 200,
};</code></pre>
<p><code>Record</code>가 인덱스 시그니처와 다른 점은, <strong>Key로 문자열 리터럴을 사용할 수 있다</strong>는 것이다.</p>
<pre><code class="language-typescript">type Score = {
 [name: '축구' | '야구']: number; 
}

// Error! </code></pre>
<p>인덱스 시그니처(Index Signature)는 <code>{[key: T] : U}</code>형식으로 객체가 여러 Key를 가질 수 있으며 Key와 매칭되는 value를 가지는 경우 사용한다. 
인덱스 시그니처는 객체가 &lt;key, value&gt;형식이고, key와 value의 타입을 정확하게 명시해야 하는 경우 사용할 수 있다.
** TypeScript는 기본적으로 객체의 프로퍼티를 읽을 때 string 타입의 key사용을 허용하지 않는다. **</p>
<p>하지만 <code>Record</code>는 Key로 문자열 리터럴을 사용할 수 있다.</p>
<p><br /><br /><hr /></p>
<p>** 참고한 글 **
<a href="https://cheeseb.github.io/typescript/typescript-record/">[Typescript] Record 타입 사용하기 (feat. Mapped Type)</a>
<a href="https://velog.io/@ahsy92/TypeScript-%EC%9D%B8%EB%8D%B1%EC%8A%A4-%EC%8B%9C%EA%B7%B8%EB%8B%88%EC%B2%98">[TypeScript] 인덱스 시그니처</a>
<a href="https://inpa.tistory.com/entry/TS-%F0%9F%93%98-%ED%83%80%EC%9E%85%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%9C%A0%ED%8B%B8%EB%A6%AC%ED%8B%B0-%ED%83%80%EC%9E%85-%F0%9F%92%AF-%EC%B4%9D%EC%A0%95%EB%A6%AC">📘 타입스크립트 유틸리티 타입 💯 총정리 (+응용)</a></p>