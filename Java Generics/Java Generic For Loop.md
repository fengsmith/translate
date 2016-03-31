Java 泛型有一种新的循环。这种新的循环通常称为 “for each” 循环。for-each 循环更方便迭代泛型集合。例如，迭代泛型 Set 或 List 。

	List<String> list = new ArrayList<String>();
	for (String aString : list) {
		System.out.println(aString);
    }

注意，String 类型的变量是声明在 for 循环内部的圆括号中的。每次迭代（List 中的每个元素）这个变量都会包含当前的元素（当前的 String）。
下面是使用 Set 的一个例子：

	Set<String> set = new HashSet<String>();
	for (String aString : set) {
		System.out.println(aString);
    }

注意，迭代 Set 和 迭代 List 看起来是一样的。
下面是一个 Map 的例子：

	Map<Integer, String> map = new HashMap<Integer, String>();
	// ... 给 map 添加键值对儿
	for (Integer aKey : map.keySet()) {
		String aValue = map.get(aKey);
		System.out.println("" + aKey + ":" + aValue);
    }
	for (String aValue : map.values()) {
		System.out.println(aValue);
	}

注意，Integer 类型的变量和 String 类型的变量是声明在 for-each 循环内部的圆括号中的。每次迭代（Map 的 key set 中的每个元素或 Value 集合中的每个元素）这个变量都会包含当前的元素（当前的 Integer 或 String）。