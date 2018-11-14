---
title: Spring Boot菜鸟踩坑笔记(1)
date: 2018-11-14 10:22:53
tags: [Spring Boot,Java]
categories: Spring Boot
---
报NullPointerException  
@Autowired注入失败  
Dao层代码:
<!-- more -->

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.data.mongodb.core.MongoTemplate;
import org.springframework.stereotype.Repository;

import java.util.List;

@Repository("userDao")
public class UserDaoImpl implements UserDao {

    @Autowired
    private MongoTemplate mongoTemplate;

    @Override
    public List<User> findAll() {
        return mongoTemplate.findAll(User.class);
    }

    @Override
    public void insert(User user) {
        mongoTemplate.insert(user);
    }
}
```

test代码(错误示例):

```java
import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.junit4.SpringRunner;

@RunWith(SpringRunner.class)
@SpringBootTest
public class InvoicemanagerApplicationTests {

    @Test
    public void contextLoads() {
        User user = new User();
        user.setUserName("test");
        user.setUserPassword("123");
        UserDao userDao = new UserDaoImpl();
        userDao.insert(user);
        System.out.println(userDao.findAll().get(0).getUserName());
    }

}
```

会发现报NullpointerException,原因是MongoTemplate为Null。因为MongoTemplate是由Spring Boot自动注入生成的实例，所以在使用时UserDao不应手动new实例，应该也用@Autowired使其注入生成实例。  
改正后:

```java
import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.junit4.SpringRunner;

@RunWith(SpringRunner.class)
@SpringBootTest
public class InvoicemanagerApplicationTests {

    @Autowired
    UserDao userDao;
    @Test
    public void contextLoads() {
        User user = new User();
        user.setUserName("test");
        user.setUserPassword("123");
        userDao.insert(user);
        System.out.println(userDao.findAll().get(0).getUserName());
    }

}

```