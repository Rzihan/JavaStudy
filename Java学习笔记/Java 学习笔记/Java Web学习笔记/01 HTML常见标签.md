### 1、HTML

* (Hyper Text Markup Language),超文本标记语言。
* HTML文件的后缀名一般是：.htm,.html

### 2、表单(form)

### 3、浏览器内核：

​	WebKit,trident

```HTML
<html>

	<head>
		<!-- 标题标签-->
		<title>这是网页的标题</title>
		
	</head>
	
	<!-- 显示在网页中间的内容 -->
	<body>
	
		<h1><font color = "green">这个网页显示的内容</font></h1>
		<!-- 超链接标签 -->
		<a href = "http://www.baidu.com" target = "_blank">这是一个超链接</a><br><br>
		<!-- 表格标签 -->
		<!-- border 设置边框 ；align 设置对其方式 ； width 设置宽度； height 设置高度-->
		<table border = "1" align = "center" width = "80%" height = "50%">
			<!-- 行标签-->
			<tr>
				<!-- 列标签 -->
				<!-- <b> 字体加粗标签-->
				<td align = "center"><b>aa</b></td>
				<td align = "center"><b>aa</b></td>
				<td align = "center"><b>aa</b></td>
			</tr>
			
			<tr>
				<td>aa</td>
				<td>bb</td>
				<td>cc</td>
			</tr>	
		</table>

		<form>
			<!-- text 文本框-->
			<!-- <br>换行 -->
			username:<input type = "text" value = "helloword"><br>
			<!-- password 密码文本框-->
			password:<input type = "password"><br>
			<!-- checkbox 复选框-->
			兴趣:学习<input type = "checkbox">
				 旅游<input type = "checkbox">
				 睡觉<input type = "checkbox"><br>
			<!-- radio 单选框；name 设置radio名字-->
			性别：男<input type = "radio" name = "gender">
				  女<input type = "radio" name = "gender"><br>
			<!-- select 下拉列表框;里面的值用 option 标签-->
			学历：<select>
					<option></option>
					<option>小学</option>
					<option>初中</option>
					<option>高中</option>
					<option>大学</option>
				   </select><br>
			<!-- <textarea>文本域 -->
			评论：<textarea>
			
				   </textarea><br>
			<!-- img src 设置图片-->
			图片：<img src = "C:\Users\Pan梓涵\Desktop\topviewCheck\Images\头像.jpg">
			<!-- file 文件上传-->
			文件上传<input type = "file"><br>
			<!-- submit 提交按钮 -->
			<input type = "submit" value = "submit">&nbsp;&nbsp;&nbsp;
			<!-- reset 重置按钮-->
			<input type = "reset" value = "reset">&nbsp;&nbsp;&nbsp;
			<!-- button 普通按钮-->
			<input type = "button" value = "button" onclick = "javascript:alert('helloword');">
		</form>
	</body>



</html>
```