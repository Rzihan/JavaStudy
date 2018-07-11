## Component
- Java的图形用户界面的最基本组成部分是Component，Component类及其子类的对象用来描
  述以图形化的方式显示在屏幕上并能与用户进行交互的GUI元素。例如：一个按钮，一个标
  签等。
- 一般的Component对象不能独立地显示出来，必须将“放在”某一的Container对象中才可以
  显示出来

## Container
- Container是Component子类，Container子类对象可以“容纳”别的Component对象。
- Container对象可使用方法add(...)向其中添加其他Component对象。
- Container是Component的子类，因此Container对象也可以被当做Component对象添加到其 
  他Container对象中
- 有两种常用的Container：
  
  Window：其对象表示自由停泊的顶级窗口。
   
  Panel：其对象可作为容纳其它Component对象，但不能独立存在，必须被添加到其他
  Container中(如Window或Applet)