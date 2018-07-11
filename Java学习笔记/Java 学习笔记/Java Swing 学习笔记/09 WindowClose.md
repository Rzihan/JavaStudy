```
/*
 * 测试 WindowClose
 */
public class TestWindowClose {
	public static void main(String[] args) {
		new MyFrame55("My Frame");
	}

}

class MyFrame55 extends Frame {
	MyFrame55(String s){
		super(s);                                       //调用Frame的构造器
		setLayout(null);                                //设置Frame的布局
		setBounds(300, 300, 400, 300);                  //设置Frame的位置和大小
		setBackground(new Color(204,201,255));          //设置Frame的背景颜色
		setVisible(true);                               //设置Frame为可见
		
		//匿名内部类的写法
		this.addWindowListener(new WindowAdapter() {
			@Override
			public void windowClosing(WindowEvent e) {  //重写windowClosing方法
				setVisible(false);                  //设置Frame为不可见
				System.exit(0);                     //正常退出
			}
			
		});
	}
}
```

## 小测试例子
```
import java.awt.BorderLayout;
import java.awt.Button;
import java.awt.Frame;
import java.awt.TextField;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;

public class TestAnonymous2 {
	Frame f = new Frame("My Frame");                //成员变量f
	TextField tf = new TextField(10);               //成员变量tf
	Button b = new Button("Start");                 //成员变量b

	public TestAnonymous2() {
		f.add(b, BorderLayout.NORTH);               //添加Button到Frame
		f.add(tf, BorderLayout.SOUTH);              //添加TextField到Frame

		b.addActionListener(new ActionListener() {  //监听事件
			private int i;

			@Override
			public void actionPerformed(ActionEvent e) {
				tf.setText(e.getActionCommand() + ++i);
			}
		});
		
		f.addWindowListener(new WindowAdapter() {   //设置窗口关闭
			@Override
			public void windowClosing(WindowEvent e) {
				f.setVisible(false);
				System.exit(0);
			}	
		});
		
		f.pack();               //打包设置Frame大小                
		f.setVisible(true);     //设置为可见
	}

	public static void main(String[] args) {
		new TestAnonymous2();
	}

}
```