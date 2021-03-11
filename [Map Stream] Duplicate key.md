错误信息

	java.lang.IllegalStateException: Duplicate key


错误代码示例：

```
public static void main(String[] args) {
    List<User> testList = new ArrayList<>();
    User user = new User();
    user.setUserId(1L);
    user.setUserName("test");
    testList.add(user);
    User user2 = new User();
    user2.setUserId(1L);
    user2.setUserName("test2");
    testList.add(user2);
    Map<Long, String> doctorIdLogoMap = testList.stream()
            .collect(Collectors.toMap(User::getUserId, User::getUserName()));
    System.out.println(doctorIdLogoMap);
}
```

解决，如果碰到重复的key，使用之后出现的key和value。

如果key重复，可以使用最新的value，也可以使用第一个value

```
Map<Long, String> doctorIdLogoMap = testList.stream()
        .collect(Collectors.toMap(User::getUserId, val->val.getUserName(), (v1, v2)->v2));
```

解决参考链接：

https://blog.csdn.net/loophome/article/details/103923031