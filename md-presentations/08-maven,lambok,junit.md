## Tasks


### Tasks

```java
class Main {
    public static void main(String[] args) throws InterruptedException{
    	String s = "Content from main";
    	Thread thread1 = new Thread(() -> {
    		s = "Content from thread1";
    	});
    	thread1.start();
    	thread1.join();
    }
}
```

1. Content from main
2. Content from thread1
3. Результат не можна передбачити
4. Помилка компіляції


### Tasks

```java
class Box{
	private int a;
	public Box(int a) {this.a = a;}
	public int getA() {return this.a;}
	public void setA(int value) {this.a = value;}
}

class Main {
    public static void main(String[] args) throws InterruptedException{
    	Box box = new Box(3);
    	Thread thread1 = new Thread(() -> {
    		box.setA(4);
    		System.out.println(box.getA());
    	});
    	Thread thread2 = new Thread(() ->{
    		box.setA(7);
    		System.out.println(box.getA());
    	}); 
    	thread1.start();
    	thread2.start();
    	thread1.join();
    	thread2.join();
    }
}
```

1. 4 4
2. 4 7
3. 7 7
4. Результат не можна передбачити