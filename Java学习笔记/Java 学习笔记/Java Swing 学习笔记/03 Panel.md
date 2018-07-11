## Panel
- Panel 对象可以看成可以容纳Component的空间
- Panel 对象可以拥有自己的布局管理器
- Panel 类拥有从其父类继承来的

    >setBounds(int x,int y,int width,int height)   
    >setSize(int width,int height)   
    >setLocation(int x,int y)   
    >setBackground(Color c)   
    >setLayout(LayoutManager mgr)等方法  
- Panel 的构造方法为：

Panel 的构造方法为：        | ---
---                         | ---
Panel()                     | 使用默认的Flowlayout类布局管理器初始化
Panel(LayoutManager layout) | 使用指定的布局管理器初始化

```
/*
 * 测试 Panel
 */
public class TestPanel {
	public static void main(String[] args) {
		
		Frame f = new Frame("My Frame");
		Panel p = new Panel(null);
		f.setLayout(null);                          //Frame布局管理器设置为null
		f.setBounds(350,200,500,500);               //设置Frame位置及大小
		f.setBackground(new Color(0,0,102));        //设置Frame背景颜色
		p.setBounds(50, 50, 400, 400);              //设置Panel位置及大小
		p.setBackground(new Color(204,204,255));    //设置Panel背景颜色
		f.add(p);                                   //在Frame中添加Panel
		f.setVisible(true);                         //设置Frame为可见
	}
}
```

```
/*
 * 测试多 Panel
 */
public class TestMultiPanel {
	public static void main(String[] args) {
		new MyFrame2("MyFrameWithPanel",200,200,400,300);
	}
}

class MyFrame2 extends Frame{
	private Panel p1,p2,p3,p4;
	
	MyFrame2(String s,int x,int y,int width,int height){
		super(s);
		setLayout(null);
		p1 = new Panel(null);
		p2 = new Panel(null);
		p3 = new Panel(null);
		p4 = new Panel(null);
		//设置Panel的位置和大小
		p1.setBounds(0, 0, width/2, height/2);
		p2.setBounds(width/2, 0, width/2, height/2);
		p3.setBounds(0, height/2, width/2, height/2);
		p4.setBounds(width/2, height/2, width/2, height/2);
		//设置Panel的背景颜色
		p1.setBackground(Color.black);
		p2.setBackground(Color.BLUE);
		p3.setBackground(Color.cyan);
		p4.setBackground(Color.RED);
		//往Frame中添加Panel
		add(p1);
		add(p2);
		add(p3);
		add(p4);
		setBounds(x,y,width,height);    //设置Frame的位置和大小
		setVisible(true);               //设置Frame是否可见
	}
}
```

```
/*
 * Panel 的小练习
 */
public class PanelPractise {
	public static void main(String[] args) {
		new MyFrame3("FrameWithPanel",200,200,600,600);
	}
}

class MyFrame3 extends Frame {
	
	MyFrame3(String s,int x,int y,int w,int h){
		super(s);
		Panel p = new Panel(null);
		Panel p2 = new Panel(null);
		//设置Frame和Panel的位置和大小
		setBounds(x, y, w, h);
		p.setBounds(w/4, h/4, w/2, h/2);
		p2.setBounds(x, y, w, h);
		//设置Frame和Panel的背景颜色
		setBackground(Color.black);
		p.setBackground(Color.yellow);
		p2.setBackground(Color.black);	
		//往Frame中添加Panel
		add(p);
		add(p2);
		setVisible(true);       //设置Frame是否可见	
	}
}
```