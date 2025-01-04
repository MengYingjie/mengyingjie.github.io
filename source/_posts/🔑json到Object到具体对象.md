---
title: 🔑json到Object到具体对象
tags: 
- java
- spring
categories:
- java
- spring
date: 2021-03-02 09:39:50
---

## 🏡环境

SpringBoot + lombok

## 📋遇到需求

大概意思

给出一个参数通过URI接收一个对象test（可能是两种类的对象）和一个type（判断test类型）

## 🌌假设：

如果type为0，test为TestTest对象，

如果type为1，test为TestTest2对象

## 🔬实现过程：

TestTest.class和TestTest2.class

```java
@Data
@Accessors(chain = true)
public class TestTest {
    String abc;
    String aaa;

    TestTest2 test2;
}

@Data
@Accessors(chain = true)
public class TestTest2 {
    String ddd;
    String ccc;
}
```

Controler

```java
@RestController
@RequestMapping("/api/v1")
public class TestController {

    private final Logger log = LoggerFactory.getLogger(TestController.class);

    @PostMapping("/hello")
    public String helloWorld(String type,
                             @RequestBody Object test) throws IOException {
        
        log.info("test {}", test.toString());
        if (type.equals("0")) {
            TestTest testTest = new TestTest();
            ObjectMapper objectMapper = new ObjectMapper();
            String testString = objectMapper.writeValueAsString(test);
            testTest = objectMapper.readValue(testString, TestTest.class);
            return testTest.toString();
        }else if (type.equals("1")){
            TestTest2 testTest2 = new TestTest2();
            ObjectMapper objectMapper = new ObjectMapper();
            String testString = objectMapper.writeValueAsString(test);
            testTest2 = objectMapper.readValue(testString, TestTest2.class);
            return testTest2toString();
        }
        return "error";
    }
}
```

> 遇到此类问题，但看了文章还是未解决
> 评论或加 QQ：781378815

