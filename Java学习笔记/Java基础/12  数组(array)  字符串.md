## 声明、创建数组对象和初始化
```
//声明
int[] a;
int b[];

//创建数组对象
a = new int[4];
b = new int[5];

//初始化(对数组元素的初始化)
//默认初始化：数组元素相当于对象的成员变量。
//默认值和成员变量的规制一样。数字0，布尔false，char\u0000,引用：null

//动态初始化
for(int i = 0;i < a.length;i++) {
    a[i] = i * 12;
}
//静态初始化
int c[]  = {23,43,56,78};       //长度4，索引范围[0,3]
Car[] cars = {new Car("奔驰"),new Car("比亚迪"),new Car("宝马")};
```

## 字符串
* 常用方法
1. 链接字符串 “+”
2. 获取字符串的信息
```
public class MyTestString{
    public static void main(String[] args){
        
        String str1 = "We like study";
        str1.length();//获取字符串的长度
        str1.indexOf(String s);//获取字符串首次出现的位置
        str1.lastIndexOf(String s);//获取字符串最后出现的位置
        str1.charAt(int index);//获取指定位置的字符
        str1.subString(int beginIndex);//获取子字符串，从索引位置到结束
        str1.trim();//除去字符串前面和后面的空格
        str1.replace(char oldChar,char newChar);//将指定的字符替换成新的字符
        str1.equals("We like study");//比较字符串
        str1.toLowerCase();
        str1.toUpperCase();//字符串大小写转换
        str1.spilt(String sign);/字符串的分割
    }
}
```
## StringBuilder(线程不安全，效率高)  
```
public class MyStringBuider{
    public static void main(String[] args){
        
        StringBuilder sb = new StringBuilder();         //字符数组长度初始为16
        StringBuilder sb1 = new StringBuilder(32);      //字符数组长度初始为32
        StringBuilder sb2 = new StringBuilder("abcd");  //字符数组长度初始为20
        
        sb2.append("ef");                               //追加字符
        sb2.append(true).append(321).append("随便");    //通过return this实现方法链
        
        StringBuilder sb0 = new StringBuilder("a");
        for(int i = 0;i < 1000;i++){
            sb0.append(i);
        }
        System.out.println(sb0);
        
        sb2.delete(int start, int end);                 //删除指定位置的字符
        sb2.insert(int offset, String str);             //插入字符串
    }
}
```


## StringBuffer(线程安全，效率低)