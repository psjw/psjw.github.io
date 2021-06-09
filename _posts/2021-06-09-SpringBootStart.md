---
layout: post
title:  "Mockito"
---


- [`https://start.spring.io/`](https://start.spring.io/) 에 접속한 이후 `ADD DEPENDENCIES` 를 클릭하여 DEPENDENCY 추가 후 아래와 같이 설정 한 후 `GENERATE` 버튼을 클릭 하여 프로젝트를 다운 받음
![](https://images.velog.io/images/psjw/post/7ca61778-9d00-4b86-ad7d-271df165f200/screencapture-start-spring-io-2021-03-28-11_30_52.png)
---

- `pom.xml` 파일을 수정
    - <version>을 `2.1.13.RELEASES`로 변경

```xml
    <parent>
    	<groupId>org.springframework.boot</groupId>
    	<artifactId>spring-boot-starter-parent</artifactId>
    	<version>2.1.13.RELEASE</version>
    	<relativePath/> <!-- lookup parent from repository -->
    </parent>
```

   - `resources` 밑에 `application.yml` 파일 생성 후 서버 포트 변경(8080 → 8088)

```yaml
    server:
      port: 8088
```