<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/1eed12ef-fd2b-4971-ac7d-062cc6a0b8fb/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/791c0f16-70c1-400b-8881-78ab30735bdd/image.png" />
어떠한 변수형을 다른 형으로 강제로 치환해야 할 경우 형변환을 사용한다.
변수형 타입이 맞지 않은 상태에서 계산하거나 리턴하는 경우 오류가 발생한다.
이번 글은 자바의 형변환에 대해서 정리를 해보려고 한다.
<br /><br /></p>
<h2 id="string-to-int">String to Int</h2>
<p>문자열에서 정수형으로 형변환 하는 방법은 두가지가 있다.</p>
<blockquote>
<p><strong>(1) Integer.parsInt(); **
&amp;nbsp&amp;nbsp&amp;nbsp&amp;nbsp→ 결과 값을 기본 자료형(Primitive Type)인 int로 반환한다.
**(2) Integer.valueOf();</strong>
&amp;nbsp&amp;nbsp&amp;nbsp&amp;nbsp→ 결과 값을 참조 자료형(Reference Type)인 Integer 객체로 만들어 반환한다.</p>
</blockquote>
<br />

<p>** String → Int 테스트 코드**</p>
<pre><code class="language-java">public class CastingTest {
    public String str_num = &quot;5&quot;;

    @Test
    @DisplayName(&quot;String to Int Casting&quot;)
    public void stringToInt() {
        int num_1 = Integer.parseInt(str_num);
        int num_2 = Integer.valueOf(str_num);

        Assertions.assertEquals(num_1+num_2, 10);
    }
}</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/ac8afe8f-5058-4167-8b08-37cef5692e0a/image.png" /></p>
<p>문자열을 정수형으로 변환한 후 계산이 잘 실행된 것을 확인할 수 있다.
<br /><br /><br /><br /></p>
<p>** 24년 12월 9일 내용 추가 **</p>
<h2 id="data의-크기가-큰-string-→-int형">Data의 크기가 큰 String → int형</h2>
<p>💀 String에서 정수형으로 형변환 시 <code>NumberFormatException.forInputString</code> 에러가 발생했다.
<img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/84836de7-f0c2-4bb5-a495-aea1210c366b/image.png" /></p>
<p><strong>int 타입은 -2,147,483,648 ~ 2,147,483,647</strong> 까지의 숫자를 표현할 수 있고,
<strong>Long 타입은 -9,223,372,036,854,775,808 ~ 9,223,372,036,854,775,807</strong> 까지 표현할 수 있다.
만약 <strong>Long보다 긴 경우는 BigInteger</strong>클래스를 이용해야한다.
자료형의 크기도 잘 확인해서 사용해야한다!</p>
<p>** String -&gt; bigInteger 테스트 예제 **</p>
<pre><code class="language-java">import java.math.BigInteger;

public class Test {
    public static void main(String[] args) {
        System.out.println(solution(&quot;18446744073709551615&quot;, &quot;287346502836570928366&quot;));
    }

    public static String solution(String a, String b) {
        BigInteger b1 = new BigInteger(a);
        BigInteger b2 = new BigInteger(b);
        return String.valueOf(b1.add(b2));
    }
}</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/5e8c4975-b5c6-4bf1-9dcf-86147fc9b0e5/image.png" />
<code>bigInteger</code> 로 계산이 올바르게 된 것을 확인할 수 있다.</p>
<p><br /><br /></p>
<h2 id="string-to-double-float">String to Double, Float</h2>
<blockquote>
<p><strong>(1) Double.valueOf();
(2) Float.valueOf();</strong></p>
</blockquote>
<br />

<p>** String → Double 테스트 코드 **</p>
<pre><code class="language-java">    public String str_num2 = &quot;1.6&quot;;

    @Test
    @DisplayName(&quot;String To Double Casting&quot;)
    public void stringToDouble() {
        double d_num = Double.valueOf(str_num2);
        System.out.println(d_num);

        Assertions.assertEquals(d_num , 1.6, 0.00002);
    }</code></pre>
<br />

<p>** String → float 테스트 코드 **</p>
<pre><code class="language-java">    public String str_num2 = &quot;1.6&quot;;

    @Test
    @DisplayName(&quot;String To Float Casting&quot;)
    public void stringToFloat() {
        float f_num = Float.valueOf(str_num2);
        System.out.println(f_num);

        Assertions.assertEquals(f_num , 1.6, 0.00002);
    }</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/31ffc24d-8c9c-4dba-954b-1e7e2e000e26/image.png" />
실수형 변수는 오차 범위가 있기 때문에 테스트 시 delta값을 준 뒤 테스트했다.
문자열을 실수형으로 변환이 잘 된 것을 확인할 수 있다.</p>
<p><br /><br /></p>
<h2 id="int-to-string">Int to String</h2>
<p>정수형에서 문자열로 변환하는 방법은 두가지가 있다.</p>
<blockquote>
<p><strong>(1) String.valueOf();</strong>
&amp;nbsp&amp;nbsp&amp;nbsp&amp;nbsp→ String 클래스 내부에 있는 메서드이며, 매개변수를 받아서 문자열로 반환한다.
<strong>(2) Integer.toString();</strong>
&amp;nbsp&amp;nbsp&amp;nbsp&amp;nbsp→ Integer 클래스 내부에 있는 메서드이며 int 타입의 정수를 매개변수로 받아서 문자열로 반환한다.</p>
</blockquote>
<p>위 메서드들은 변환하는 정수 타입이 <code>int(Primitive type)</code>인지 <code>Integer(Wrapper class)</code>인지에 따라 차이가 발생한다.</p>
<p>String클래스의 <code>valueOf()</code>메서드 자체가 <code>Integer.toString()</code>메서드를 사용하고 있기 때문에
<strong>매개변수에 int를 사용할 때 두 메서드는 동일하게 동작</strong>한다.</p>
<br />

<h3 id="💡-wrapper-class인-integer의-값이-null일-경우"><strong>💡 Wrapper class인 Integer의 값이 null일 경우</strong></h3>
<p><code>String.valueOf()</code>의 경우에는 값이 잘 나오지만,
<code>Integer.toString()</code> 메서드에서 <code>NullPointerException</code>을 던진다.</p>
<pre><code class="language-java">public class Test {
    public static void main(String[] args) {
        Integer integer = null;

        System.out.println(String.valueOf(integer));
        System.out.println(Integer.toString(integer));
    }
}</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/96e14865-3341-4eb8-9b1c-67b1c4bf92c0/image.png" /></p>
<br />

<p>** Int → String 테스트 코드 **</p>
<pre><code class="language-java">    public int num = 3;

    @Test
    @DisplayName(&quot;Int To String Casting&quot;)
    public void intToString() {
        String str_1 = String.valueOf(num);
        String str_2 = Integer.toString(num);

        Assertions.assertEquals(str_1, str_2);
    }</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/9c3da3e2-80ae-465e-afbe-b0220ac59510/image.png" />
정수형이 문자열로 변환이 잘 된 것을 확인할 수 있다.</p>
<p><br /><br /></p>
<h2 id="double-float-to-string">Double Float to String</h2>
<p>정수형과 마찬가지로 <code>toString()</code>, <code>String.valueOf()</code> 함수로 치환할 수 있다.
<br /></p>
<p>** float, double → String 테스트 코드 **</p>
<pre><code class="language-java">    public void castingToString() {
        double d_num = 15.15;
        float f_num = 15.15f;
        String s_num = &quot;&quot;;

        // double
        s_num = String.valueOf(d_num);
        s_num = Double.toString(d_num);

        // float
        s_num = String.valueOf(f_num);
        s_num = Float.toString(f_num);
    }</code></pre>
<h2 id="double-float-to-int">Double, Float to Int</h2>
<p>실수를 정수로 치환하는 방법은 <code>(int)</code> 캐스팅 방식으로 변환할 수 있다.
이 때** 소수점 아래는 버려진다.**
<br /></p>
<p>** float, double → int 테스트 코드 **</p>
<pre><code class="language-java">    public double d_num = 10.14;
    public float f_num = 10.33f;

    @Test
    @DisplayName(&quot;Casting to Int&quot;)
    public void castingToInt() {
        int i_num = (int)d_num;
        int i_num2 = (int)f_num;

        Assertions.assertEquals(i_num, i_num2);
    }</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/2b6b7655-b9ac-42ca-a950-abe181eaf3b5/image.png" /></p>
<h2 id="int-to-double-float">Int to Double, Float</h2>
<p>정수형을 실수형으로 변경하는 방법은 마찬가지로 <code>(double)</code>, <code>(float)</code> 로 변환할 수 있다.
<br /></p>
<p>** int → double 테스트 코드 **</p>
<pre><code class="language-java">    public int i_num = 3;

    @Test
    @DisplayName(&quot;Casting to Double&quot;)
    public void castingToDouble() {
        double d_num = (double)i_num;
        System.out.println(d_num);
    }</code></pre>
<p><br /><br />
** int → float 테스트 코드 **</p>
<pre><code class="language-java">    @Test
    @DisplayName(&quot;Casting to Float&quot;)
    public void castingToFloat() {
        float f_num = (float)i_num;
        System.out.println(f_num);
    }</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/3a60943d-6cd7-40d1-97e4-7c7ae4b4adab/image.png" />
<code>int</code>형 변수 <code>i_num</code>이 <code>double</code>, <code>float</code>형으로 변환 되어서 3.0으로 출력되는 것을 확인할 수 있다. 
출력 결과는 같다.</p>
<p><br /><br /><br /></p>
<p>** 출처/참고한글 **
<a href="https://stackoverflow.com/questions/7554281/junit-assertions-make-the-assertion-between-floats">JUnit assertions : make the assertion between floats</a></p>