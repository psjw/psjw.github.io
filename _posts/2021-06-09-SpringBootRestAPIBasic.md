---
layout: post
title:  "Spring REST API 기본호출 구현"
---

- `HelloWorldController` 를 만들어 기본적인 REST API 연결 확인
    - 함수명 : helloWorld
    - 리턴값 : String
    - Parameter 값 : 없음
    - Method 상단에 `@GetMapping(path ="/hello-world")` 추가
    - 호출 URL : [`http://localhost:8088/hello-world`](http://localhost:8088/hello-world)
    - Reponse : HttpStatus = 200 / Value = Hello World

```java
    import org.springframework.web.bind.annotation.RestController;
    import org.springframework.web.bind.annotation.GetMapping;

    @RestController
    public class HelloWorldController {
    		//GET
        // /hello-world (endpoint)
        //@RequestMapping(mehtod=RequestMethod.Get, path="/hello-world")
        @GetMapping(path ="/hello-world")
        public String helloWorld(){
            return "Hello World";
        }
    }
```

---

- `HelloWorldController` 에 Bean을 추가하여 REST API 호출
    - 함수명 : helloWorldBean
    - 리턴값 : HelloWorldBean
    - Parameter 값 : 없음
    - Method 상단에 `@GetMapping(path ="/hello-world-bean")` 추가
    - 호출 URL : [`http://localhost:8088/hello-world-bean`](http://localhost:8088/hello-world-bean)

```java
    import org.springframework.web.bind.annotation.RestController;
    import org.springframework.web.bind.annotation.GetMapping;

    @RestController
    public class HelloWorldController {
    		//GET
        // /hello-world (endpoint)
        //@RequestMapping(mehtod=RequestMethod.Get, path="/hello-world")
        @GetMapping(path ="/hello-world")
        public String helloWorld(){
            return "Hello World";
        }

    		@GetMapping(path ="/hello-world-bean")
        public HelloWorldBean helloWorldBean(){
            return new HelloWorldBean("Hello World");
        }
    }
```

---

- `HelloWorldBean` 추가
    - 변수타입 / 변수명 : String / message
    - `Lombok` Annotation으로 `setter` / `getter` / `toString` 생성 → `@Data`
    - `Lombok` Annotation으로 `Contructor`생성 → `@AllArgsContructor`

```java
    package com.example.restfulwebservice.helloworld;

    import lombok.AllArgsConstructor;
    import lombok.Data;

    @Data 
    @AllArgsConstructor
    public class HelloWorldBean {
        private String message;
    }
```

   - [`http://localhost:8088/hello-world-bean`](http://localhost:8088/hello-world-bean) 호출 - JSON 결과값 확인

```json
    {
        "message": "Hello World"
    }
```

---

- `PathVariable` 사용
    - `HelloWorldController`에 `helloWorldBean` 메서드 추가
    - 함수명 : helloWorldBean
    - 리턴값 : HelloWorldBean
    - Parameter 값 : String name
    - Method 상단에 `@GetMapping(path ="/hello-world-bean/path-variable/{name}")` 추가
    - Parameter에 `@PathVariable(value="name")` 추가
    - 호출 URL : [`http://localhost:8088/hello-world-bean/path-variable/abcdef`](http://localhost:8088/hello-world-bean/path-variable/abcdef)

```java
    import org.springframework.web.bind.annotation.PathVariable;

    @GetMapping(path ="/hello-world-bean/path-variable/{name}")
    public HelloWorldBean helloWorldBean(@PathVariable(value="name") String name){
    	return new HelloWorldBean(String.format("Hello World, %s",name));
    }
```
    
   - [`http://localhost:8088/hello-world-bean/path-variable/abcdef`](http://localhost:8088/hello-world-bean/path-variable/abcdef) URL 호출

```json
    {
        "message": "Hello World, a"
    }{
        "message": "Hello World, abcdef"
    }
```

---