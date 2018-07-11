```
/**
	 * 操作目录
	 */
	public static void testFile() {
		File src = new File("C:\\Users\\Pan梓涵\\Desktop\\Test\\Test1\\test2");
		//mkdir() 创建目录，必须确保父目录存在，如果不存在，创建失败
		src.mkdir();
		//mkdirs() 创建目录，如果父目录链不存在，一同创建
		src.mkdirs();
	}
	
	/*
	 * 测试list（）
	 */
	@SuppressWarnings("unused")
	public static void printListFile() {
		File src = new File("C:\\Users\\Pan梓涵\\Desktop\\思修作业");
		printListFileVer(src);
	}
	
	public static void printListFileVer(File src) {
		File[] file =  src.listFiles(new FilenameFilter() {
			//添加过滤器
			@Override
			public boolean accept(File dir, String name) {
				return name.endsWith(".mp4");
			}
		});
		//遍历打印所有文件
		for (File file2 : file) {
			if(!file2.isFile()) {
				printListFileVer(file2);
			}else {
				System.out.println(file2.getName());
			}
		}
	}
	
```