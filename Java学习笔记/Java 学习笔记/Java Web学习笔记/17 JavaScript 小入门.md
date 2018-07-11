#### 1.客户端和服务器验证的比较

* 客户端确认   
    * 减少服务器负载   
    * 缩短用户等待时间   
    * 兼容性难   

* 服务器端确认 
    * 统一确认 
    * 兼容性强 
    * 服务器负载重

#### 2.JavaScript 
* 获取组件的主要方法
```javascript
    var username = document.getElementById("username");
    var username = document.getElementsByName("username")[0];
    var emails = document.getElementsByName("email");
    var nodes = document.getElementsByTagName("input");
```
* 组件的常用属性
```javascript
 var username;
 //属性的值、长度、类型、选择状态
 username.value
 username.value.length
 username.type
 username.checked
```