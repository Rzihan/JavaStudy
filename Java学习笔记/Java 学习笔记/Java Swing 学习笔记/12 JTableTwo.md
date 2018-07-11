```
一、添加按钮显示效果

在JTable中，单元格的数据默认是Label的效果，也没有事件。

如果要为单元格添加一个按钮显示效果的话，那么就需要使用到一个swing的接口：javax.swing.table.TableCellRenderer，来改变单元桥格的默认默认渲染方法（DefaultTableCellRenderer），

实现的自定义的渲染器如下：

  
package org.sky.table.render;

import java.awt.Component;

import javax.swing.JButton;
import javax.swing.JPanel;
import javax.swing.JTable;
import javax.swing.table.TableCellRenderer;

public class MyButtonRender implements TableCellRenderer
{
    private JPanel panel;

    private JButton button;

    public MyButtonRender()
    {
        this.initButton();

        this.initPanel();

        // 添加按钮。
        this.panel.add(this.button);
    }

    private void initButton()
    {
        this.button = new JButton();

        // 设置按钮的大小及位置。
        this.button.setBounds(0, 0, 50, 15);

        // 在渲染器里边添加按钮的事件是不会触发的
        // this.button.addActionListener(new ActionListener()
        // {
        //
        // public void actionPerformed(ActionEvent e)
        // {
        // // TODO Auto-generated method stub
        // }
        // });

    }

    private void initPanel()
    {
        this.panel = new JPanel();

        // panel使用绝对定位，这样button就不会充满整个单元格。
        this.panel.setLayout(null);
    }

    public Component getTableCellRendererComponent(JTable table, Object value, boolean isSelected, boolean hasFocus, int row,
            int column)
    {
        // 只为按钮赋值即可。也可以作其它操作，如绘背景等。
        this.button.setText(value == null ? "" : String.valueOf(value));

        return this.panel;
    }

}

 

修改表格的渲染器：this.table.getColumnModel().getColumn(2).setCellRenderer(new MyButtonRender());//只有获取到表格的列后才能添加渲染器。

 

二、添加事件

通过第一部已经为表格添加了默认的渲染器，但是还无法触发事件，触发事件是没有反应的，因为在点击表格时，会触发表格的编辑事件，而要想触发渲染的按钮的事件，还需要通过修改表格的默认编辑器来实现：

package org.sky.table.editor;  
import java.awt.Component;  
import java.awt.event.ActionEvent; 
import java.awt.event.ActionListener;  
  
import javax.swing.DefaultCellEditor;  
import javax.swing.JButton;  
import javax.swing.JPanel;  
import javax.swing.JTable;  
import javax.swing.JTextField;  
  
/** 
 * 自定义一个往列里边添加按钮的单元格编辑器。最好继承DefaultCellEditor，不然要实现的方法就太多了。 
 *  
 */  
public class MyButtonEditor extends DefaultCellEditor  
{  
  
    /** 
     * serialVersionUID 
     */  
    private static final long serialVersionUID = -6546334664166791132L;  
  
    private JPanel panel;  
  
    private JButton button;  
  
    public MyButtonEditor()  
    {  
        // DefautlCellEditor有此构造器，需要传入一个，但这个不会使用到，直接new一个即可。   
        super(new JTextField());  
  
        // 设置点击几次激活编辑。   
        this.setClickCountToStart(1);  
  
        this.initButton();  
  
        this.initPanel();  
  
        // 添加按钮。   
        this.panel.add(this.button);  
    }  
  
    private void initButton()  
    {  
        this.button = new JButton();  
  
        // 设置按钮的大小及位置。   
        this.button.setBounds(0, 0, 50, 15);  
  
        // 为按钮添加事件。这里只能添加ActionListner事件，Mouse事件无效。   
        this.button.addActionListener(new ActionListener()  
        {  
            public void actionPerformed(ActionEvent e)  
            {  
                // 触发取消编辑的事件，不会调用tableModel的setValue方法。   
                MyButtonEditor.this.fireEditingCanceled();  
  
                // 这里可以做其它操作。  
                // 可以将table传入，通过getSelectedRow,getSelectColumn方法获取到当前选择的行和列及其它操作等。   
            }  
        });  
  
    }  
  
    private void initPanel()  
    {  
        this.panel = new JPanel();  
  
        // panel使用绝对定位，这样button就不会充满整个单元格。   
        this.panel.setLayout(null);  
    }  
  
  
    /** 
     * 这里重写父类的编辑方法，返回一个JPanel对象即可（也可以直接返回一个Button对象，但是那样会填充满整个单元格） 
     */  
    @Override  
    public Component getTableCellEditorComponent(JTable table, Object value, boolean isSelected, int row, int column)  
    {  
        // 只为按钮赋值即可。也可以作其它操作。   
        this.button.setText(value == null ? "" : String.valueOf(value));  
  
        return this.panel;  
    }  
  
    /** 
     * 重写编辑单元格时获取的值。如果不重写，这里可能会为按钮设置错误的值。 
     */  
    @Override  
    public Object getCellEditorValue()  
    {  
        return this.button.getText();  
    }  
  
} 

修改表格的默认编辑器：

this.table.getColumnModel().getColumn(2).setCellEditor(new MyButtonEditor());

 

这样后就能基本达到效果了。但是还要注意，对列2来说，还需要启用可编辑功能，才行，不然仍然触发不了事件的。

代码片段：

public boolean isCellEditable(int row, int column)  
{  
    // 带有按钮列的功能这里必须要返回true不然按钮点击时不会触发编辑效果，也就不会触发事件。   
    if (column == 2)  
    {  
        return true;  
    }  
    else  
    {  
        return false;  
    }  
} 

三、测试代码：

测试代码的界面是由windowbuilder插件生成的，懒得自己去写干净的代码了，所以下边的代码有点冗余，大家看表格下边的那段代码即可：

package org.sky.table.frame;  
  
import java.awt.EventQueue;  
  
public class TestTable  
{  
  
    private JFrame frame;  
    private JTable table;  
  
    /** 
     * Launch the application. 
     */  
    public static void main(String[] args)  
    {  
        EventQueue.invokeLater(new Runnable()  
        {  
            public void run()  
            {  
                try  
                {  
                    TestTable window = new TestTable();  
                    window.frame.setVisible(true);  
                }  
                catch (Exception e)  
                {  
                    e.printStackTrace();  
                }  
            }  
        });  
    }  
  
    /** 
     * Create the application. 
     */  
    public TestTable()  
    {  
        this.initialize();  
    }  
  
    /** 
     * Initialize the contents of the frame. 
     */  
    private void initialize()  
    {  
        this.frame = new JFrame();  
        this.frame.setBounds(100, 100, 450, 300);  
        this.frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);  
        this.frame.getContentPane().setLayout(null);  
  
        JPanel panel = new JPanel();  
        panel.setBounds(10, 10, 414, 242);  
        this.frame.getContentPane().add(panel);  
        panel.setLayout(null);  
  
        JScrollPane scrollPane = new JScrollPane();  
        scrollPane.setBounds(10, 10, 394, 222);  
        panel.add(scrollPane);  
  
        this.table = new JTable();  
        scrollPane.setViewportView(this.table);  
  
        this.table.setModel(new DefaultTableModel()  
        {  
            @Override  
            public Object getValueAt(int row, int column)  
            {  
                return (row + 1) * (column + 1);  
            }  
  
            @Override  
            public int getRowCount()  
            {  
                return 3;  
            }  
  
            @Override  
            public int getColumnCount()  
            {  
                return 3;  
            }  
  
            @Override  
            public void setValueAt(Object aValue, int row, int column)  
            {  
                System.out.println(aValue + "  setValueAt");  
            }  
  
            @Override  
            public boolean isCellEditable(int row, int column)  
            {  
                // 带有按钮列的功能这里必须要返回true不然按钮点击时不会触发编辑效果，也就不会触发事件。   
                if (column == 2)  
                {  
                    return true;  
                }  
                else  
                {  
                    return false;  
                }  
            }  
        });  
  
        this.table.getColumnModel().getColumn(2).setCellEditor(new MyButtonEditor());  
  
        this.table.getColumnModel().getColumn(2).setCellRenderer(new MyButtonRender());  
  
        this.table.setRowSelectionAllowed(false);// 禁止表格的选择功能。不然在点击按钮时表格的整行都会被选中。也可以通过其它方式来实现。   
    } 
```