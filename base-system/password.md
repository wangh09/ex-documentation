# Password

## Registration
## 用户注册

user email: "test@example.com", all lower case.
user email: "test@example.com"，全部小写（在前端验证）

user password: "12345678".

generate HmacSHA256 password before send http request by registration form:
在发送口令前，先计算HmacSHA256口令，计算方式为：

```
hashedPassword = HmacSHA256(inputPassword, key=email)
               = HmacSHA256("12345678", key="test@example.com")
               = "dc4f7db0e4515251918d4c9b7de405434692e47017bcd42682bb7a58d0f1e0d6"
```

Send form data with HmacSHA256 password, not plain password:
发送口令时，实际发送的是HmacSHA256口令，而非明文口令：

```
email=test@example.com
password=dc4f7db0e4515251918d4c9b7de405434692e47017bcd42682bb7a58d0f1e0d6
```

Now create user by UserService.createUser():
通过调用UserService.createUser()在exchange创建一个新用户：

1. create an User object to obtain id as user-id.
1. 创建一个User对象并获取id作为User ID；

2. create a random long as "random-number".
2. 创建一个随机数作为"random-number".

3. create a PasswordAuth object with userId=user-id, random=random-number, passwd=HmacSHA256(formPassword, key=random).
3. 创建一个PasswordAuth对象，设置userId=user-id, random=random-number, passwd=HmacSHA256(formPassword, key=random).

NOTE the field name is `passwd` in PasswordAuth.
注意：PasswordAuth存储口令的字段名是`passwd`。

## Sign In

user email: "test@example.com", all lower case.
user password: "12345678".
form-password=HmacSHA256(password, key=email)

Verify password:
验证口令：

1. find user which email is "test@example.com"
1. 根据email查找User对象；

2. find PasswordAuth object by user id.
2. 根据User ID查找PasswordAuth对象；

3. calculate password=HmacSHA256(formPassword, key=PasswordAuth.random) and check with PasswordAuth.passwd.
3. 计算HmacSHA256(formPassword, key=PasswordAuth.random)，并与PasswordAuth.passwd进行对比。
