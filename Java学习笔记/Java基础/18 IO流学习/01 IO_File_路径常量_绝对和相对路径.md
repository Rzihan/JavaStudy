### 1、File常量
```
public class Demo1 {
	
	public static void main(String[] args) {
		printConstants();
	}
	
	/**
	 * 打印File的常量
	 * 1、路径分割符：	;
	 * 2、文件分隔符：\(Windows)	/(linux)
	 */
	public static void printConstants() {
		//路径分割符
		System.out.println(File.pathSeparator);
		//文件分割符
		System.out.println(File.separator);
	}
	
}
```
--- 
### 2、绝对路径和相对路径

 * 绝对路径和相对路径构造File对象
    * File(File parent, String child) 
    * 根据 parent 抽象路径名和 child 路径名字符串创建一个新 File 实例。
    * File(String pathname) 
    * 通过将给定路径名字符串转换为抽象路径名来创建一个新 File 实例。
    * File(String parent, String child) 
    * 根据 parent 路径名字符串和 child 路径名字符串创建一个新 File 实例。
 *

方法名| 功能
---|---
getName() | 返回由此抽象路径名表示的文件或目录的名称。
getPath()  | 将此抽象路径名转换为一个路径名字符串。
getAbsolutePath() |   返回此抽象路径名的绝对路径名字符串。

```
public class Demo2 {

	public static void main(String[] args) {
		Mytest();
	}

	public static void Mytest() {
		String parentPath = "D:/study";
		String name = "2.jpg";
		//相对路径
		File src = new File(parentPath,name);
		src = new File(new File(parentPath),name);
		//输出
		System.out.println(src.getName());
		System.out.println(src.getPath());
		
		//绝对路径
		src = new File("E:/study/student.jpg");
		System.out.println(src.getName());
		System.out.println(src.getPath());
		
		//没有盘符：以user.dir构建
		src = new File("student.jpg");
		System.out.println(src.getName());
		System.out.println(src.getPath());
		System.out.println(src.getAbsolutePath());
		
	}
	
}
```