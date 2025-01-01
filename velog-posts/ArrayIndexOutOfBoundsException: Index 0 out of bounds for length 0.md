<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/c1f385ed-1e30-42a7-9670-009225164b88/image.png" /></p>
<h3 id="에러-발생">에러 발생</h3>
<blockquote>
<p>Exception in thread &quot;main&quot; java.lang.ArrayIndexOutOfBoundsException: Index 0 out of bounds for length 0</p>
</blockquote>
<p>프로그래머스 문제를 풀다가 별로 작성한 것도 없는 코드에 오류가 발생했다!?
<br /><br /></p>
<h3 id="코드">코드</h3>
<pre><code class="language-java">public static int[] solution(int[] num_list) {
        int[] answer = {};
        for(int i = 0; i &lt; num_list.length; i++) {
            answer[i] = num_list[i];
        }

        return answer;
    } </code></pre>
<p>위 코드를 main에서 실행하면 위와 같은 에러가 발생한다.
이 에러는 <strong>인덱스가 배열의 크기보다 크거나 음수가 나오면 발생시키는 예외</strong>이다.
다시 보니 배열 선언도 안하고 값을 대입했다. </p>
<p>어처구니없는 실수..</p>
<p><br /><br /></p>
<h3 id="수정된-코드">수정된 코드</h3>
<pre><code class="language-java">     public static int[] solution(int[] num_list) {
        int[] answer = new int[7];
        for(int i = 0; i &lt; num_list.length; i++) {
            answer[i] = num_list[i];
        }

        return answer;
    }</code></pre>
<p><br /><br />
배열의 크기를 지정해주면 정상적으로 실행된다.
이런 실수는 다시는 하지말자....!</p>