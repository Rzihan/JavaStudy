
方法                | 描述
---                 |---
drawLine(int x1, int y1, int x2, int y2)        | 画一条线
drawOval(int x, int y, int width, int height)   | 绘制椭圆的边框
drawRect(int x, int y, int width, int height)   | 绘制指定矩形的边框。
drawString(String str, int x, int y)            |  使用此图形上下文的当前字体和颜色绘制由指定 string 给定的文本
fillOval(int x, int y, int width, int height)   | 使用当前颜色填充外接指定矩形框的椭圆。
fillRect(int x, int y, int width, int height)   | 填充指定的矩形。
getColor()                          |获取此图形上下文的当前颜色。
```
public class TestPaint {
	public static void main(String[] args) {
		new PaintFrame().launchFrame();
	}
}

class PaintFrame extends Frame {

	@Override
	public void paint(Graphics g) {
		Color c = g.getColor();                     //获取当前画笔颜色
		setBackground(Color.BLACK);                 //设置Frame的背景颜色
		g.setColor(Color.cyan);                     //设置画笔颜色
		g.fillOval(50, 50, 30, 30);                 //画一个实心椭圆
		g.drawRoundRect(80, 80, 40, 40, 5, 5);      //画一个矩形
		g.drawLine(50, 50, 250, 250);               //画直线
		g.drawString("我爱学习，学习使我快乐", 200, 200);//写String字体
		g.drawString("学习！！！", 100, 100);
		g.setColor(c);                              //设置为原先的画笔颜色
	}
	
	public void launchFrame() {
		setBounds(150, 150, 400, 400);              //设置Frame位置和大小
		setVisible(true);                           //设置Frame为可见
	}
}
```