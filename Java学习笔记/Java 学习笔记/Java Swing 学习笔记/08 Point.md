```
/*
 * 测试Point
 */
public class MyMouseAdapter {
	public static void main(String[] args) {
		new MyFrame01("drawing");
	}
}

class MyFrame01 extends Frame {

	ArrayList points = null;                //创建容器，放置point对象

	MyFrame01(String s) {
		super(s);                           //调用Frame的含参构造器
		points = new ArrayList();
		setLayout(null);                    //设置Frame布局管理器为null
		setBounds(200, 200, 400, 300);      //设置Frame位置和大小
		setBackground(Color.BLACK);         //设置Frame背景颜色
		setVisible(true);                   //设置Frame为可见
		this.addMouseListener(new Monitor());//添加鼠标监听事件
	}

	public void paint(Graphics g) {
		Iterator i = points.iterator();
		while (i.hasNext()) {                   //遍历ArrayList集合
			Point p = (Point) i.next();     
			g.setColor(Color.RED);          //设置画笔颜色
			g.fillOval(p.x, p.y, 10, 10);   //画一个椭圆
		}
	}

	public void addPoint(Point p) {         //添加Point到Points 集合中
		points.add(p);
	}
}

class Monitor extends MouseAdapter {
	@Override
	public void mousePressed(MouseEvent e) {
		MyFrame01 f = (MyFrame01) e.getSource();           //获取来源
		f.addPoint(new Point(e.getX(), e.getY()));         //获取点击的坐标
		f.repaint();                                       //刷新窗口
	}

}

```