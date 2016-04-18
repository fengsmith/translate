hashCode() 方法和 equals() 方法在 Java Collections 中的对象上扮演了不同的角色。在 JavaDoc 中对这两个方法满足的契约约束有了很好的说明。在本文中我会告诉大家这两个方法在 Java collections 中的对象上扮演了什么样的角色。
 他们的用途，所以知道为什么他们是这样实现的是很重要的。
  
### equals()
在大多数的集合中都使用 equals() 方法来判断一个集合中是否包含某一个元素。例如：
  
  List list = new ArrayList();
  list.add("123");
  
  boolean contains123 = list.contains("123");
  
ArrayList 会迭代所有的元素并执行 "123".equals(element) 方法来判断 element 和参数对象 "123" 是否相等。这是 String.equals() 方法的实现，可以判断两个字符串的内容是否相等。
在移除元素的是否也会用到 equals() 方法。例如：

    List list = new ArrayList();
    list.add("123");
    
    boolean removed = list.remove("123");

ArrayList 会再次迭代所有的元素并执行 "123".equals(element) 方法来判断 element 和参数对象 "123" 是否相等。list 会删除最先找到的并且满足 element.equals("123") 为 true 条件的元素。

可以看出，为自定义的类实现一个正确的 equals() 方法是非常重要的，尤其是在使用 Java Collection 类时。那么，怎么样才能正确的实现一个 equals() 方法呢？
        
两个对象是怎么比较相等呢？这依赖于具体的 application ，classes 和业务场景。例如，加载和处理存储在数据库中的 Employee 对象。下面以 Employee 类为例：

    public class Employee {
        protected long employeeId;
        protected String firstName;
        protected String firstName;
    }  
          
比较两个 Employee 对象是否相等可以仅仅通过比较两个 Employee 对象的 employeeId 是否相等，或者 employeeId、firstName、firstName 这三者都必须相等。下面的两个例子分别实现了两种比较标准：

    public class Employee {
        ...
        public boolean equals(Object o) {
            if (o == null) return false;
            if (! o instanceof Employee) return false;
            Employee other = (Employee) o;
            return this.employeeId == other.employeeId
        }
    }

    public class Employee {
        ...
        public boolean equals(Object o){
            if(o == null) return false;
            if(!(o instanceof) Employee) return false;
    
            Employee other = (Employee) o;
            if(this.employeeId != other.employeeId)      return false;
            if(! this.firstName.equals(other.firstName)) return false;
            if(! this.lastName.equals(other.lastName))   return false;
    
            return true;
        }
    }   
        
上面的两种实现哪种更好依赖于具体的业务场景。有时候，需要从缓存中查询一个 Employee 对象，这种情况下，只比较 employeeId 是否相等就能满足需求。可能需要比较一个拷贝的 Employee 对象和原始的对象之间是否有差异，在这种情形下就需要比较三个字段是否都相等。
        
### hashCode()
在往 HashTable、HashMap、HashSet 中插入对象时会用到 hashCode() 方法。如果不知道 hashtable 的工作原理，可以阅读 [hastables on Wikipedia.org.](http://en.wikipedia.org/wiki/Hashtable)
        
在往 hashtable 中插入对象时需要一个 key 。插入的时候会计算这个 key 的 hash 值，这个 hash 值决定了对象的内部存储位置。查询 hashtable 时也需要使用一个 key ，先计算出这个 key 的 hash 值，然后由这个 hash 值来决定在哪儿搜索对象。

hash code 只指向了一个确定”区域“（list，bucket 等）的内部。由于不同的 key 对象有可能具有相同的 hash code，hash code 本身不能保证找到正确的 key 。然后，hashtable 会迭代这个”区域（所有的 key 都具有相同的 hash code）“并使用 key 对象的 equals() 方法而找到正确的 key 。一旦找到正确的 key，就会把 key 相应的对象返回。

可以看出，在一个 hashtable 中存储和查询对象时需要把 hashCode() 方法和 equals() 方法结合起来使用。

如果想让自己实现的类也能在 Java Collections API 中的 hashtables 中正常的工作，实现 hashCode() 方法时需要遵守两个原则：

- 如果 object1 和 object2 根据它们的 equals() 方法比较时是相等的，它们的 hash code 值也必须是相同的。
- 如果 object1 和 object2 的 hash code 值是相同的，调用它们的 equals() 方法比较时它们未必是相等的。

简而言之：

- 如果两个对象相等，它们也有同样的 hash code 。
- 相同的 hash code 不能保证两个对象是相等的。

下面是两个 hashCode() 方法的实现，这两种实现对应着上面的两个 equals() 方法：

    public class Employee {
        protected long employeeId;
        protected String firstName;
        protected String lastName;
        
        public int hashCode() {
            return (int) employeeId;
        }
    }  

    public class Employee {
        protected long employeeId;
        protected String firstName;
        protected String lastName;
        
        public int hashCode() {
            return (int) employeeId * firstName.hashCode() * lastName.hashCode();
        }
    }            

注意，两个 Employee 对象相等，那么它们的 hash code 也相同，从第一个例子中很容易看出这一点。但，两个 Employee 对象不相等，它们仍然也有可能具有相同的 hash code 。
   
两个例子中，都把 employeeId 截取为 int 。导致了很多 employee 的 hashCode() 方法返回了相同的 hash code ，但这些对象是不相同的，因为它们的 id 不同。

### JavaDoc 中的更多细节

可以通过查阅 JavaDoc 来了解应该到底怎样实现 equals() 方法和 equals() 方法的精确描述。本文的主要目的是解释在 Java Collection classes 中怎样去使用 equals() 方法和 hashCode() 方法。理解了 equals() 方法和 hashCode() 方法之后就可以更好地实现满足自己需求的 equals() 方法和 hashCode() 方法。
   
   
   
   
   
