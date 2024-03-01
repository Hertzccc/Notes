

# Postman学习笔记

## 1. 接口：API(Application Programming interface)

- 做数据传输，软件提供给外部的服务
- 让内部的数据从外部进行修改

需要鉴权码（token，key，appkey）

内部接口：开发人员自己开发的对自身系统提供的接口

外部接口：开发系统调用外部

+ 接口测试的必要性

  前后端进度不一样时，两边可以用mock模拟

+ 安全考虑

  前端验证容易绕过，直接请求接口![Screen Shot 2024-03-01 at 17.04.22](/Users/nibaba/Library/Application Support/typora-user-images/Screen Shot 2024-03-01 at 17.04.22.png)

## 2. 接口测试本质

测试接口能否正常**交互数据，权限控制以及异常场景**

## 3. 接口数据格式

- ### json(这个多一些)

  1. 三组数据：{error_code:0, msg:"提现成功", data:[]}
  2. json：数据类型，整型，小数，字符串
  3. json由两组数据组成：Map对象，键值对 {key:value, key: value}
  4. 数组：{value1, value2, value3}

​	

- html

  <html>

  ...

  <html>

- xml

  <?xml?version="1.0" encoding="utf8">

  ​	<error_code>0<error_code>

  </xml>

  