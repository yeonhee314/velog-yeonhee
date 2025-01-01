<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/780f0a21-3be1-4804-b038-2198cf606fc9/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/7fe2f42c-9e77-4193-a9de-74ca343b1b83/image.png" /></p>
<p><strong>정규표현식(Regex; Regular Expression)</strong>을 정리하게 된 데에는...
프로그래머스 문제를 풀고 나서 다른 사람의 풀이를 봤는데 
나는 복잡하게 푼 문제를 다른 사람은 정규식을 사용해서 무려 한줄로 풀었다..! 
다음엔 나도 꼭 효율적으로 풀 것이라 다짐하며...
<em>(짧은 코드가 무조건 효율적이라는건 아니지만 저는 그에 비해 비효율적으로 코드를 짰습니다.)</em></p>
<br />


<p><br /><br /></p>
<h2 id="💡정규-표현식regular-expression이란">💡정규 표현식(Regular Expression)이란?</h2>
<blockquote>
<p>정규표현식이란 문자열 데이터 중에서 원하는 조건(패턴)과 일치하는 문자열 부분을 찾아내기 위해 사용하는 것으로, 미리 정의된 기호와 문자를 이용해서 작성한 문자열을 말한다.</p>
</blockquote>
<p>개발을 할 때 전화번호, 주민번호, 이메일 등과 같이 정해져있는 형식이 있고 사용자가 그 형식대로 제대로 입력했는지 검증해야 하는 경우 정규 표현식을 사용하면 쉽게 구현할 수 있다.
<br /></p>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/883ab42c-efc1-48de-a15a-2c236933dd4e/image.png" />
정규식을 이용하면 많은 양의 텍스트 파일 중 원하는 데이터를 손쉽게 뽑아낼 수 있고, 입력된 데이터가 형식에 맞는지 체크할 수 있다. 하지만 문자 기호 조합으로 가독성이 떨어진다는 단점이 있다.</p>
<p>📚 자바 외의 대부분의 언어들도 정규 표현식을 지원하며, 사용법은 언어마다 차이가 있지만 거의 비슷하다. </p>
<p><br /><br /></p>
<h3 id="정규식-기본-기호">정규식 기본 기호</h3>
<table>
  <tr>
    <th>기호</th>
    <th>설명</th>
    <th>예제</th>
  </tr>
  <tr>
    <td>.</td>
    <td>임의의 문자 1개를 의미한다.</td>
    <td></td>
  </tr>
  <tr>
      <td>^</td>
    <td>시작을 의미한다.<br />[] 괄호 안에 있다면 일치하지 않는 부정의 의미로 쓰인다.</td>
    <td>^a : a로 시작하는 단어<br />[^a] : a가 아닌 철자인 문자 1개</td>
  </tr>
  <tr>
      <td>$</td>
    <td>$ 앞의 문자열로 문자가 끝나는 지를 의미한다.</td>
    <td>a$ : a로 끝나는 단어</td>
  </tr>
  <tr>
      <td>[]</td>
    <td>[] 괄호 안의 문자가 있는지를 확인한다.</td>
    <td>[ab][cd] : a, b중 한 문자와 c,d중 한 문자<br /> → ac ad bc bd</td>
  </tr>
  <tr>
      <td>[^]</td>
    <td>[] 대괄호 안에 ^ 문자가 있으면 제외를 뜻한다.<br />
      - 대괄호 안에 ^가 쓰이면 제외의 뜻<br />
      - 대괄호 밖에 ^가 쓰이면 시작점의 뜻
    </td>
    <td>[^a-z] : 알파벳 소문자 a부터 z를 제외한 모든 문자</td>
  </tr>
  <tr>
      <td>-</td>
    <td>
      사이의 문자 혹은 숫자를 의미한다.
    </td>
    <td>
    [a-z] : 알파벳 소문자 a부터 z까지 하나
      <br />[a-z0-9] : 알파벳 소문자 전체, 0~9중 한 문자
    </td>
  </tr>
  <tr>
      <td>|</td>
    <td>또는
    </td>
    <td>[a|b] : a 혹은 b</td>
  </tr>
  <tr>
      <td>()</td>
    <td>그룹
    </td>
    <td>01(0|1) : 01 뒤에 0 또는 1이 들어간다.<br />
    →010(o), 011(o), 012(x)</td>
  </tr>
  <tr>
      <td>{}</td>
    <td>개수
    </td>
    <td>a{3}b : a가 3번 온 후 b가 온다
    <br />
      → aab(x), aaab(o), aaaab(o)
    </td>
  </tr>
  <tr>
      <td>\b</td>
    <td>공백, 탭, ",", "/" 등을 의미한다.
    </td>
    <td>apple\b : apple 뒤에 공백 탭 등이 있다.  
    <br />
      → apple juice (o), apple.com (x)
    </td>
  </tr>
  <tr>
      <td>\B</td>
    <td>\b의 부정
      <br />
      공백 탭등이 아닌 문자인 경우 매치한다.
    </td>
    <td>apple\B
    <br />
    → apple.com (o)
    </td>
  </tr>
  <tr>
      <td>\d</td>
    <td>0~9 사이의 숫자
      <br />
      [0~9]와 동일
    </td>
    <td></td>
  </tr>
  <tr>
      <td>\D</td>
    <td>\d의 부정
      <br />
      숫자가 아닌 어떤 문자, [^0~9]와 동일
    </td>
    <td></td>
  </tr>
  <tr>
      <td>\s</td>
    <td>공백, 탭
    </td>
    <td></td>
  </tr>
  <tr>
      <td>\S</td>
    <td>공백, 탭이 아닌 문자
    </td>
    <td></td>
  </tr>
  <tr>
      <td>\w</td>
    <td>
      알파벳 대소문자 + 숫자 + "_"
      <br />
      [a-zA-Z_0-9]와 동일
    </td>
    <td></td>
  </tr>
  <tr>
      <td>\W</td>
    <td>\w의 부정
      <br />
      [^a-zA-Z_0-9]와 동일
    </td>
    <td></td>
  </tr>
</table>

<br />

<h3 id="정규식-수량-기호">정규식 수량 기호</h3>
<table>
  <tr>
    <th>기호</th>
    <th>설명</th>
    <th>예제</th>
  </tr>
  <tr>
    <td>?</td>
    <td>앞의 표현식이 없거나 or 최대 한개만</td>
    <td>a1? : 1이 최대 한개만 있거나 없을 수도 있다.
    <br />
      → a(o), a1(o), a11(x), a111(x)
    </td>
  </tr>
  <tr>
    <td>*</td>
    <td>앞의 표현식이 없거나  or 있거나(여러개)</td>
    <td>a1* : 1이 있을 수도 없을 수도 있다. 
    <br />
      → a(o), a1(o), a11(o), a111(o)
    </td>
  </tr>
  <tr>
    <td>+</td>
    <td>앞의 표현식이 1개 이상 or 여러개</td>
    <td>a1+ : 1이 1개 이상 있다.
    <br />
      → a(x), a1(o), a11(o), a111(o)
    </td>
  </tr>
  <tr>
    <td>{n}</td>
    <td>딱 n개 있다.</td>
    <td>a{3} : a가 딱 3개 있다.
    <br />
      → aa(x), aaa(o), aaaa(x), aaaaaaaa(x)
    </td>
  </tr>
  <tr>
    <td>{n, m}</td>
    <td>n개 이상 m개 이하</td>
    <td>a{3,5} : a가 3개 이상 5개 이하 있다.
    <br />
      → aa(x), aaa(o), aaaa(o), aaaaaaaa(x)
    </td>
  </tr>
  <tr>
    <td>{n, }</td>
    <td>n개 이상</td>
    <td>a{3,} : a가 3개 이상 있다.
    <br />
      → aa(x), aaa(o), aaaa(o), aaaaaaaaa(o)
    </td>
  </tr>
</table>

<br />

<h3 id="정규식-그룹-캡쳐-기호">정규식 그룹 캡쳐 기호</h3>
<p>()로 그룹화 한다고 했을 때 이를 '캡쳐한다'고 한다. </p>
<table>
  <tr>
    <th>기호</th>
    <th>설명</th>
  </tr>
  <tr>
    <td>0</td>
    <td>그룹 및 캡쳐</td>
  </tr>
  <tr>
    <td>(?:)</td>
    <td>찾지만 그룹에 포함 안됨</td>
  </tr>
  <tr>
    <td>(?=)</td>
    <td>=앞 문자를 기준으로 전방 탐색</td>
  </tr>
  <tr>
    <td>(?<=)</td>
    <td>=뒤 문자를 기준으로 후방 탐색</td>
  </tr>
  </table>


<p><br /><br /></p>
<p><strong>🤓 마치며...</strong>
내용은 새롭게 계속 알아낼 때 마다 업데이트 될 것입니다..!!!! 
완벽하게 이해하고 사용하는 그날 까지 달려달려. 렛츠고!!!</p>
<p><br /><br /><br />
<strong>출처/참고한 글:</strong>
<a href="https://adjh54.tistory.com/104">[Java] 정규표현식(RegExp) 이해하기 : 패턴, 문자 클래스, 자주 사용 패턴</a>
<a href="https://medium.com/@tararamgoyal4_92353/how-to-build-regular-expression-in-java-16e3c3cc9f43">How to build Regular Expression in Java - TARA RAM GOYAL</a>
<a href="https://inpa.tistory.com/entry/JAVA-%E2%98%95-%EC%A0%95%EA%B7%9C%EC%8B%9DRegular-Expression-%EC%82%AC%EC%9A%A9%EB%B2%95-%EC%A0%95%EB%A6%AC">자바 정규식(Regular Expression)사용법 정리 - 인파</a>
<a href="https://dogcowking.tistory.com/230">정규표현식 그룹 캡쳐 활용 - 패턴 일치부분 가져오기</a></p>