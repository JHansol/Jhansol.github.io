---
layout: post
title: Dev 서버 Invalid bound statement 해결 방법
tags: [Postman, Test, Ipsum, Markdown, Portfolio]
---

# mvnw을 통해 빌드된 war "Invalid bound Statement" 해결 방법 

로컬에서 이클립스 스프링 부트 앱을 작동하였을때에는 DB서버와의 연동이 정상적으로 잘 되었다. 그러나 개발서버(Linux)에 소스파일을 올리고 Maven Wrapper(mvnw)을 이용하여 빌드 후 톰캣으로 작동을 시켰을때에는 페이지는 커녕 **"Invalid bound statement (not found):"** 라는 에러가 발생하였다. 

우선 해당 에러메시지는 Mapper의 함수가 연결이 제대로 되지 않아서 발생하는 에러로 추정되나 필자의 경우에는 XML과 java에서 정의한 메소드명이 같았으며 똑같은 소스코드로 로컬에서는 정상적으로 작동이 되었다.  구글링을 통해 원인을 찾아본 결과 mvnw를 이용하여 빌드할때 **src/main/java** 폴더 아래에 있는 xml 파일을 생략하고 빌드할 경우 이러한 에러가 발생한다고 한다. 그래서 pom.xml 설정을 통해 mapper*.xml 파일들도 함께 빌드하도록 해주었더니 에러메시지가 해결되었다.

자세한 해결 방법은 **pom.xml**에서 다음과 같이 추가시켜주면 된다. 

```
<build>
		<plugins>
			....
		</plugins>

		<resources>
			<resource>
				<directory>src/main/java</directory>
				<includes>
					<include>**/*.properties</include>
					<include>**/*.xml</include>
				</includes>
				<filtering>false</filtering>
			</resource>
			<resource>
				<directory>src/main/resources</directory>
				<includes>
					<include>**/*.properties</include>
					<include>**/*.xml</include>
				</includes>
				<filtering>false</filtering>
			</resource>
		</resources>
		
	</build>
```

<*resources> ~ </*resource> 부분을 <*build> 사이에 추가한다.

다시 개발서버에서 mvnw로 빌드한 뒤 war 파일을 구동시키면 정상적으로 작동이 될 것이다. 