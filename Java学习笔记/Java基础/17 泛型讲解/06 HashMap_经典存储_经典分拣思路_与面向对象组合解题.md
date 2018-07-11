```
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;
import java.util.Set;

/**
 * 定义一个Student类，属性：name 	姓名，no 班号，score 成绩
 * 现在将若干Student对象放入List，请统计每个班级的总分和平均分
 * @author Pan梓涵
 *
 */
public class Demo {
	public static void main(String[] args) {
		
		List<Student> list = new ArrayList<Student>();
		//添加学生
		list(list);
		Map<String,ClassRoom> map = new HashMap<String,ClassRoom>();
		//统计成绩
		exam(map,list);
		//打印输出结果
		printTotal(map);
	}
	
	/**
	 * 添加学生
	 */
	public static void list(List<Student> list) {
		list.add(new Student("a", "001", 80));
		list.add(new Student("b", "001", 80));
		list.add(new Student("c", "002", 70));
		list.add(new Student("d", "002", 90));
		list.add(new Student("a", "003", 70));
	}
	
	/**
	 * 统计总分
	 */
	public static void exam(Map<String,ClassRoom> map,List<Student> list) {
		for(Student student : list) {
			ClassRoom room = map.get(student.getNo());
			if(room == null) {
				room = new ClassRoom();
				room.setNo(student.getNo());
				map.put(student.getNo(), room);
			}
			room.setTotal(room.getTotal() + student.getScore());
			room.getStudents().add(student);	
		}
	}
	
	/**
	 * 打印总分和平均分
	 */
	public static void printTotal(Map<String,ClassRoom> map) {
		Set<String> keys = map.keySet();
		for (String string : keys) {
			ClassRoom room = map.get(string);
			System.out.println("班级号：" + room.getNo() + ",总分：" + room.getTotal() + ",平均分：" + room.getTotal()/room.getStudents().size());
		}
	}
	
}

```

### 学生类
```
package com.pzh.test.gen06;

/**
 * 学生类：姓名，班号，成绩
 * @author Pan梓涵
 *
 */
public class Student {

	private String name;//姓名
	private String no;//班号
	private double score;//成绩
	
	public Student() {
		
	}
	
	public Student(String name,String no,double score) {
		this.name = name;
		this.no = no;
		this.score = score;
	}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public String getNo() {
		return no;
	}

	public void setNo(String no) {
		this.no = no;
	}

	public double getScore() {
		return score;
	}

	public void setScore(double score) {
		this.score = score;
	}
	
	
}

```

### 班级类
```
package com.pzh.test.gen06;

import java.util.ArrayList;
import java.util.List;

/**
 * 班级类 属性 no 班级号，students 学生集合，total 总分
 * @author Pan梓涵
 *
 */
public class ClassRoom {
	
	private String no;
	private double total;
	private List<Student> students;
	
	public ClassRoom() {
		students = new ArrayList<Student>();
	}

	public ClassRoom(String no) {
		this();
		this.no = no;
	}

	public String getNo() {
		return no;
	}

	public void setNo(String no) {
		this.no = no;
	}

	public double getTotal() {
		return total;
	}

	public void setTotal(double total) {
		this.total = total;
	}

	public List<Student> getStudents() {
		return students;
	}

	public void setStudents(List<Student> students) {
		this.students = students;
	}
	
	

}

```