## Tasks


### Tasks
```java
//Line 1
switch (cardVal) {
 case 4:
 case 5:
 case 6:
 case 7:
 case 8:
  System.out.println("Hit");
  break;
 case 9:
 case 10:
 case 11:
  System.out.println("Double");
  break;
 case 15:
 case 16:
  System.out.println("Surrender");
  break;
 default:
  System.out.println("Stand");
}
```

Що можна підставити в Line1, щоб було написатано "Stand"

1. int cardVal = 6; 2. int cardVal = 10;
3. int cardVal = 14; 4. int cardVal = 18;


### Tasks
```java
class SuperClass {
 SuperClass(int x) {
  System.out.println("Super");
 }
}
public class SubClass extends SuperClass {
 SubClass() {
     //Line n1
	 System.out.println("Sub 2");
     }
}
```

Що можна підставити в Line1, щоб код скомпілювався:
1. this(10);
2. super(10);
3. SuperClass(10);
4. super.SuperClass (10);


### Tasks
```java
public abstract class Customer {
 private String name;
 public Customer(String name) {
  this.name = name;
 }
 public String getName() {
  return name;
 }
 public abstract void buy();
}
```

Які з цих тверджень правдиві?

1. Не сожна створити екземпляр каласу Customer.
2. Не можна унаслідувати клас Customer.
3. Підкласи Customer не можуть перевизначити метод getName().
4. Дочірній клас Customer повинен реалізувати метод buy().


### Tasks
```java
public interface MyInt {
 public void method1() {
  System.out.println("method1");
 }
 public default void method2() {
  System.out.println("method2");
 }
 public static void method3() {
  System.out.println("method3");
 }
 public abstract void method4();
}
```

Які з цих тверджень правдиві?

1. Лише method4() валідний.
2. method2() method4() валідні.
3. method2(), method3(), method4() валідні.
4. Всі методи валідні.


### Tasks
```java
class Vector{
  private int value;

  public Vector(int value){
    this.value = value;
  }

  public intVal(){
    return this.value;
  }

  public static Vector operator+(Vector vec1, Vector vec2){
    return new Vector(vec1.intVal() + vec2.intVal());
  }
}
```

Який результат виконання?

1. Все ок.
2. Код не скомпілюється.
3. Неправильний синтаксис перезавантаження оператора.


### Tasks
```java
Integer i1 = 22;
Integer i2 = 22;
if (i1 == i2)
	System.out.println("i1 == i2");
Integer i3 = 300;
Integer i4 = 300;
if(i3 == i4)
	System.out.println("i3 == i4");
if(i3.equals(i4))
	System.out.println("i3 == i4");
Integer i5 = new Integer(2);
Integer i6 = new Integer(2);
if(i5 == i6)
	System.out.println("i5 == i6");
```

Що буде напечатано:
1. i1 == i2 i3 == i4 i5 == i6
2. i3 == i4 i5 == i6
3. i1 == i2 i3 == i4
4. i1 == i2


### Tasks
```java
String s1 = "qwe";
String s2 = "qwe";
if(s1 == s2)
	System.out.println("s1 == s2");
String s3 = "zxc";
String s4 = "xcv";
if(s3 == s4)
	System.out.println("s3 == s4 dfd");
if(s3.equals(s4))
	System.out.println("s3 == s4");
String s5 = new String("a");
String s6 = new String("a");
if(s5 == s6)
	System.out.println("s5 == s6");
```

Що буде напечатано:
1. s1 ==s2 s3 == s4 s3 == s4 s5 == s6 
2. s3 == s4 s5 == s6
3. s1 == s2



## GC


### GC



## Collection Framework

