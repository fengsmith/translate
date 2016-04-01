为了能让自定义的集合类型使用 for-each 循环，必须要实现 java.lang.Iterable<E> 接口。下面是一个很简单的例子：

    public class MyCollection<E> implements Iterable<E> {
        public Iterator<E> iterator() {
            return new MyIterator<E>();
        }
    }

下面是相应的 MyIterator 的实现骨架：

    public class MyIterator<T> implements Iterator<T> {
        public boolean hasNext() {
            // 实现 。。。
        }
        public T next() {
            /// 实现 。。。
        }
        public void remove() {
            // 如果支持 remove 方法的话就实现该方法
        }
    }

下面是 MyCollection 的泛化使用和 for-each 循环迭代：

    public static void main(String[] args) {
        MyCollection<String> stringCollection = new MyCollection<String>();
        for (String string : stringCollection) {

        }

    }