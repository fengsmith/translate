可以使用 java.util.Collections.sort() 方法来为 List 集合排序。可以为两种类型的 List 排序。

- List
- LinkedList

### 自然顺序排序

List 排序的方法：

    List list = new ArrayList();
    Collections.sort(list);
像上面这种 list ，根据元素的”自然顺序“排序。有自然顺序的对象必须实现 java.lang.Comparable 接口。换句话说，对象必须通过比较来决定它们之前的顺序。下面是 Comparable 接口：
    
    public inteface Comparable<T> {
        int comparaeTo(T o);
    }
    
compareTo() 方法会把 this 对象和另外一个对象进行比较并返回一个 int 值。下面是返回的 int 值的含义：
    
- 如果 this 对象比另一个对象小的话返回一个负整数
- 如果 this 对象和另一个对象相等的话返回一个 0 
- 如果 this 对象比另一个对象大的话返回一个正整数

在实现 compareTo() 方法时还需要遵守一些其他的规则，上面的这三个规则只是最基本的要求。查阅 JavaDoc 来获取更多细节。

假如，正在为 String 元素的 List 排序。为了排序，每个 string 元素需要和其他元素通过排序算法（这儿不关注比较算法的实现）来比较。每个 string 会把它自己和另外一个 string 进行字母表顺序比较。所以，通过字母表顺序比较，如果一个字符串和另外一个字符串小的话 compareTo() 方法会返回一个负整数。
如果，为自己的 classes 实现 compareTo() 方法时需要考虑这些对象之间应该怎么比较。比如，Employee 对象可以比较它们的 first name、last name、薪水、入职时间等你感兴趣的字段。

### 使用 Comparator 来排序
有时候需要根据其他顺序而不是自然顺序来为 list 排序。甚至，有些对象就没有自然顺序。在这些情形下，只能用 Comparator 。下面的例子使用 Comparator 来排序 list ：
 
    List list = new ArrayList();
    // 往 list 中添加元素
    
    Comparator comparator = new SomeComparator();
    Collections.sort(list, comparator);
注意，现在 Collections.sort() 方法除了有一个 List 参数外还有一个 java.util.Comparator 参数。Comparator 对 list 中的元素两两之间进行比较。下面是 Comparator 接口：

    public interface Comparator<T> {
        int compare(T object1, T object 2);
    
    }
compare() 方法对两个对象比较后返回值的含义：
    
- 如果 object1 比 object2 小的话返回一个负整数
- 如果 object1 和 object2 相等的话返回一个 0 
- 如果 object1 比 object2 大的话返回一个正整数  
   
在实现 compare() 方法时还需要遵守一些其他的规则，上面的这三个规则只是最基本的要求。查阅 JavaDoc 来获取更多细节。  
 
下面的例子使用 Comparator 比较了两个虚拟的 Employee 对象：

    public class MyComparator<Employee> implements Comparator<Employee> {
        public int compare(Employee emp1, Employee emp2) {
            if (emp1.getSalary() < emp2.getSalary()) return -1;
            if (emp1.getSalary() == emp2.getSalary()) return 0;
            if (emp1.getSalary() < emp2.getSalary()) return 1;
        
        }
    }
     
下面是更简短的一种方式：
     
    public class MyComparator<Employee> implements Comparator<Employee> {
        public int compare(Employee emp1, Employee emp2) {
            return emp1.getSalary() - emp2.getSalary();
        }
    } 

通过相减两个 Employee 的薪水，结果自然就分成了 0、负整数、正整数。是不是很巧妙？

如果想要从不同的维度上比较对象，首先从第一个维度上比较（例如，first name）。然后，如果第一个维度相等，再比较第二个维度（例如，last name，薪水等）等。        
     























    