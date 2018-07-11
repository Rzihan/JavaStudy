## Integer类
```
public class MyInteger{
    public static void main(String[] args){
        //Integer的构造方法
        Integer number = new Integer(1000);
        Integer number1 = new Integer("45");
        
        //常用方法
        int num = number.intValue();        //byte,short类似
        number.compareTo(Integer another);  //比较两个Integer对象的值大小
        number.equals(Integer another);     //标胶两个Integer对象是否相等
        num = Integer.parseInt(String str); //返回该字符串等价的整数值
        number1 = Integer.valueOf(String str); //返回保存指定的String值的Integer对象 
        
        Integer.toBinaryString(456);
        Integer.toHexString(456);
        Integer.toOctalString(456);
    }
}
```

## Date时间类(java.util.Date)
```
public class MyDate{
    public static void main(String[] args){
        //两种构造方法
        Date date = new Date();
        Date date = new Date(1000);
        System.out.pirntln(date.getTime();//获取该long类型的数
    }
}
```
## DateFormat类和SimpleDateFormat类
```
public class MyDateFormat {

	public static void main(String[] args) {
		DateFormat df = new SimpleDateFormat("yyyy-MM-dd hh:mm:ss");
		Date date = new Date(123468885L);
		
		String str = df.format(date);
		System.out.println(str);
		
		String str2 = "1998-12-12";
		DateFormat df2 = new SimpleDateFormat("yyyy-MM-dd");
		try {
			Date date2 = df2.parse(str2);
			System.out.println(str2);
		} catch (ParseException e) {
			e.printStackTrace();
		}
	}

}
```