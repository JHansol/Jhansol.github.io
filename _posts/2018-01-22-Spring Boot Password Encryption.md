---
layout: post
title: 스프링 부트 암호화
tags: [Postman, Test, Ipsum, Markdown, Portfolio]
---

# 스프링 부트 암호화 

스프링 시큐리티를 이용하여 문자열을 암호화하고 복호화 하는 방법을 포스팅 하려고 한다.

			<dependency>
			<groupId>org.springframework.security</groupId>
			<artifactId>spring-security-config</artifactId>
			</dependency>
우선 스프링 프로젝트에서 pom.xml에 다음과 같이 추가한다.

그 다음 config 파일을 생성하여 BCryptPasswordEncoder 빈 객체를 생성시켜줘야 한다.

필자는 com.hu.ht.myhf**.config** 패키지를 만들고 SomeConfig 라는 클래스를 만들었다.

	
	import org.springframework.context.annotation.Bean;
	import org.springframework.context.annotation.Configuration;
	import org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder;
	
	@Configuration
	public class SomeConfig {
		@Bean
	    public BCryptPasswordEncoder passwordEncoder() {
	        return new BCryptPasswordEncoder(12);
	    }
	}
	
다음과 같이SomeConfig 를 생성하였다면 암호화를 사용할 서비스 및 컨트롤러 클래스로 이동한다.

	@Autowired
	BCryptPasswordEncoder passwordEncoder;

암호화를 사용할 서비스 또는 컨트롤러 클래스에 다음과 같이 선언한다.

```
user.setPassword(passwordEncoder.encode(user.getPassword()));
```

암호화 사용법은 다음과 같으며 passwordEncoder.encode(평문 문자열) 형식으로 사용하면 된다. 이때 salt는 넣어줄 필요 없이 암호화 하는 시점에 랜덤하게 생성되어 salt 기능을 수행 한다.

```
if( passwordEncoder.matches(password, user.getPassword()) ) {
  //참
}
```

복호화 사용법은 다음과 같으며 첫번째 인자에는 평문 데이터, 두번째 인자에는 암호화된 문자열을 넣어준다음 검증을 거치면 된다.