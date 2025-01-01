<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/12348a67-a836-45d1-9f68-e614d9976840/image.png" /></p>
<br />

<p>요즘 매일 코딩테스트 입문 문제를 쭈욱 풀어나가고 있는데, 풀면서 <strong>기초가 정말 중요</strong>하다고 느낀다.
머리로는 이거 이렇게 해야지~ 라고 생각이 드는데 막상 키보드 앞에 서면 '<em>그거 어떻게 하더라..?</em>' 한다.
블로그도 열심히 써보기로 했으니 블로그에 정리하면서 다시 한번 상기 시켜야겠다.
<br /></p>
<hr />
<br />


<h2 id="1-💡-arrayssort">1. 💡 Arrays.sort()</h2>
<p>자바에서는 배열을 정렬할 때 <code>java.util.Arrays</code> 클래스에 포함 된 정렬 알고리즘 <code>sort()</code>를 메서드로 제공 한다.
<code>sort()</code> 메서드를 사용하면 정렬을 간단하게 구현할 수 있다.</p>
<br />

<h3 id="1-1-기본형primitive-type-배열-정렬">1-1. 기본형(Primitive Type) 배열 정렬</h3>
<p><code>Arrays.sort()</code> 는 기본 오름차순으로 정렬한다.
<br /></p>
<p><strong>오름차순 정렬</strong></p>
<pre><code class="language-java">import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        int[] numbers = {5, 2, 9, 1, 5, 6};
        Arrays.sort(numbers);
        System.out.println(Arrays.toString(numbers)); // [1, 2, 5, 5, 6, 9]
    }
}</code></pre>
<p>기본형 배열은  <code>Arrays.sort()</code>로 간단하게 오름차순 정렬할 수 있다.
<code>Arrays.sort()</code> 자체는 <strong>기본적으로 오름차순 정렬</strong>만 지원하지만, <strong>내림차순 정렬</strong>도 구현할 수 있다.</p>
<br />

<p><strong>내림차순 정렬</strong>
예) 기본형 <code>int</code>배열은 <code>Arrays.sort()</code>와 함께 <code>Integer</code>클래스를 활용하면 된다.</p>
<pre><code class="language-java">import java.util.Arrays;
import java.util.Collections;

public class Main {
    public static void main(String[] args) {
        Integer[] numbers = {5, 2, 9, 1, 5, 6}; // int[] 대신 Integer[]
        Arrays.sort(numbers, Collections.reverseOrder());
        System.out.println(Arrays.toString(numbers)); // [9, 6, 5, 5, 2, 1]
    }
}</code></pre>
<p>기본형 배열은 <code>Collections.reverseOrder()</code>를 사용할 수 없기 때문에 <code>Integer[]</code>로 사용했다.</p>
<br />

<h3 id="1-2-객체reference-type-배열-정렬">1-2. 객체(Reference Type) 배열 정렬</h3>
<p>객체 배열은 참조형 데이터 타입인 객체의 주소를 저장하는 배열이다.
기본형 배열 정렬과 마찬가지로 <code>Arrays.sort()</code>를 사용하여 정렬할 수 있지만, 
객체는 <code>Comparable</code> 인터페이스를 구현해야 한다.</p>
<p><code>Arrays.sort()</code> 메서드를 사용해 객체 배열을 정렬하려면, <strong>정렬의 기준</strong>을 Java가 알아야 한다.
이 기준을 제공하기 위해 객체 클래스에서 <code>Comparable</code>인터페이스를 구현해야 한다.
<br /></p>
<p><strong>나이를 기준으로 오름차순 정렬 하기</strong></p>
<pre><code class="language-java">import java.util.Arrays;

class Person implements Comparable&lt;Person&gt; {
    String name;
    int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public int compareTo(Person other) {
        return this.age - other.age; // 나이 기준 오름차순
    }

    @Override
    public String toString() {
        return name + &quot;(&quot; + age + &quot;)&quot;;
    }
}

public class Main {
    public static void main(String[] args) {
        Person[] people = {
            new Person(&quot;Alice&quot;, 30),
            new Person(&quot;Bob&quot;, 25),
            new Person(&quot;Charlie&quot;, 35)
        };

        Arrays.sort(people);
        System.out.println(Arrays.toString(people)); // [Bob(25), Alice(30), Charlie(35)]
    }
}</code></pre>
<p>자바의 <code>Comparable</code> 인터페이스는 <code>compareTo()</code> 메서드를 통해 객체 간의 순서를 비교할 수 있도록 해준다. </p>
<p><code>Person</code>클래스에 나이를 기준으로 정렬한다고 했을 때,
<code>this.age - other.age</code>는 <strong>오름차순</strong>을 의미한다.</p>
<p>결과가 음수면 <code>this</code>가 <code>other</code>보다 앞에 온다는 의미이고,
결과가 양수이면 <code>this</code>가 <code>other</code>보다 뒤에 온다는 의미이다.</p>
<br />



<br />

<p>** 나이를 기준으로 내림차순 정렬하기 **</p>
<p>객체 배열 또한 내림차순으로 정렬이 가능한데, 
객체 배열은 <code>Comparator</code>을 사용해서 내림차순으로 정렬할 수 있다.</p>
<pre><code class="language-java">Arrays.sort(배열, Comparator);</code></pre>
<p>두번 째 인자인 <code>Comparator</code>는 정렬 기준을 제공하는 함수이다.</p>
<pre><code class="language-java">import java.util.Arrays;

class Person {
    String name;
    int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public String toString() {
        return name + &quot;(&quot; + age + &quot;)&quot;;
    }
}

public class Main {
    public static void main(String[] args) {
        Person[] people = {
            new Person(&quot;Alice&quot;, 30),
            new Person(&quot;Bob&quot;, 25),
            new Person(&quot;Charlie&quot;, 35)
        };

        // 나이 기준 내림차순 정렬
        Arrays.sort(people, (p1, p2) -&gt; p2.age - p1.age);

        System.out.println(Arrays.toString(people)); // [Charlie(35), Alice(30), Bob(25)]
    }
}</code></pre>
<p><strong>람다식</strong>을 사용해서 객체 배열을 <strong>내림차순 정렬</strong> 했다.
<code>Comparator</code>를 간단하게 <strong>람다식</strong>으로 표현한 것인데,
<code>p1</code>과 <code>p2</code>는 <code>Person</code>객체를 의미하고, <code>p2.age - p1.age</code>는 <strong>나이 기준 내림차순 정렬</strong>을 뜻한다.</p>
<p><code>Arrays.sort()</code>는 <strong>람다식</strong>을 기준으로 <code>people</code>배열을 정렬한다.
<code>p2.age</code> - <code>p1.age</code> 덕분에 <strong>나이가 많은 순서</strong>로 정렬 된다.</p>
<br />

<h2 id="💡-2-stream-api-정렬-구현">💡 2. Stream API 정렬 구현</h2>
<p><code>Stream API</code>는 Java8에서 도입된 기능으로 <code>Collection</code>(<code>List</code>, <code>Set</code>)이나 배열 같은 데이터 소스를 처리하고 변환하는데 사용된다.</p>
<p><code>Stream API</code>를 사용했을때 장점은 코드가 간결해지고, 데이터 변경 없이 새로운 결과를 사용할 수 있다.</p>
<h3 id="2-1-이름을-기준으로-오름차순-정렬">2-1. 이름을 기준으로 오름차순 정렬</h3>
<pre><code class="language-java">import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        String[] names = {&quot;Charlie&quot;, &quot;Alice&quot;, &quot;Bob&quot;};

        String[] sortedNames = Arrays.stream(names)
                                     .sorted()
                                     .toArray(String[]::new);

        System.out.println(Arrays.toString(sortedNames)); // [Alice, Bob, Charlie]
    }
}</code></pre>
<p><code>sorted()</code>를 사용하면 오름차순으로 정렬한다.</p>
<br />

<h3 id="2-2-이름을-기준으로-내림차순-정렬">2-2. 이름을 기준으로 내림차순 정렬</h3>
<pre><code class="language-java">import java.util.Arrays;
import java.util.Comparator;

public class Main {
    public static void main(String[] args) {
        String[] names = {&quot;Charlie&quot;, &quot;Alice&quot;, &quot;Bob&quot;};

        String[] sortedNames = Arrays.stream(names)
                                     .sorted(Comparator.reverseOrder())
                                     .toArray(String[]::new);

        System.out.println(Arrays.toString(sortedNames)); // [Charlie, Bob, Alice]
    }
}</code></pre>
<p><code>Comparator.reverseOrder()</code>를 사용하여 내림차순 정렬도 가능하다.</p>
<p>하지만 <code>Comparator.reverseOrder()</code>는 <strong>객체 타입에서만 사용</strong>할 수 있기 때문에 
<strong>기본형 배열에서는 사용할 수 없다</strong>.</p>
<br />

<h2 id="💡-3-정렬-알고리즘-직접-구현">💡 3. 정렬 알고리즘 직접 구현</h2>
<p>사실 알고리즘 공부할 때는 직접 구현해보는 것이 제일 좋다고 생각한다. </p>
<h3 id="1-버블-정렬bubble-sort">1. 버블 정렬(Bubble Sort)</h3>
<p>버블 정렬(Bubble Sort)은 <strong>인접한 두 요소를 비교해 교환하면서 정렬</strong>하는 단순한 정렬 알고리즘이다.</p>
<p>이름처럼 배열의 요소가 거품처럼 뽀글뽀글 위로 올라오듯이 
<strong>가장 큰 값이 반복적으로 배열의 끝으로</strong> 이동하며 정렬 된다.</p>
<pre><code class="language-java">public class Main {
    public static void main(String[] args) {
        int[] numbers = {5, 2, 9, 1, 5, 6};
        bubbleSort(numbers);
        System.out.println(Arrays.toString(numbers)); // [1, 2, 5, 5, 6, 9]
    }

    public static void bubbleSort(int[] array) {
        int n = array.length;
        for (int i = 0; i &lt; n - 1; i++) {
            for (int j = 0; j &lt; n - 1 - i; j++) {
                if (array[j] &gt; array[j + 1]) {
                    // Swap
                    int temp = array[j];
                    array[j] = array[j + 1];
                    array[j + 1] = temp;
                }
            }
        }
    }
}</code></pre>
<p>*<em>버블정렬 동작 방식 *</em></p>
<blockquote>
<ol>
<li>배열의 처음부터 끝까지 인접한 두 요소를 비교한다.</li>
<li>만약 두 요소의 순서가 맞지 않으면 두 요소의 위치를 교환(swap) 한다.</li>
<li>위 과정을 배열 크기만큼 반복한다.</li>
<li>각 반복(iteration)마다 큰 값이 맨 뒤로 정렬되므로, 다음 반복에서는 마지막 요소를 제외하고 작업한다.</li>
</ol>
</blockquote>
<p>버블 정렬은 구현이 쉽지만 데이터가 클 경우 성능이 좋지 않기 때문에 실무에서는 <strong>퀵정렬(Quick Sort)</strong>나 <strong>병합 정렬(Merge Sort)</strong>같은 더 효율적인 알고리즘을 사용하는 것이 일반적이다.</p>
<br />
<br />