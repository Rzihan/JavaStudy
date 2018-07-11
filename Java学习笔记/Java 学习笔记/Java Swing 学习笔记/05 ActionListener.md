## 动作事件监听器

* 动作事件监听器

事件名称 | 事件源 |  监听接口 | 添加或删除相应类型监听器的方法   
---|---|---|---
ActionEvent |Button、List、TextField|ActionListener|addActionListener(),removelistener()

```
/*
 * 测试 ActionEvent
 */
public class TestActionEvent {

	public static void main(String[] args) {
		
		Frame f = new Frame("This is my Frame");        //创建窗体
		Button b = new Button("Press me !!!");          //创建按钮
		Moniter mn = new Moniter();                     //创建实现ActionListener接口的对象
		b.addActionListener(mn);                        //添加监听器的方法
		f.add(b, BorderLayout.CENTER);                  //往Frame添加组件
		f.pack();                                       //打包设置窗体大小
		f.setVisible(true);                             //设置窗体为可见
	}

}

class Moniter implements ActionListener{
	@Override
	public void actionPerformed(ActionEvent e) {
		System.out.println("我被单击了！！！！");
	}
	
}
```

```
/*
 * 测试 ActionEvent 2
 */
public class TestActionEvent2 {

	public static void main(String[] args) {
		
		Frame f = new Frame("This is my Frame");        //创建Frame
		Button b1 = new Button("Start");                //创建Button
		Button b2 = new Button("Stop");                 //创建Button
		Monitor2 bh = new Monitor2();                    //创建实现ActionListener接口的对象
		b1.addActionListener(bh);                       //添加动作监听事件
		b2.addActionListener(bh);                       //添加动作监听事件
		b2.setActionCommand("Game over");
		f.add(b1, BorderLayout.NORTH);                  //往Frame添加Button
		f.add(b2, BorderLayout.SOUTH);                  //往Frame添加Button
		f.pack();                                       //打包，设置Frame大小
		f.setVisible(true);                             //设置Frame为可见
	}

}

class Monitor2 implements ActionListener{

	@Override
	public void actionPerformed(ActionEvent e) {
		System.out.println("a button has been pressed:\t" + e.getActionCommand());
		
	}
	
}
```