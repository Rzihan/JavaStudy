### 1、File_方法 - 文件名

方法名 | 功能
---|---
getName() | 获取文件名
getPath() | 如果是绝对路径，获取绝对路径，否则获取相对路径
getAbsolutePath() | 获取绝对路径
getParent() | 获取上一层的路径，如果是相对路径，则返回空

```
//1、文件名
	public static void TestFileName() {
		File src = new File("110.txt");
		//获取文件名
		System.out.println(src.getName());
		//如果是绝对路径，获取绝对路径，否则获取相对路径
		System.out.println(src.getPath());
		//获取绝对路径
		System.out.println(src.getAbsolutePath());
		//获取上一层的路径，如果是相对路径，则返回空
		System.out.println(src.getParent());
	}
	
```
---
### 2、File_方法 - 判断信息

方法名 | 功能
---|---
exists()    | 是否存在
canWrite()  | 是否可写
canRead()   | 是否可读
isAbsolute() | 是否为绝对路径名
isDirectory() | 是否是一个目录
isFile() | 是否是一个标准文件
```
//2、判断信息
	public static void TestFileManage() {
		File src = new File("110.txt");
		//是否存在
		System.out.println("是否存在：" + src.exists());
		//是否可写，可读
		System.out.println("是否可写：" + src.canWrite());
		System.out.println("是否可读：" + src.canRead());
		//是否为绝对路径名
		System.out.println("是否为绝对路径名：" + src.isAbsolute());
		//是否是一个目录
		System.out.println("是否是一个目录：" + src.isDirectory());
		//是否是一个标准文件
		System.out.println("是否是一个标准文件：" + src.isFile());
	}
```

---
 
### 3、File_方法 - 长度信息
方法名 | 功能
---|---
length()   | 长度信息
```
	//3、长度信息
	public static void TestFileLength() {
		File src = new File("110.txt");
		System.out.println(src.length());
	}
```

---

### 4、File_方法 - 创建和删除
方法名 | 功能
---|---
createNewFile()   | 创建文件
delete()          | 删除文件
```
//4、创建删除文件
	public static void TestFileCreateAndDelete() throws IOException {
		File src = new File("110.txt");
		if(!src.exists()) {
			//创建文件
			boolean flag = src.createNewFile();
		}else {
			//删除文件
			boolean flag = src.delete();
		}
	}
```

