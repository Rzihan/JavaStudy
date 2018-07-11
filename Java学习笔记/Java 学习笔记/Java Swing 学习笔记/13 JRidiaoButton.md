### JRadioButton   
```
JRadioButton(String text)   
创建一个具有指定文本的状态为未选择的单选按钮。
JRadioButton(String text, boolean selected) 
创建一个具有指定文本和选择状态的单选按钮
paramString() 
返回此 JRadioButton的字符串表示形式
```

### ButtonGroup

```
构造方法摘要
ButtonGroup() 
          创建一个新的 ButtonGroup
add(AbstractButton b) 
          将按钮添加到组中。
clearSelection() 
          清除选中内容，从而没有选择 ButtonGroup 中的任何按钮。
getButtonCount() 
          返回此组中的按钮数。
Enumeration<AbstractButton>getElements() 
          返回此组中的所有按钮。
ButtonModel	getSelection() 
          返回选择按钮的模型。
isSelected(ButtonModel m) 
          返回对是否已选择一个 ButtonModel 的判断。
remove(AbstractButton b) 
          从组中移除按钮。
setSelected(ButtonModel m,boolean b) 
          为 ButtonModel 设置选择值
```