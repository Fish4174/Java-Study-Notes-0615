# Java-Study-Notes-0615
6月15日Java学习笔记：泛型与集合
# 第十章实践：泛型与集合

## 1.泛型方法

定义Middle类，其中定义一个泛型方法middle()来计算数组的中间元素，然后在main方法中，定义字符串数组和整型数组后，调用middle方法返回它们的中间元素并输出。

②定义一个泛型方法reverse() 实现数组的逆置

**代码**

```java
public class Middle
{
    public static <T> T middle(T[] array)
    {
        return array[(array.length - 1) / 2];
    }
    public static <T> void reverse(T[] array)
    {
        for(int i = 0, j = array.length - 1; i < j; i++, j--)
        {
            T temp = array[i];
            array[i] = array[j];
            array[j] = temp;
        }
    }

    public static void main(String[] args)
    {
        String[] strings = new String[]{"aaa", "bbb", "ccc", "ddd", "eee"};
        Integer[] ints = new Integer[]{1, 2, 3, 4, 5};
        System.out.println("字符串数组的中间元素是：" + middle(strings));
        System.out.println("整型数组的中间元素是：" + middle(ints));
        reverse(strings);
        reverse(ints);
        System.out.print("逆置后的字符串数组为：");
        for(String s : strings)
        {
            System.out.print(s + " ");
        }
        System.out.println();
        System.out.print("逆置后的整型数组为：");
        for(Integer i : ints)
        {
            System.out.print(i + " ");
        }
    }
}
```

**运行截图**

![](https://img2024.cnblogs.com/blog/2979549/202606/2979549-20260620155137832-1950806553.png)

## 2.程序填空

以下程序实现将中国四大名著按照《水浒传》《三国演义》《西游记》《红楼梦》的顺序摆放输出，请将正确答案写在横线处，并上机验证。

```java
/* Book.java */
import java.util.*;
public class Book {
	public static void main(String[] args) {
		List<String> shelf = new ArrayList<>();
		shelf.add("《三国演义》");
		shelf.add("《莎士比亚诗选》");
		shelf.add("《红楼梦》");
		System.out.println("书架上的书籍：" + shelf); 
		List<String> desk = new ArrayList<>();
		desk.add("《西游记》");
		desk.add("《水浒传》");
		System.out.println("书桌上的书籍：" + desk);
		  ①                                
	      ②                                	               
		System.out.print("中国的四大名著分别是："); 
		for (int i = 0; i < ③   ; i++) {
			System.out.print(shelf.get(i) + " ");
		}
	}
}
```

**代码**

```java
import java.util.*;
public class Book
{
    public static void main(String[] args)
    {
        List<String> shelf = new ArrayList<>();
        shelf.add("《三国演义》");
        shelf.add("《莎士比亚诗选》");
        shelf.add("《红楼梦》");
        System.out.println("书架上的书籍：" + shelf);
        List<String> desk = new ArrayList<>();
        desk.add("《西游记》");
        desk.add("《水浒传》");
        System.out.println("书桌上的书籍：" + desk);
        shelf.add(0, desk.get(1));
        shelf.set(2, desk.get(0));
        System.out.print("中国的四大名著分别是：");
        for (int i = 0; i < shelf.size() ; i++)
        {
            System.out.print(shelf.get(i) + " ");
        }
    }
}
```

**运行截图**

![](https://img2024.cnblogs.com/blog/2979549/202606/2979549-20260620155142019-1162143866.png)

## 3.约瑟夫环（LinkedList）

假设有100只猴子，从1..100进行编号并按顺序围坐⼀圈，从k号开始进⾏1，2，3报数，谁报数为3，就离开圈⼦，剩下的猴子继续报1，2，3，报数为3的出圈...，如此这样，最后⼀个留下来的猴子就是大王。编写一个java程序，解答这个问题。

**代码**

```java
import java.util.LinkedList;

public class Monkey
{
    public static void main(String[] args)
    {
        var monkeyList = new LinkedList<Integer>();
        for(int i = 1; i <= 100; i ++)
            monkeyList.add(i);
        int count = 0;//报数器
        int index = 0;//当前猴子在链表中的索引
        while(monkeyList.size() > 1)
        {
            count ++;//报数
            if(count == 3)
            {
                monkeyList.remove(index);
                count = 0;//报数器清零
            }
            else
                index ++;
            if(index == monkeyList.size())//表走完了，回到表头
                index = 0;
        }
        System.out.println("大王是" + monkeyList.get(0));
    }
}
```

**运行截图**

![](https://img2024.cnblogs.com/blog/2979549/202606/2979549-20260620155145934-494730819.png)

## 4.编程ArrayList的使用

①定义一个学生类Student，包括3个成员变量name(姓名）、sex（性别）和age(年龄)，并通过构造方法初始化。

②定义一个公共的学生管理类StudentManage，在main()方法中创建一个学生顺序表（即创建ArrayList对象，指定类型为Student类），并向其中添加3个学生对象，学生数据可以随意给定，然后输出所有存储在表中的所有学生信息。

③让Student类实现Comparable<T>接口，实现compareTo方法，两个学生对象可以按年龄比较大小（升序比较）。

④在StudentManage的main()方法中继续编写代码，调用Collections.sort(List<T> )方法，对前面定义过的List<Student>表中的学生对象可以按照年龄由小到大进行排序。

**代码**

```java
//Student.java
public class Student implements Comparable<Student>
{
    private String name;
    private String sex;
    private int age;
    public Student(){}
    public Student(String name, String sex, int age)
    {
        this.name = name;
        this.sex = sex;
        this.age = age;
    }
    public String getName()
    {
        return name;
    }
    public String getSex()
    {
        return sex;
    }
    public int getAge()
    {
        return age;
    }
    @Override
    public int compareTo(Student student)
    {
        if(this.age > student.age)
            return 1;
        else if(this.age < student.age)
            return -1;
        else
            return 0;
    }
}
```

```java
//StudentManage.java
import java.util.ArrayList;
import java.util.Collections;
import java.util.Iterator;

public class StudentManage
{
    public static void main(String[] args)
    {
        var stuList = new ArrayList<Student>();
        stuList.add(new Student("Tina", "男", 21));
        stuList.add(new Student("Fish", "男", 20));
        stuList.add(new Student("Tear", "女", 19));
        Collections.sort(stuList);
        //迭代器
        Iterator<Student> iterator = stuList.iterator();
        while(iterator.hasNext())
        {
            //迭代器中存在下一个元素
            //取出下一个元素（学生）
            Student student = iterator.next();
            System.out.println("学生姓名：" + student.getName() + "，性别：" + student.getSex() + "，年龄：" + student.getAge());
        }
    }
}
```

**运行截图**

![](https://img2024.cnblogs.com/blog/2979549/202606/2979549-20260620155148581-269949701.png)
