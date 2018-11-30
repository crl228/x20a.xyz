---
title: Java中Optional的使用
date: 2018-03-30 16:51:49
updated: 2018-03-30 16:51:49 
tags: [技术,Java,常用]
categories: 技术
---

> 升级SpringBoot2之后SpringData也一并升级到了2.0.5，之前的CrudRepository提供的默认实现很多都采用了Optional的方式，致使之前业务代码中的null处理显得很尴尬，在迁移过程中记录整理下Optional的一些使用。

NPE作为Java中最著名的梗已无需多言，Java8之后提供了Optional的方式来对其进行处理，毕竟Java作为一个大龄语言，没有Elvis之类的特殊语法或运算符来处理null这种类型（结果），加入Optional这种语法糖也算是一点点进步。

以实际中SpringData的一些操作为例

```java
//传统方式
User user = userRepository.findById(1L);
if (user == null) {
    throw new Exception("user not exists");
}
//伪优化
Optional<User> optional = userRepository.findById(1L);
if (!optional.isPresent()) {
    throw new Exception("user not exists");
}
//优雅一点的方式（已抛出业务异常为例）
User user = userRepository.findById(1L).orElseThrow(() -> new Exception("User not exists"));
```

在获取对象内容时减少形如`if(user != null)`这样的判断

```java
private String getName(User user) {
    return Optional.ofNullable(user).map(u -> u.getNickname()).orElse("默认昵称");
}
```