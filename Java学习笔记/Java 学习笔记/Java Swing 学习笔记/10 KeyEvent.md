## 测试 KeyEvent

```
import java.awt.Color;
import java.awt.Frame;
import java.awt.event.KeyAdapter;
import java.awt.event.KeyEvent;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;

public class TestKey {

	public static void main(String[] args) {
		new MyKeyFrame().runFrame();
	}

}

@SuppressWarnings("serial")
class MyKeyFrame extends Frame {
	void runFrame() {
		setSize(250, 250);                      //设置Frame的大小
		setLocation(200, 200);                  //设置Frame的位置
		setVisible(true);                       //设置Frame为可见
		setBackground(Color.BLACK);             //设置Frame的背景颜色

		addWindowListener(new WindowAdapter() {//设置Window的关闭方式
			@Override
			public void windowClosing(WindowEvent e) {
				setVisible(false);
				System.exit(0);
			}
		});

		addKeyListener(new KeyAdapter() {
			@Override
			public void keyPressed(KeyEvent e) {
				int keyCode = e.getKeyCode();   //获取按下的key位置
				if (keyCode == KeyEvent.VK_UP) {
					System.out.println("Up");   //在后台打印输出UP
				}
			}
		});
	}
}
```