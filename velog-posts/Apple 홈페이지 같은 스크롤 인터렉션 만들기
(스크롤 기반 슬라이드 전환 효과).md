<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/e4d52206-f705-47d5-a424-1ba5b53b79ef/image.gif" /></p>
<p>Apple 홈페이지의 <a href="https://www.apple.com/kr/iphone-16-pro/">iphone16 pro 상세페이지</a>이다.
이 페이지는 스크롤을 계속 내리면 화면은 고정 되어 있지만(<em>고정 되어 있는 것 처럼 보이지만)</em>, 
오른쪽의 스크롤은 계속 밑으로 내려가고 있는 것을 볼 수 있다.</p>
<p>이와 비슷한 인터랙티브한 웹사이트를 개발 하면서 약간의 시행착오를 겪었기 때문에 포스팅하면서 정리해보려고 한다.
<br /></p>
<hr />



<p>첫 번째로 시도했던 방법은 <strong><a href="https://developer.mozilla.org/en-US/docs/Web/API/IntersectionObserver">Intersection Observer</a></strong> 이다.
Intersection Observer API는 브라우저 뷰포트와 원하는 요소의 교차점을 관찰하여,
<strong>요소가 뷰포트에 포함되는지 아닌지 구별하는 기능을 제공</strong>한다.
즉, 화면에 보이는지 보이지 않는지를 판단 한다.
<br /></p>
<pre><code class="language-typescript">let options = {
    threshold: 0.9,
};

const targetRef = useRef&lt;HTMLDivElement | null&gt;(null);

useEffect(() =&gt; {
    if(!targetRef.current) return;

  const observer = new IntersectionObserver((entries) =&gt; {
      entries.forEach((entry) =&gt; {
        console.log(entry.isIntersecting);
    }, options);

    observer.observe(targetRef.current);
  })
}, []);</code></pre>
<p>이렇게 작성하면 타겟 영역이 뷰포트에 90%(0.9)가 보이면 <code>entry.isIntersecting</code>이 <code>true</code> 를 리턴하고, 
<code>console</code>에 <code>true</code>를 출력하고, 영역 밖을 벗어나면 <code>false</code>를 출력하는 것을 확인할 수 있다.</p>
<p>나는 타겟 UI가 뷰포트 영역에 들어와 리턴 값이 <code>true</code>인 경우 Wheel 이벤트를 주려고 했는데, 
Wheel 이벤트는 모바일에서 사용할 수 없기 때문에  또 이를 고민하다가 내가 만드려고 하는 웹 페이지에 적합한 방법이 아닌 것 같다는 생각이 들었다.</p>
<p>이 시도를 하는 도중에 Apple 홈페이지를 참조해서 레퍼런스 삼아 만들기 시작했다.
어쨌든, 이 코드는 쓰지 않았지만 새로운 API를 써보았기 때문에 좋은 시행착오였다.</p>
<br />


<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/f29aadf1-d229-4695-b5bf-86c266d46aa0/image.gif" /></p>
<p>스크롤을 밑으로 움직이지만 영역은 고정되어 보이도록 시도한 두번째 방법이다.</p>
<pre><code class="language-typescript">const slides = [
  {
    title: '🐈 고양이',
    sub: '혁신적인 외모와 귀여움',
  },
  {
    title: '❤️ 짧지만 보드라운 털',
    sub: '현존 최강 성능 털빠짐',
  },
  {
    title: '😽 귀여워 사람 죽는 애교',
    sub: '애교의 새로운 차원',
  },
  {
    title: '🔋 하루 종일 잠 자는 능력',
    sub: '온종일 지속되진 못하는 파워',
  },
];

export default function Home() {
  const containerRef = useRef&lt;HTMLDivElement&gt;(null);
  const [index, setIndex] = useState(0);

  useEffect(() =&gt; {
    const handleScroll = () =&gt; {
      if (!containerRef.current) return;
      const { top } = containerRef.current.getBoundingClientRect();
      const screenHeight = window.innerHeight;
      const newIndex = Math.round(-top / screenHeight);
      setIndex(Math.max(0, Math.min(slides.length - 1, newIndex)));
    };

    window.addEventListener('scroll', handleScroll);
    return () =&gt; window.removeEventListener('scroll', handleScroll);
  }, []);

  return (
    &lt;Wrapper&gt;
      &lt;StickySection&gt;
        &lt;SlideWrapper&gt;
          {slides.map((slide, i) =&gt; (
            &lt;Slide key={i} active={i === index}&gt;
              &lt;Title&gt;{slide.title}&lt;/Title&gt;
              &lt;SubText&gt;{slide.sub}&lt;/SubText&gt;
            &lt;/Slide&gt;
          ))}
        &lt;/SlideWrapper&gt;
      &lt;/StickySection&gt;
      &lt;Spacer ref={containerRef}&gt;
        {slides.map((_, i) =&gt; (
          &lt;SlideSpacer key={i} /&gt;
        ))}
      &lt;/Spacer&gt;
    &lt;/Wrapper&gt;
  );
}</code></pre>
<p>스크롤을 아래로 내릴 때마다 한 화면 단위로 슬라이드를 변경하고, <code>Sticky</code> 요소 안에 슬라이드 내용이 애니메이션과 함께 전환된다.</p>
<p><code>top</code>을 화면 높이로 나누면 몇 번째 슬라이드인지 알 수 있기 때문에 이 값을 인덱스로 사용했다.
내부에 있는 슬라이드를 모두 <code>absolute</code> 포지션을 가지게 해서 현재 인덱스에 해당하는 경우 <code>opacity</code> 값을 변경해주었다.</p>
<p><code>SlideSpacer</code>는 각각 <code>height:100vh</code>로 구성해서 뷰포트의 스크롤 높이를 만들어준다.
<code>map</code>으로 슬라이드 갯수 만큼 만들어져있으므로 각 슬라이드마다 화면 높이 한개를 차지하게되고,
<code>StickySection</code>으로 영역을 고정했으므로 해당 영역은 항상 고정되어 보인다.</p>
<br />

<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/9ce5209a-fd84-4896-a6b1-cf6b06a41e6c/image.png" /></p>
<p>얼마 전까지 이러고 있었던 것 같은데... 🤣 재밌게 만들었다.</p>