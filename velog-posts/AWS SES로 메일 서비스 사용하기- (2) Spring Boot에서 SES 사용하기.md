<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/51acff48-677b-426b-81e6-f52dd6700cf2/image.png" /></p>
<p>지난 게시글에서는 AWS SES 계정을 만들고 이메일 설정까지 했다.
이번에는 AWS SES를 사용하여 이메일을 직접 보내보자.
<br /></p>
<h2 id="💡-spring-boot에서-aws-ses-사용하기">💡 Spring Boot에서 AWS SES 사용하기</h2>
<h3 id="1-maven-설정">1. Maven 설정</h3>
<p>현재 내 프로젝트에서는 Maven을 사용하므로 <code>pom.xml</code> 을 설정해주어야 한다.</p>
<pre><code class="language-xml">&lt;dependency&gt;
    &lt;groupId&gt;com.amazonaws&lt;/groupId&gt;
    &lt;artifactId&gt;aws-java-sdk-ses&lt;/artifactId&gt;
    &lt;version&gt;1.12.30&lt;/version&gt;
&lt;/dependency&gt;

&lt;dependency&gt;
    &lt;groupId&gt;org.springframework.boot&lt;/groupId&gt;
    &lt;artifactId&gt;spring-boot-starter-mail&lt;/artifactId&gt;
&lt;/dependency&gt;</code></pre>
<p><code>spring-boot-starter-mail</code> 과 <code>ses</code> dependency를 추가 한다.</p>
<br />


<h3 id="2-액세스-키-발급-받기">2. 액세스 키 발급 받기</h3>
<p>SES를 사용하려면 Spring Boot의 라이브러리가 SES에 접근할 수 있도록 액세스 키를 발급 받아야 한다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/67acdf56-c2f2-44fc-970d-5996ec973c69/image.png" />
우측 상단의 내 계정 선택 후 보안 자격 증명 탭에서 <strong>액세스 키</strong>를 발급받는다. 
액세스 키는 AWS 리소스에 접근하기 위해 사용하는 자격증명이다.
<br /></p>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/32ba31b7-161e-4a89-80a9-fc997479a233/image.png" />
액세스 키를 생성하려고 하니 경고 문구가 나타났다.
<strong>루트 사용자는 AWS 계정을 처음 만들 때 생성되는 AWS 계정의 전체 권한을 가진 사용자</strong>이다.
만약 이런 경고창이 떴다면 바로 액세스 발급 받지 말고 <strong>IAM(Identity and Management)</strong> 사용자를 만들어서 엑세스 키를 발급 받는 것을 권장한다.
<br /></p>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/be3b5d06-1e13-473b-b85b-7c20cb6953cf/image.png" />
AWS SES를 사용할 것이므로 IAM에 <code>AmazonSESFullAccess</code> 권한을 추가해야 한다.</p>
<p>액세스 키를 발급 받았다면 <strong>Secret access key는 CSV를 저장해두거나 따로 메모해서 기억해둬야 한다.</strong>
액세스 키의 ID는 확인할 수 있지만 Secret access key는 확인할 수 없다.</p>
<br />


<h3 id="3-applicationyml-설정">3. application.yml 설정</h3>
<p>발급 받은 access key는 <code>application.yml</code>에 등록한다.</p>
<p><code>application.properties</code> 나 <code>application.yml</code>의 기본 구조는 비슷하지만 중복되는 코드가 줄어들기 때문에 yml을 사용 했다.</p>
<pre><code class="language-yml">aws:
  ses:
    access-key: {key}
    secret-key: {key}
    send-mail-to: {mail}
  region: ap-northeast-2</code></pre>
<br />


<h3 id="4-aws-ses-설정-파일-생성">4. AWS SES 설정 파일 생성</h3>
<p>AWS SES와 관련한 설정 파일을 Bean으로 등록한다.</p>
<blockquote>
<ul>
<li><code>@Value</code>를 사용하여 <code>application.yml</code>에 등록한 값을 주입 받는다.</li>
</ul>
</blockquote>
<ul>
<li><code>amazonSimpleEmailService()</code> : AWS SES 클라이언트를 <code>Bean</code>으로 생성한다.<ul>
<li><code>BasicAwsCredemcials()</code> : <code>access-key</code>, <code>secret-key</code>를 사용하여 자격 증명을 설정 한다.</li>
<li><code>AWSStaticCredentialsProvider</code> : 정적 자격 증명을 생성한다. 
AWS 서비스에 대한 요청을 인증하는데 필요하다.</li>
<li><em>Application이 시작될 때 한 번만 설정되며, 실행 도중에 변경되지 않는다.*</em></li>
</ul>
</li>
</ul>
<p>설정을 마치면 AWS SES 클라이언트를 생성하여 <code>Bean</code>에 등록된다.</p>
<pre><code class="language-java">@Configuration
public class AwsConfig {
    @Value(&quot;${aws.ses.access-key}&quot;)
    private String accessKey;
    @Value(&quot;${aws.ses.secret-key}&quot;)
    private String secretKey;
    @Value(&quot;${aws.region}&quot;)
    private String region;

    @Bean
    AmazonSimpleEmailService amazonSimpleEmailService() {
        BasicAWSCredentials basicAWSCredentials = new BasicAWSCredentials(accessKey, secretKey);
        AWSStaticCredentialsProvider awsStaticCredentialsProvider = new AWSStaticCredentialsProvider(basicAWSCredentials);

        return AmazonSimpleEmailServiceClientBuilder.standard()
                .withCredentials(awsStaticCredentialsProvider)
                .withRegion(region)
                .build();
    }
}</code></pre>
<br />

<h3 id="5-이메일-전송-dto-생성">5. 이메일 전송 DTO 생성</h3>
<p>이메일 정보를 담은 DTO를 생성한다.</p>
<blockquote>
<ul>
<li><code>Destionation</code> : 수신자의 이메일 주소를 설정한다.</li>
</ul>
</blockquote>
<ul>
<li><code>Message</code> : 이메일의 제목과 본문을 설정한다.</li>
</ul>
<pre><code class="language-java">@Getter
@AllArgsConstructor
@NoArgsConstructor
public class EmailDTO {
    static final String FROM_EMAIL =&quot;mouse97_@naver.com&quot;;    // 보낸 사람 이메일
    private List&lt;String&gt; receivers;    // 받는 사람
    private String subject; // 제목
    private String content; // 내용

    // SendEmailRequest 객체 형태로 맞춰 준다.
    public SendEmailRequest toSendRequestDto() {
        // 목적지 설정
        Destination destination = new Destination().withToAddresses(this.receivers);
        // 제목, 본문 설정
        Message message = new Message().withSubject(createContent(this.subject))
                          .withBody(new Body().withHtml(createContent(this.content)));
        return new SendEmailRequest().withSource(FROM_EMAIL).withDestination(destination).withMessage(message);
    }

    // 본문 형식 설정
    private Content createContent(String text) {
        return new Content().withCharset(&quot;UTF-8&quot;).withData(text);
    }
}</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/d83606bf-6351-481d-8c64-03407454d5cb/image.png" /></p>
<p><code>FROM_EMAIL</code>은 SES에서 등록한 이메일로 지정한다.
그리고 AWS에서는 <a href="https://docs.aws.amazon.com/AWSJavaSDK/latest/javadoc/com/amazonaws/services/simpleemail/model/SendEmailRequest.html">SendEmailRequest</a> 타입으로 메일을 보내기 때문에 미리 세팅해주는 메서드를 만들었다.
<br /></p>
<h3 id="6-service비즈니스-로직-로직">6. Service(비즈니스 로직) 로직</h3>
<blockquote>
<p><code>@RequiredArgsConstructor</code> :  스프링에서 의존성 주입 방법 중에 생성자 주입을 임의의 코드 없이 자동으로 설정해주는 어노테이션</p>
</blockquote>
<pre><code class="language-java">@Service
@RequiredArgsConstructor 
@Slf4j
public class EmailService {
    private final AmazonSimpleEmailService amazonSimpleEmailService;

    // 이메일 전송하기
    public void sendMail(String subject, String content, List&lt;String&gt; receivers) {
        // 이메일 정보를 담은 객체
        EmailDTO emailDto = new EmailDTO(receivers, subject,content);
        // EmailDTO를 SendEmailResult 형태로 바꿔준 뒤 이메일 전송
        SendEmailResult sendEmailResult = amazonSimpleEmailService.sendEmail(emailDto.toSendRequestDto());

        //메일이 정상적으로 전송된 경우 200 OK를 반환한다.
        if(sendEmailResult.getSdkHttpMetadata().getHttpStatusCode() == 200) {
            log.info(&quot;Email을 발송했습니다!&quot;);
        }else {
            log.info(&quot;Email 발송에 실패했습니다.&quot;);
        }
    }
}</code></pre>
<p>이메일 전송을 위한 비즈니스 로직을 작성 한다.
메일이 정상적으로 발송되는 경우 <code>200</code>을 반환하므로 발송 여부에 따른 로그를 확인할 수 있다.</p>
<br />

<h3 id="7-controller">7. Controller</h3>
<pre><code class="language-java">@Controller
public class EmailController {
    @Autowired
    private EmailService emailService;

    @Autowired
    private UserService userService;

    // 이메일 전송 API
    @GetMapping(&quot;/api/sendEmail&quot;)
    public String sendEmail() {
        List&lt;UserVO&gt; users = userService.selectByUsers();
        List&lt;String&gt; receivers = new ArrayList&lt;&gt;();
        for(int i = 0; i &lt; users.size(); i++) {
            receivers.add(users.get(i).getEmail());
        }
        String subject = &quot;AWS SES 전송 테스트 &quot;;
        String content = &quot;이메일 전송 테스트입니다.&lt;hr&gt;&quot;;
        emailService.sendMail(subject, content, receivers);
        return &quot;true&quot;;
    }
}</code></pre>
<p> 받는 사람은 뉴스레터를 구독한 구독자들에게 보내므로 구독자 DB에서 리스트를 받아와서 대입한다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/e8e5f899-4758-4bc2-b6d2-2d5e68a835ac/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/yeonhee314/post/b74de496-f30b-4448-b130-c11dc4616ec8/image.png" /></p>
<p>이메일 발송이 정상적으로 완료 되었기 때문에 로그도 잘 나오고 태그도 적용된 것을 확인할 수 있었다. 
메일 발송 테스트가 완료 되었기 때문에 이제 뉴스 기사 파싱 작업을 진행해야겠다.
 <img src="https://velog.velcdn.com/images/yeonhee314/post/1a15001d-528f-4e09-bad6-d5f829232a40/image.png" width="150px" /></p>
<p>근데 이메일 주소를 naver로 했더니 스팸 의심 경고 문구가 뜨는게 별로 보기 좋지 않아서 
gmail로 바꾸는 것도 고려해봐야겠다...!</p>
<p><br /><br /><br /></p>
<hr />
<p>개인적으로 공부하며 작성하는 게시물입니다.
혹시 잘못된 정보가 있거나, 질문은 편하게 댓글 달아주세요.
감사합니다😊<br /><br /></p>
<p><strong>출처/참고한 글</strong>
<a href="https://velog.io/@korea3611/aws-ses-%EB%A5%BC-%EC%82%AC%EC%9A%A9%ED%95%98%EC%97%AC-%EB%A9%94%EC%9D%BC%EC%9D%84-%EB%B3%B4%EB%82%B4%EB%B3%B4%EC%9E%90">[Spring Boot] AWS SES를 사용하여 메일을 보내보자</a>
<a href="https://jhlee-developer.tistory.com/entry/AWS-AWS-CLI-%EC%84%A4%EC%B9%98-%EB%B0%8F-V2-%EC%97%85%EB%8D%B0%EC%9D%B4%ED%8A%B8">[AWS] IAM 사용자 생성하는법 - 액세스 키 발급</a>
<a href="https://server-technology.tistory.com/303">[Spring]AWS SES를 사용하여 메일을 보내기</a>
<a href="https://hyunki99.tistory.com/94">[AWS] AWS Access Key란? (엑세스 키 생성 방법)</a>
<a href="https://curiousjinan.tistory.com/entry/spring-boot-yml-vs-properties">[Spring] yml vs properties 설정파일 비교</a>
<a href="https://hesh1232.tistory.com/156">Maven과 Gradle 차이 및 프로젝트 설정</a>
<a href="https://docs.aws.amazon.com/ko_kr/sdk-for-java/v1/developer-guide/setup-project-maven.html">Apache Maven으로 SDK 사용하기</a>
<a href="https://velog.io/@rainbowweb/AWS-SES%EB%A1%9C-%EC%9D%B4%EB%A9%94%EC%9D%BC-%EB%B3%B4%EB%82%B4%EA%B8%B0-%EC%98%88%EC%A0%9C">AWS SES로 이메일 보내기 예제</a></p>