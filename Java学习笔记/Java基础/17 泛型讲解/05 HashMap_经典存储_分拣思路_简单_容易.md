```
/*
 * this is a cat and that is mice and where is the food?
 * 统计每个单词出现的次数
 *
 * 存储到Map中
 * key： String
 * value： 自定义类型
 */
public class Demo2 {
	
	public static void test() {
		String str = "this is a cat and that is mice and where is the food?";
		//分割字符串
		String[] arrayStr = str.split(" ");
		
		Map<String,Letter> map = new HashMap<String,Letter>();
		for(String temp : arrayStr) {
			if(!map.containsKey(temp)) {
				map.put(temp, new Letter());
			}
			Letter letter = map.get(temp);
			letter.setCount(letter.getCount() + 1);
		}
		
		Set<String> keys = map.keySet();
		for(String temp : keys) {
			Letter letter = map.get(temp);
			System.out.println("name:   " + temp + ",   count:" + letter.getCount());
		}
	}
	
	public static void test1() {
		String str = "this is a cat and that is mice and where is the food?";
		//分割字符串
		String[] arrayStr = str.split(" ");

		Map<String,Letter> map = new HashMap<String,Letter>();
		for (String string : arrayStr) {
			Letter letter = null;
			if(null == map.get(string)) {
				letter = new Letter();
				letter.setCount(1);
				map.put(string, letter);
			}else {
				letter = map.get(string);
				letter.setCount(letter.getCount() + 1);
			}
		}
		Set<String> keys = map.keySet();
		for(String temp : keys) {
			Letter letter = map.get(temp);
			System.out.println("name:   " + temp + ",   count:" + letter.getCount());
		}
		
	}
	
}
```