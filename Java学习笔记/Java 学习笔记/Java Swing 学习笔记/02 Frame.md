## Frame
Frame是Window的子类，有Frame或其子类创建的对象为一个窗体

Frame的常用构造方法     | ---
---|---
Frame（）               | ---
Frame（String s）       | 创建标题栏为字符串s的窗口


* 常用方法

方法                    | 说明
---|---
setBounds(int x,int y, int width,int height) | 设置窗体位置和大小，x，y，是左上角坐标，width和height是宽度和高度
setSize(int width,int height)   |设置窗体的大小，width和height分别是宽度和高度
setLocation(int x,int y)        |设置窗体的位置，x，y是左上角坐标
setBackground(Color c)          |设置背景颜色，参数为Color对象
setVisible(boolean b)           |设置是否可见
setTitle(String name)           |---
getTitle();                     |---
setResizable(boolean b)         |设置是否可以调整大小

```
/*
 * 测试Frame
 */
public class TestFrame {
	public static void main(String[] args) {
	
		Frame f = new Frame("My first Frame");  //创建窗体
		f.setLocation(350, 200);                //设置位置
		f.setSize(400, 400);                    //设置大小
		f.setBackground(Color.black);           //设置背景颜色
		f.setResizable(false);                  //设置是否可调整大小
		f.setVisible(true);                     //设置是否可见
		
	}
}
```

```
/*
 * 测试 多个 Frame
 */
public class TestMultiFrame {
	public static void main(String[] args) {
		MyFrame f1 = new MyFrame(100, 100, 200, 200, Color.BLACK);
		MyFrame f2 = new MyFrame(300, 100, 200, 200, Color.BLUE);
		MyFrame f3 = new MyFrame(100, 300, 200, 200, Color.CYAN);
		MyFrame f4 = new MyFrame(300, 300, 200, 200, Color.DARK_GRAY);
	}

}

class MyFrame extends Frame{
	static int id = 0;
	
	MyFrame(int x,int y,int width,int height,Color color){
		super("MyFrame" + (++id));
		setBackground(color);
		setLayout(null);
		setBounds(x,y,width,height);
		setVisible(true);
	}
}
```