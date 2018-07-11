## TextField
* 构造方法

构造方法                |  功能描述
---|---
TextField()             |  构造新文本字段
TextField(int columns)  |构造具有指定列数的新空文本字段。
TextField(String text)  | 构造使用指定文本初始化的新文本字段
TextField(String text,int columns)|构造使用要显示的指定文本初始化的新文本字段，宽度足够容纳指定列数。

* 常用方法

方法摘要                |  功能描述
---|---
addActionListener(ActionListener l) | 添加指定的操作侦听器
removeActionListener(ActionListener l) |移除指定的操作侦听器
setEchoChar                         | 设置此文本字段的回显字符
setColumns(int columns)             | 设置此文本字段中的列数。
getColumns()                        | 获取此文本字段中的列数。
getEchoChar()                       | 获取用于回显的字符
setText(String t)                   | 将此文本组件显示的文本设置为指定文本。

---  ---
```
/*
 * 测试 TextField
 */
public class TestTextField {
	public static void main(String[] args) {
		new TFFrame();
	}

}

/*
 * 创建自己的窗体类
 */
class TFFrame extends Frame{                        
	TFFrame(){
		TextField tf = new TextField();                //创建文本组件
		tf.setEchoChar('*');                           //设置回显字符
		add(tf);                                       //往Frame中添加组件
		tf.addActionListener(new TFActionListener());  //添加动作监听事件
		pack();                                        //打包，设置窗体大小
		setVisible(true);		                       //设置Frame为可见
	}
}

class TFActionListener implements ActionListener{
	@Override
	public void actionPerformed(ActionEvent e) {
		TextField tf = (TextField) e.getSource();       //获取事件源
		System.out.println(tf.getText());
		tf.setText("");                                 //设置文本组件的值
	}
	
}

```

* 简单的加法测试
```
public class TestMath {
	public static void main(String[] args) {
		new TFFrame2();
	}

}

class TFFrame2 extends Frame {
	TextField num1, num2, num3;

	TFFrame2() {
		num1 = new TextField(10);                   //设置TextField
		num2 = new TextField(10);                   //设置TextField
		num3 = new TextField(10);                   //设置TextField
		Label add = new Label("+");                 //设置Label
		Button addButton = new Button("=");         //设置Button
		addButton.addActionListener(new MyMonitor(this));//添加动作监听事件
		setLayout(new FlowLayout());                //设置布局管理器
		add(num1);                                  //往Frame中添加组件
		add(add);                                   //往Frame中添加组件
		add(num2);                                  //往Frame中添加组件
		add(addButton);                             //往Frame中添加组件
		add(num3);                                  //往Frame中添加组件
		pack();                                     //打包设置Frame的大小
		setVisible(true);                           //设置Frame为可见
	}   
}

class MyMonitor implements ActionListener {
	TFFrame2 tf = null;                             //保留TFFrame的引用

	public MyMonitor(TFFrame2 tf) {
		this.tf = tf;
	}

	@Override
	public void actionPerformed(ActionEvent e) {
		int n1 = Integer.parseInt(tf.num1.getText());
		int n2 = Integer.parseInt(tf.num2.getText());
		tf.num3.setText("" + (n1 + n2));
	}

}
```