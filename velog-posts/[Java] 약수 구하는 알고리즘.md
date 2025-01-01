<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/47b27161-0b22-4750-8185-274247db89db/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/04637ab5-0017-476c-afc3-cdbeef337621/image.png" /></p>
<p>약수란 인수를 나누어 떨어지게 하는 수를 의미한다.
예를 들어 12의 약수는 1, 2, 3, 4, 6, 12 이다.
<br /></p>
<h2 id="💡-약수-구하는-알고리즘">💡 약수 구하는 알고리즘</h2>
<p>약수를 구하기 위해서는 다음 단계를 따른다.</p>
<blockquote>
<ol>
<li>1부터 주어진 수 <code>n</code>까지 반복문을 돌린다.</li>
<li><code>n</code>을 <code>i</code>로 나누었을 때 나머지가 0이면, <code>i</code>는 <code>n</code>의 약수이다.</li>
</ol>
</blockquote>
<br />

<h3 id="단순-반복문을-이용한-방법">단순 반복문을 이용한 방법</h3>
<p>시간 복잡도는 O(n)이다.</p>
<pre><code class="language-java">int number = 20;
for(int i = 1; i &lt;= number; i++){
    if(number % i == 0){
        System.out.print(i + &quot; &quot;);  // 1 2 4 5 10 20 
        }
    }</code></pre>
<p>20의 약수를 구한다고 했을 때 <code>number</code>를 <code>i</code>로 나누었을 때 나머지가 0일 경우 약수가 출력 된다.</p>
<br />

<h3 id="제곱근을-이용한-방법">제곱근을 이용한 방법</h3>
<p>모든 약수를 확인할 필요 없이, 숫자의 <strong>제곱근</strong>까지만 확인해도 된다.
시간 복잡도를 O(√n)으로 줄일 수 있다.</p>
<pre><code class="language-java">        int number = 20;
        List&lt;Integer&gt; divisors = new ArrayList&lt;&gt;();

        for(int i = 1; i * i &lt;= number; i++){
            if(number % i == 0){
                divisors.add(i);
                if(i != number / i){
                    divisors.add(number / i);
                }
            }
        }
        divisors.sort(Integer::compareTo);
        for(int div: divisors){
            System.out.print(div + &quot; &quot;);    // 1 2 4 5 10 20 
        }</code></pre>
<p><code>number % i == 0</code> : <code>number</code>를 <code>i</code>로 나눌 때 나머지가 0이면 <code>i</code>는 약수이다.
<code>divisiors.add(i)</code>: 작은 약수 <code>i</code>를 리스트에 추가한다.
<code>if (i != number / i)</code> :</p>
<ul>
<li><code>number / i</code>는 큰 약수를 의미한다.</li>
<li><code>i</code>와 <code>number / i</code>가 같지 않을 때만 추가한다. 
예를 들어 16의 경우 (4, 4)와 같은 중복 방지.</li>
</ul>
<p><br /><br /></p>
<table border="1" cellpadding="10" cellspacing="0">
    <thead>
        <tr>
            <th>방법</th>
            <th>시간 복잡도</th>
            <th>특징</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>단순 반복문 이용</td>
            <td>O(n)</td>
            <td>코드가 단순하고 이해하기 쉬움</td>
        </tr>
        <tr>
            <td>제곱근 활용</td>
            <td>O(√n)</td>
            <td>큰 숫자에 대해 더 효율적</td>
        </tr>
    </tbody>
</table>

<p><br /><br /></p>
<p>약수 구하기는 알고리즘 문제에서 자주 등장하는 주제이므로 알아두는 것이 좋다.</p>
<h3 id="내-풀이">내 풀이</h3>
<pre><code class="language-java">class Solution {
    public int solution(int n) {
        int answer = 0;
        for(int i = 1; i &lt;= n; i++){
            if(n % i == 0){
                answer ++;
            }
        }
        return answer;
    }
}</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/621fb36c-1b23-4bb5-b5f8-8eb919908e8d/image.png" /></p>