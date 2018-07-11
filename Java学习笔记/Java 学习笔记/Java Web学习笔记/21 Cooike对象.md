1. Cookie的英文原意是“点心”，它是用户访问Web服务器时，服务器在用户硬盘上存放的信息，好像是服务器送给客户的“点心”。
2. 服务器可以根据Cookie来跟踪用户，这对于需要区别用户的场合（如电子商务）特别有用。
3. 一个Cookie包含一对Key/Value。下面的代码生成一个Cookie并将它写到用户的硬盘上：
```java
Cookie cookie = new Cookie("cookieName","cookieValue");
response.addCookie(the Cookie);
cookie.setMaxAge(15);
Cookie[] cookies = req.getCookies();.setMaxAge(15);
```
