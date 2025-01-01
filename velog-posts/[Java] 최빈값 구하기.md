<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/27eb442e-7bc5-476f-9060-221fad0720cf/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/5319fd4f-65bc-4cec-ae46-b3c722f01a8b/image.png" /></p>
<p><br /><br /></p>
<h3 id="💭-나의-풀이오답">💭 나의 풀이(오답)</h3>
<pre><code class="language-java">class Solution {
    public int solution(int[] array) {
       int answer = 0, count = 0;
        for(int i = 0; i &lt; array.length; i++) {
            for(int j = 0; j &lt; array.length; j++) {
                if(array[i] == array[j])
                    count++;
            }
            if(answer &lt; count) {
                answer = array[i];    
            }else if(answer == count) {
                answer = -1;
            }
            count = 0;
        }

        return answer;
    }
}</code></pre>
<p>이중 <code>for</code>문을 돌리면서 <code>array[i]</code> 와 <code>array[j]</code>가 같다면 <code>count++</code>해서 갯수를 세고,
가장 큰 수가 <code>answer</code>에 저장되고, <code>answer</code>와 <code>count</code>가 같으면 <code>answer</code>에 -1을 대입했다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/18ff9513-b3a4-403c-907d-2d155c31a0a2/image.png" /></p>
<p>기본 TC에 4, 5, 6번 TC 반례를 추가했을 때 6개 모두 통과했지만 
채점했을 때는 16개 중 5개의 TC만 통과했다.</p>
<p><br /><br /><br /></p>
<h3 id="💡-해결-방법">💡 해결 방법</h3>
<p><code>HashMap</code>을 사용해서 간단하게 해결하는 기가막힌 답안을 찾았다.</p>
<pre><code class="language-java">import java.util.*;

    public static int solution(int[] array) {
        int answer = 0, maxCount = 0;

        Map&lt;Integer, Integer&gt; map = new HashMap&lt;&gt;();
        for(int num : array) {
            int count = map.getOrDefault(num, 0) + 1;
            if(count &gt; maxCount) {
                maxCount = count;
                answer = num;
            }else if(count == maxCount) {
                answer = -1;
            }
            map.put(num, count);
        }

        return answer;
    }
</code></pre>
<ul>
<li><p><code>map</code> 에 각 숫자가 배열에서 나타난 횟수를 저장한다.
<code>key</code>는 숫자, <code>value</code>는 그 숫자가 나타난 횟수이다.</p>
</li>
<li><p>반복문에서 배열의 각 숫자(<code>num</code>)에 대해 반복하면서,
<code>map.getOrDefault(num, 0)</code>을 사용하여 <code>num</code>이 이미 <code>map</code>에 있으면 가져오고 , 없으면 기본 값 0을 반환 한다.</p>
</li>
<li><p>가져온 값을 1 증가시켜서 <code>count</code>를 구하고 <code>count</code>가 <code>maxCount</code>보다 크면, <code>maxCount</code>값을 갱신하고 
<code>answer</code>에 해당 숫자(<code>num</code>)을 저장한다.</p>
</li>
<li><p>만약 <code>count</code>와 <code>maxCount</code>가 같으면 <code>answer</code>를 <code>-1</code>로 설정한다.</p>
</li>
<li><p>마지막으로 <code>map.put(num, count)</code>를 통해 해당 숫자의 빈도를 갱신한다.
<br /><br /><br /></p>
<hr />
<br />

</li>
</ul>
<h4 id="❗알게-된-것">❗알게 된 것</h4>
<blockquote>
<p><code>getOrDefault(Object key, V DefaultValue)</code> </p>
</blockquote>
<p>찾는 키가 존재할 경우 찾는 키의 값을 반환하고 없다면 기본 값을 반환하는 메서드이다.</p>
<p>** 매개변수 **</p>
<ul>
<li><strong>key</strong> : 값을 가져와야 하는 요소의 <strong>키</strong></li>
<li><strong>defaultValue</strong> : 지정된 키로 매핑된 값이 없는 경우 <strong>반환되어야 하는 기본 값</strong></li>
</ul>
<p><br /><br /><br /></p>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/18d6bebd-e23d-401e-98c6-1abcb468fd65/image.png" /></p>
<p><code>HashMap</code> <strong>쓸 생각을 왜 못했지?</strong> → <strong>익숙하지 않아서</strong> 인 것 같다.
문제 보면 어떤 자료형을 써야할지 툭 튀어나올 정도로 연습을 많이 해야할 것 같다.
나는 아직 갈길이 멀구나 ~~ 😶</p>