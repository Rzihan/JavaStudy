## 1.CSS功能简介

1. CSS 意思就是层叠样式表

2. 样式定义了HTML元素怎样去显示

3. 样式一般存储在样式表中

4. 样式添加到HTML 4.0中用来解决问题

5. 利用外部样式表可以提高你的工作效率

6. 外部样式表存储在CSS文件中

7. 使用CSS，你的HTML文档可以用不同的样式输出来显示

     
---
## 2.CSS设计背景
​	HTML标签起初被设计成为定义文档的内容。通过使用像<h1><p><table>这样的标签，他们应该表达的是“这是一个标题”，“这是一个段落”“这是一张表格”，二布局该有浏览器来处理并非使用格式化标签

​	为了解决这个难题，W3C(World Wide Web Consotium)这个非营利的，建立标准的组织，为HTML4.0增加了样式。

​	所有主流浏览器都支持样式表

​	样式表定义元素怎样去显示，外部样式表能够让你改变所有出现在你WEB中的外观和布局，而仅仅通过编辑一个单独的CSS文档。(原理就是一动多变)

​	CSS是一个在设计领域中的突破，因为它允许开发者一下就能控制多个WEB页的样式和布局，作为一个WEB开发者你可以为每个HTML元素和应用他的每个页面定义一个你想要的样式。来实现全面的改变，简单的改变样	式，所有与之相关的元素都会主动更新

​	样式表允许样式信息用多种方式来定义。样式可以在一单独的HTML元素中指定，在<head>元素中或在一外部CSS文件中。甚至多个外部样式表能集中在一个单一的HTML文档中

---

## 3.样式表的使用规则

1. Browser default(浏览器默认)
2. External style sheet(外部样式表)
3. Internal style sheet(inside the <head> tag) 内嵌样式表(在<head>标签内)
4. Inline style(inside an HTML element)行内样式(在一HTML元素内)
---
## 4.CSS语法
1. The CSS syntax is made up of three parts: a selector,a property and a value:
2. CSS的语法由三部分组成：一个选择器，一个属性和一个值
3. selector{property:value}

## 5.The class Selector(选择器)
1. 选择器是你希望去定义的HTML元素/标签，每个属性可以有一个值，属性和值由冒号区分开外面用大括号括起来	

   ```css
   body{color:black}
   ```

   

2. 如果值为多个单词则用双引号括起来    

   ```CSS
   p{font-family:"sans serif"}
   ```

   

3. 注意：如果你想指定多个属性，你就必须将每个属性用分号隔开，下面的例子就演示了怎样定义居中红色文字段落      

   ```CSS
   p{text-align:center;color:red} 
   ```

   

4. 用选择器类你可以将同一类型的HTML元素定义出不同的样式。比如你想在你的文档中有两种不同样式的段落：一种是右对其，另外是居中。这就告诉你该怎么样样式来做到这点

   ```CSS
   p.right{text-align:right}
   p.center{text-align:center}
   ```

5. 你必须在你的HTML文档中使用类属性(才能显示出效果)

6. 你也可以省略标签名称直接去定义，这样就可以在所有的HTML元素中使用了。下面的例子就能让所有HTML中所有带class = "center" 的元素居中文字：

   ```CSS
   .center{text-align:center}
   ```

   


## 6.The id Selector(id 选择器)
- 使用id选择器你可以为不同的HTML元素定义相同的样式

- 下面的样式规则对任何一个带有id属性值为“green”的元素都是匹配的
    ```CSS
      green{color:green}
    ```

- 上面的规则将匹配h1和p元素
    ```HTML
    <h1 id = "green">Some text</h1>
    <p id = "green">Some text</h1>
    ```

    