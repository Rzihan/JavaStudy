## Layout(布局管理器)
- **Java语言中，提供了布局管理器的对象可以管理**

    - 管理Component在Container中的布局，不必直接设置Component位置和大小
    - 每个Container都有一个布局管理器对象，当容器需要对某个组件进行定位或判断其大小尺寸时，就会调用其对应的布局管理器，调用Container的setLayout方法改变其布局管理器对象
- **Awt提供了5种布局管理器类**
    - FlowLayout
    - BorderLayout
    - GridLayout
    - CardLayout
    - GridBagLayout

### FlowLayout 布局管理器
- FlowLayout 是 Panel 类的默认布局管理器
    - FlowLayout 布局管理器对组件逐行定位，行内从左到右一行排满后换行
    - 不改变组件的大小，按组件原有尺寸显示组件，可设置不同的组件间隔，行距以及对齐方式。
- FlowLayout 布局管理器默认的对齐方式是居中
- **FlowLayout的构造方法**
    - new FlowLayou(FlowLayout.RIGHT,20,40);
        - 右对齐，组件之间的水平间距为20个像素，垂直间距为40个像素
    - new FlowLayout(FlowLayout.LEFT)
        - 左对齐，水平和垂直间距为缺省值（5）
    - new FlowLayout()
        - 使用缺省的居中对齐方式，水平和垂直间距为缺省值（5）

```
/*
 * 测试 FlowLayout
 */
public class TestFlowLayout {

	public static void main(String[] args) {
		Frame f = new Frame("FlowLayout");
		Button button1 = new Button("Ok");
		Button button2 = new Button("Open");
		Button button3 = new Button("Close");
		f.setLayout(new FlowLayout(FlowLayout.CENTER));
		f.add(button1);
		f.add(button2);
		f.add(button3);
		f.setSize(100, 100);
		f.setBackground(Color.BLACK);
		f.setVisible(true);
	}

}
```

### BorderLayout 布局管理器
* BorderLayout-边界布局管理器可以将容器划分为东南西北中5个区域

成员变量                | 含义
---                     |---
BorderLayout.NORTH      | 在容器中添加组件时，组件位于顶端
BorderLayout.SOUTH      | 在容器中添加组件时，组件位于滴端
BorderLayout.EAST       | 在容器中添加组件时，组件位于右端
BorderLayout.WEST       | 在容器中添加组件时，组件位于左端
BorderLayout.CENTER     | 在容器中添加组件时，组件置于中间开始填充

```
/*
 * 测试 BorderLayout
 */
public class TestBorderLayout {

	public static void main(String[] args) {
		Frame f = new Frame("BorderLayout");
		f.setLayout(new BorderLayout());        //为Frame设置布局管理器BorderLayout
		
		Button button1 = new Button("center");
		Button button2 = new Button("south");
		Button button3 = new Button("north");
		Button button4 = new Button("east");
		Button button5 = new Button("west");
		f.add(button1, BorderLayout.CENTER);
		f.add(button2, BorderLayout.SOUTH);
		f.add(button3, BorderLayout.NORTH);
		f.add(button4, BorderLayout.EAST);
		f.add(button5, BorderLayout.WEST);
		
		f.setBackground(Color.BLACK);
		f.pack();                               //打包，设置窗体的大小
		f.setVisible(true);
		
	}

}
```

### GirdLayout 网格布局管理器
构造方法                | 含义
---                     |---
public Girdlayout(int rows,int columns) | rows与columns代表网格的行数和列数
public Girdlayout(int rows,int columns,int horizGap,int vertGap)  | horizGap和vertGap 指定网格之间的距离

```
/*
 * 测试 GirdLayout
 */
public class TestGirdLayout {
	public static void main(String[] args) {
		Frame f = new Frame("This is my frame");
		f.setLayout(new GridLayout(3, 2, 0, 0));    //设置GirdLayout布局管理器

		for (int i = 0; i < 6; i++) {
			f.add(new Button("button" + i));
		}
		
		f.setBackground(Color.BLACK);
		f.pack();                                   //打包，设置窗体大小
		f.setVisible(true);
	}
}
```