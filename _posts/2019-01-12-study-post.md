---
title: "스프링부트에 부트스트랩 적용시 경로 설정"
date: 2019-01-12 08:26:28 -0400
categories: jekyll test hohoho
---


스프링부트에 부트스트랩을 적용하기 위해서 기존에 제공된 index 페이지로 테스트 중이었는데
@RequestMapping에서 입력되는 경로가 /index2 이냐 /study/index2이냐에 따라
부트스트랩이 적용됐다 안됐다 하는 문제를 겪었다<br/><br/><br/>

-결론
  
    @RequestMapping("/index2")
    public String list2() {
      return "study/index2";
    }
    <!-- Custom styles for this template -->
    <link href="css/clean-blog.min.css" rel="stylesheet">
<br/>

    @RequestMapping("/study/index2")
    public String list2() {
      return "study/index2";
    }
    <!-- Custom styles for this template -->
    <link href="/css/clean-blog.min.css" rel="stylesheet">


http://localhost:8080/<B>index</B> 인 경우, 정적 파일의 경로 앞에 “/” 없이 <href="css/~로 사용하고<br/>
http://localhost:8080/<B>study/index2</B> 인 경우, 경로 앞에 “/”를 붙여준다


-해결경로<br/>
스프링 철저 입문 책에서 스프링부트 정적 파일 경로에 대해 봤던 것 같아서 책을 찾아봄(p.679)

>src/main/resources/static 이 위치는 url 호출시 컨텍스트 아래의 경로로 접근할 수 있게 매핑 되어있다<br/>

라고 되어있음.<br/>
이 말은 src/main/resources/static 하위의 파일들은 http://localhost:8080/css/file.css 처럼 접근가능 하다는 뜻<br/><br/>

    http://localhost:8080/index.html
    http;//localhost:8080/css/clean-blog.min.css

그래서 이 경우엔 같은 위치에 css가 있으므로 “/”없이 <link href=”css/~”처럼 상대경로로 가능했고<br/>


    http://localhost:8080/study/index.html
    http;//localhost:8080/css/clean-blog.min.css

이 경우엔 같은 위치에 css가 없으므로 당연히 적용이 되지 않으니까 <link href=”/css/~”처럼 절대경로로 바꿔준다<br/><br/>



*해결하고 보니 더 바보가 된 느낌이다(주륵)*



