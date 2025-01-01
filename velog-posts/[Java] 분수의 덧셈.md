<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/29a4b256-30b4-44a9-ac34-9e839a36b149/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/db6b5c1e-f111-4721-8d2e-c2efc2ef5bdf/image.png" />
프로그래머스에 분수의 덧셈 문제가 있다.
이는 <strong>최소공배수(LCM; Least Common Multiple)</strong>, <strong>최대공약수(GCD;Greatest Common Divisor)</strong> 알고리즘을 알아야 해결할 수 있다.</p>
<p><br /><br /></p>
<h3 id="💡-분수의-덧셈-알고리즘">💡 분수의 덧셈 알고리즘</h3>
<blockquote>
<ol>
<li><strong>분모의 최소공배수(LCM)을 구한다</strong><ul>
<li>두 분수의 분모를 공통 분모로 맞추기 위해 최소 공배수를 계산한다.<ol start="2">
<li>** 분자를 공통 분모에 맞춘다 **</li>
</ol>
</li>
<li>각 분수의 분자를 공통 분모로 변환된 분모에 맞춰 재계산한다.</li>
</ul>
</li>
<li><strong>분자끼리 더한다</strong><ul>
<li>두 분수의 분자를 더하여 합계 분자를 구한다.</li>
</ul>
</li>
<li><strong>기약분수로 변환한다</strong><ul>
<li>결과 분수의 분자와 분모를 최대공약수(GCD)로 나눠 기약분수로 변환한다.</li>
</ul>
</li>
</ol>
</blockquote>
<p><br /><br /></p>
<h3 id="💡-최대-공약수gcd-구하는-알고리즘">💡 최대 공약수(GCD) 구하는 알고리즘</h3>
<p>최대공약수란 두 수가 서로 공통으로 가지고 있는 약수 중 가장 큰 수 이다.</p>
<h4 id="유클리드-호제법">유클리드 호제법</h4>
<p>유클리드 호제법(Euclidean Algorithm)은 두 정수의 <strong>최대공약수(GCD)</strong>를 구하는 효율적인 방법이다.
이 알고리즘은 나눗셈을 반복적으로 수행하여 나머지가 0이 될 때의 나누는 수를 최대공약수로 반환한다.
<br /></p>
<pre><code class="language-java">public class GCD{
    public static int gcd(int a, int b){
        while(b != 0){
            int temp = b;
            b = a % b;
            a = temp;
        }
        return a;
    }

    public static void main(String[] args){
        System.out.println(gcd(56, 42));    // 14
    }
}</code></pre>
<p><strong>💡 알고리즘 과정</strong></p>
<blockquote>
<ol>
<li><strong>반복문 <code>while(b != 0)</code></strong></li>
</ol>
</blockquote>
<ul>
<li>분모 <code>b</code>가 0이 아닐 때까지 반복한다. <ol start="2">
<li><strong>변수 <code>temp</code>에 현재 b의 값을 저장한다.</strong></li>
</ol>
</li>
<li>나머지를 계산하기 전에 현재 <code>b</code>의 값을 임시로 저장한다.<ol start="3">
<li><strong><code>b</code>를 <code>a % b</code>로 업데이트 한다.</strong></li>
</ol>
</li>
<li>나머지 계산 : <code>a % b</code></li>
<li>이 값이 새로운 b가 된다.<ol start="4">
<li><strong><code>a</code>를 <code>b</code>값으로 업데이트 한다.</strong></li>
</ol>
</li>
<li><code>temp</code>에 저장했던 <code>b</code> 값을 <code>a</code>로 설정한다.<ol start="5">
<li><strong><code>b</code>가 0이 되면 반복을 종료하고, 마지막 <code>a</code>값을 반환한다.</strong></li>
</ol>
</li>
</ul>
<p>만약 <code>gcd(int a, int b)</code>메서드에서 매개변수 <code>a</code>가 분자이고 <code>b</code>가 분모일 때 
<strong>두 수의 최대 공약수를 구해 기약분수</strong>를 만든다면 도출한 최대공약수로 <code>a</code>와 <code>b</code>에 각각 나누어 준다.</p>
<br />

<h3 id="💡-최소-공배수lcm-구하는-알고리즘">💡 최소 공배수(LCM) 구하는 알고리즘</h3>
<p>최소공배수란 두 정수의 공통 배수 중에서 가장 작은 양의 정수를 의미한다.</p>
<pre><code class="language-java">public class LCM {
    // 최대공약수(GCD)
    public static int gcd(int a, int b) {
        while (b != 0) {
            int temp = b;
            b = a % b;
            a = temp;
        }
        return a;
    }

    // 최소공배수(LCM)
    public static int lcm(int a, int b) {
        return (a * b) / gcd(a, b);
    }

    public static void main(String[] args) {
        System.out.println(lcm(12, 18)); // 출력: 36
    }
}</code></pre>
<p><strong>💡 알고리즘 과정</strong></p>
<blockquote>
<ol>
<li>두 정수 <code>a</code>와 <code>b</code>의 최대공약수를 계산한다.</li>
<li><code>a * b</code>를 계산한다.</li>
<li><code>(a * b) / gcd(a, b)</code>로 최소 공배수를 구한다.</li>
</ol>
</blockquote>
<br />