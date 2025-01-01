<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/691d5252-785c-4364-85f8-1279abe1baa3/image.png" /></p>
<p>단위 테스트는 적은 비용, 유지보수의 용이함의 장점으로 중요하게 사용된다.
실무에서도 굉장히 많이 사용하므로 필수로 알아두는 것이 좋을 것 같아 정리하게 되었다.</p>
<h3 id="단위테스트란">단위테스트란?</h3>
<blockquote>
<p>하나의 모듈을 기준으로 독립적으로 진행되는 가장 작은 단위의 테스트</p>
</blockquote>
<p>단위테스트는 해당 부분만 독립적으로 테스트하기 때문에 어떤 코드를 리팩토링 해도 빠르게 문제 여부를 확인할 수 있다.</p>
<ul>
<li>테스팅에 대한 시간과 비용을 절감할 수 있다.</li>
<li>새로운 기능 추가 시에 수시로 빠르게 테스트 할 수 있다.</li>
<li>리팩토링 시에 안정성을 확보할 수 있다.</li>
<li>코드에 대한 문서가 될 수 있다.</li>
</ul>
<br />

<h3 id="좋은-단위테스트의-특징">좋은 단위테스트의 특징</h3>
<p>코드를 변경하는 것은 버그가 발생할 수 있음을 내포한다.
좋은 테스트 코드가 있다면 변경된 코드를 검증함으로써 이를 해결할 수 있다.
실제 코드가 변경되면 테스트 코드도 변경해야할 수 있는데 이러한 이유로 테스트 코드도 가독성있게 작성할 필요가 있다.</p>
<blockquote>
<ol>
<li>한개의 테스트 함수에 대해 assert를 최소화 하라.</li>
<li>1개의 테스트 함수는 1가지 개념만을 테스트 하라.</li>
</ol>
</blockquote>
<p>또한 좋고 깨끗한 코드는 <strong>FIRST</strong>라는 5가지 규칙을 따라야 한다.</p>
<blockquote>
<ol>
<li>Fast : 테스트는 빠르게 동작하여 자주 돌릴 수 있어야 한다.</li>
<li>Independent: 각각의 테스트는 독립적이며 서로 의존해서는 안된다.</li>
<li>Repeatable: 어느 환경에서도 반복 가능해야 한다.</li>
<li>Self-Validating: 테스트는 성공 또는 실패로 bool값으로 결과를 내어 자체적으로 검증되어야 한다.</li>
<li>Timely: 테스트는 적시에 즉, 테스트하려는 실제 코드를 구현하기 직전에 구현해야 한다.</li>
</ol>
</blockquote>
<p>단위 테스트의 가장 큰 장점은 개발한 코드를 바로 검증받고, 테스트를 통과하지 못하면 코드를 수정해 또 다시 빠르게 검증 받는 것이다. 수시로 실행하며 검증하면서 버그를 잡고 개발 비용을 줄여나갈 때 테스트의 가치를 느낄 수 있다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/71e6fd29-881b-4215-9726-c4b467b8851f/image.png" />
JUnit이란 자바 언어를 위한 단위 테스트 프레임 워크이다.
단위는 보통 메소드가 사용되는데 JUnit을 사용하면 단위 테스트를 작성하고 테스트하는 데 도움을 준다.
<br /></p>
<h3 id="junit-특징">JUnit 특징</h3>
<blockquote>
<ul>
<li>테스트 방식을 구분할 수 있는 어노테이션을 제공한다.</li>
</ul>
</blockquote>
<ul>
<li>@Test 어노테이션으로 케소드를 호출할 때 마다 새 인스턴스를 생성한다. <ul>
<li>독립 테스트가 가능하다.</li>
</ul>
</li>
<li>예상 결과를 검증하는 assert 메소드를 제공한다.</li>
<li>사용 방법이 단순하고 테스트 코드 작성시간이 적다.</li>
<li>자동 실행, 자체 결과를 확인하고 즉각적인 피드백을 제공한다.</li>
</ul>
<br />

<h3 id="테스트-시-주의-사항">테스트 시 주의 사항</h3>
<blockquote>
<ul>
<li>테스트 메소드는 추상메소드이면 안된다.</li>
</ul>
</blockquote>
<ul>
<li>테스트 메소드는 어떤 값도 return 해서는 안된다.</li>
<li>Happy path만 생각하는 것이 아니라, Unhappy path를 생각해야 한다.</li>
</ul>
<p>Happy path는 주요 흐름을 말하고, Unhappy path는 예외 흐름을 말한다.</p>
<p><br /><br /></p>
<h3 id="assert-메소드">Assert 메소드</h3>
<table>
  <tr>
    <td>assertEquals(a,b);</td>
    <td>객체 a와 b의 실제 값이 일치한지 확인한다.<br />
        a(예상 값)과 b(실제 값)이 같으면 테스트 통과
    </td>
  </tr>
  <tr>
    <td>assertArrayEquals(a, b);</td>
    <td>배열 a와 b가 일치함을 확인한다.</td>
  </tr>
  <tr>
    <td>assertFalse(x)</td>
    <td>x가 false인지 확인한다.</td>
  </tr>
  <tr>
    <tr>
    <td>assertTrue(x)</td>
    <td>x가 true인지 확인한다.</td>
  </tr>
    <td>assertSame(a,b);</td>
    <td>객체 a와 b가 같은 객체임을 확인한다. <br />
      a와 b가 같은 객체를 참조하고 있으면 테스트를 통과한다.
    <br />
       - assertEquals 메서드는 두 객체의 값의 비교 <br />
      - assertSame 메서드는 두 객체가 동일한지 객체의 비교<br />(두 객체의 레퍼런스가 동일한가를 확인한다.)
    </td>
  </tr>
  <tr>
    <td>assertNotSame(a, b);</td>
    <td>a와 b가 같은 객체를 참조하고 있지 않으면 통과한다.</td>
  </tr>
  <tr>
    <td>assertTrue(a);</td>
    <td>조건 a가 참인가를 확인한다.</td>
  </tr>
  <tr>
    <td>assertTure(message, condition);</td>
    <td>condition이 true이면 message를 표시한다.</td>
  </tr>
  <tr>
    <td>assertNull(a);</td>
    <td>객체 a가 null인지 확인한다.</td>
  </tr>
  <tr>
    <td>assertNotNull(a);</td>
    <td>객체 a가 null이 아님을 확인한다.</td>
  </tr>
  <tr>
    <td>assertfail();</td>
    <td>테스트를 바로 실패처리한다.</td>
  </tr>
  </table>

<p><br /><br /></p>
<h2 id="junit으로-단위-테스트-코드-만들기">JUnit으로 단위 테스트 코드 만들기</h2>
<p>스프링 부트 2.x 이후 버전에서는 JUnit4 및 JUnit5 테스트를 모두 실행할 수 있다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/e1f7ed46-8ac0-4f86-b1e3-5d1f2ff4509f/image.png" /></p>
<p>src/test/java 경로에 jUnitTest 패키지 안에 <em><del>JUnitTest</del></em> 클래스를 만들었다.
<br /><br /><br /></p>
<h3 id="→-2024-12-09-수정"><strong>→ 2024-12-09 수정</strong></h3>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/0dbc1664-7f27-4b70-bc93-925294df0543/image.png" />
패키지 이름 규칙을 지키지 않고 패키지를 작성해서 경고가 발생했다.
<strong>패키지 이름은 모두 소문자로 작성해야 하고 도메인 이름의 역순으로 작성해야 한다.</strong>
아래는 패키지이름이 대문자로 되어있으나 다음부터는 소문자로 적어 패키지 이름 규칙을 지켜 작업해야한다.</p>
<p><br /><br /><br /></p>
<pre><code class="language-java">package JunitTest;

import org.junit.jupiter.api.Assertions;
import org.junit.jupiter.api.DisplayName;
import org.junit.jupiter.api.Test;

public class JUnitTest {
    @DisplayName(&quot;1+2는 3&quot;)        // 테스트 이름
    @Test                        // 테스트 메소드
    public void junitTest() {
        int a = 1;
        int b = 2;
        int sum = 3;

        Assertions.assertEquals(sum, a + b);
    }
}</code></pre>
<p>1) 테스트 클래스는 반드시 public으로 선언해야 한다.
2) 클래스명은 관례상 테스트 클래스명 + TEST 를 끝나는 이름으로 사용해야 한다.
3) @Test 어노테이션을 선언한 메서드는 JUnit이 알아서 실행할 수 있게 한다.
<br /><br /></p>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/b046ec0a-d993-47a7-907e-b00a1b7d10c0/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/b932ec21-942c-47c1-a8ee-7b72cfe58af0/image.png" /></p>
<p>테스트 코드를 작성한 뒤 클래스 마우스 오른쪽 버튼 Run As &gt; JUnit Test를 눌러 테스트를 실행하면 테스트 결과가 출력 된다.</p>
<p>a + b = sum의 테스트 결과가 참으로 나온다.
<br /><br /></p>
<h3 id="테스트-결과가-거짓인-경우"><strong>테스트 결과가 거짓인 경우</strong></h3>
<pre><code class="language-java">public class JUnitTest {
    @DisplayName(&quot;1+2는 3&quot;)        // 테스트 이름
    @Test                        // 테스트 메소드
    public void junitTest() {
        int a = 1;
        int b = 2;
        int sum = 5;

        Assertions.assertEquals(sum, a + b);
    }
}</code></pre>
<p>위 코드에서 a + b = sum 의 결과는 false일 것이다. 
테스트 코드를 실행시켜보자.</p>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/65299aa3-a80c-4ff3-b164-39b682b9e6a5/image.png" /></p>
<p>Failures : 1로 테스트 결과가 거짓이다.</p>
<blockquote>
<ul>
<li>Failure :테스트의 기대값과 결과 값이 틀린 경우 발생한다.</li>
</ul>
</blockquote>
<ul>
<li>개발자가 기대값을 지정하고 그것과 다른 결과 값이 나올 경우 발생한다.<ul>
<li>Error: 테스트 수행 시 오류 발생, NullPointerException과 같은 RuntimeError일 경우 발생한다.</li>
<li>주로 xml 파일에 오타 등의 에러가 발생하면 Error가 발생한다.</li>
</ul>
</li>
</ul>
<p><br /><br /></p>
<p>코딩테스트 연습할 때 단위테스트를 사용해보는 중인데 바로바로 테스트해볼 수 있어서 편리한 것 같다.</p>
<pre><code class="language-java">package JunitTest;

import org.junit.jupiter.api.Assertions;
import org.junit.jupiter.api.Test;

public class JUnitTest {
    // 홀수번 째 원소들의 합과 짝수번 째 원소들의 합 중 큰 값 리턴
    @Test
    public void SolutionTest() {
        int even = 0, odd = 0;
        int[] num_list = {4, 2, 6, 1, 7, 6};
        for(int i = 0; i &lt; num_list.length; i++) {
            if(i % 2 != 0) {
                odd += num_list[i];
            }else {
                even += num_list[i];
            }
        }
        Assertions.assertTrue(odd &lt; even);
    }
}
</code></pre>
<p>만약 문제가 홀수번 째 원소들의 합과 짝수번 째 원소들의 합 중 큰 값을 리턴해야 한다면 코드를 작성하고 마지막에 <code>Assertions.assertTrue(odd &lt; even);</code> 와 같이 조건을 입력해서 테스트 해볼 수 있다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/9b3926e4-2325-4ff3-85a5-e312bea37293/image.png" /></p>
<p>홀수번 째 원소들의 합보다 짝수번 째 원소들의 합이 더 크다는 테스트 결과가 나왔다.</p>
<p><br /><br /></p>
<h4 id="마치며">마치며..</h4>
<p>단위테스트를 적용하니까 예상하지 못한 오류도 발견할 수 있고 여러가지 값을 넣어 테스트 하면서 빠르게 오류를 고칠 수 있어서 편리했다. 앞으로 코드를 작성할 때는 단위테스트도 작성하면서 더 안정성있는 코드를 작성할 수 있도록 해야겠다.</p>
<p><br /><br /><br /><br /><br /><br /></p>
<h4 id="참고한-글출처">참고한 글/출처</h4>
<p><a href="https://mangkyu.tistory.com/143">https://mangkyu.tistory.com/143</a>
<a href="https://velog.io/@suhyun_zip/JUnit%EC%9C%BC%EB%A1%9C-%EB%8B%A8%EC%9C%84-%ED%85%8C%EC%8A%A4%ED%8A%B8-%EC%BD%94%EB%93%9C-%EB%A7%8C%EB%93%A4%EA%B8%B0">https://velog.io/@suhyun_zip/JUnit으로-단위-테스트-코드-만들기</a>
<a href="https://sowon-dev.github.io/2020/10/14/201015spring-1/">https://sowon-dev.github.io/2020/10/14/201015spring-1/</a>
<a href="https://velog.io/@suran-kim/SpringBoot-JUnit%EC%9D%84-%EC%9D%B4%EC%9A%A9%ED%95%9C-%ED%85%8C%EC%8A%A4%ED%8A%B8-%EC%8B%A4%EC%8A%B5">https://velog.io/@suran-kim/SpringBoot-JUnit을-이용한-테스트-실습</a>
<a href="https://goddaehee.tistory.com/210">https://goddaehee.tistory.com/210</a>
<a href="https://sjh9708.tistory.com/195">https://sjh9708.tistory.com/195</a></p>