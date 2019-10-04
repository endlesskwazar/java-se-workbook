## Tasks


### Tasks
```java
try {
	int a = 1/0;
}
finally {
	System.out.println("Finaly block");
}
```

Що буде результатом виконання даного коду:

1. Код не скомпілюється
2. java.lang.ArithmeticException
3. Finaly block, java.lang.ArithmeticException


### Tasks
```java
try {
	int a = 1/0;
}
catch(Exception e) {
	System.out.println("Generic exception");
}
catch(ArithmeticException e) {
	System.out.println("ArithmeticException");
}
```

Що буде результатом виконання даного коду:
1. Код не скомпілюється
2. Generic exception
3. ArithmeticException


### Tasks
```java
try {
	int a = 1/0;
}
catch(ArithmeticException e) {
	System.out.println("catch block");
}
finally {
	throw new ArithmeticException("/ by zero");
}
```

Що буде результатом виконання даного коду:
1. Код не скомпілюється
2. catch block, ArithmeticException / by zero
3. catch block
4. ArithmeticException / by zero


### Tasks
```java
private void work() {
	try {
		work();
	} finally {
		work();
	}
}
```

1. StackOverflowError
2. NullPointerException
3. Зависне
4. Все ок


### Tasks
Чи є даний інтерфейс функціональним:

```java
interface Some {
	default void test() {
		System.out.println("Testing");
	}
	
	static void run() {
		
	}
	
	void grid(Integer a);
}
```



## GC


### GC
```cpp
int
send_request()
{
  size_t n = read_size();

  int* elements = malloc(n * sizeof(int));

  if (read_elements(n, elements) < n){
      return -1;
  }

  return 0;
}
```

Цей код містить потенційний memory leak. Так-як нам вручну потрібно звільнити пам'ять ``` free(elements)```.


### GC
Пишучи на Java, про memory leak потрібно хвилюватися набагато менше, тому що java використовує Garbage collector.

> Збирання сміття (англ. garbage collection) — одна з форм автоматичного керування оперативною пам'яттю комп'ютера під час виконання програм. Підпрограма — «прибиральник сміття» — вивільняє пам'ять від об'єктів, які не будуть використовуватись програмою в подальшому.


### GC
Хоча наявність GC не дає 100% гарантію відсутності memory leak.

> Наприклад, до Java 7 метод substring класу String міг викликати memory leak.


### GC
GC для своєї роботи будує граф об'єктів. GC проходить по графові знаходить об'єкти до яких не можна добратись і знищує їх.

![](../resources/img/6/1.png)


### GC
**Що таке мусор**

> Мусор - це об'єкт на який ніхно не посилається.

Просте визначення, але нажаль не все так просто.


### GC
![](../resources/img/6/2.png)


### GC
- Складно визначити, що таке мусор використовуючи характеристики "хто на кого посилається".
- Мусором є об'єкти, які не можуть використовуватися програмой
- Питання: А які об'єкти можуть використовуватися?


### GC
Не мусором є:

1. Об'єкти в статичних полях
2. Об'єкти в локальних змінних, які доступні із фрейма методів (локальні змінні і стек операндів) стека виклику всіх Java потоків.
3. Об'єкти, на які посилається не мусор


### GC
Java GC базується на наступній гіпотезі:

> Більшість об'єктів скоро стануть недоступні. Посилання із "старих" об'єктів на "нові" існують в малій кількості.


### GC
GC має три стадії:

- Mark: GC проходе по графові об'єктів і визначає,я кі об'єкти є мусором
- Delete/sweep: Знищення мусора
- Compactiong: Фрагментація пам'яті, так щоб об'єкти лижали безперервно


### GC
Java GC - generational collector.

Це означає, що відбувається поділ об'єктів в залежності від часу створення і їх життя.


### GC
Heap поділений на 2 простори:

- Young generation: місце, де живуть молоді об'єкти
- Old(Tenured) generation: місце, де живуть старі об'єкти


### GC
Young generation в свою чергу поділений на 3 простори:

- Eden space: місце де живуть, щойно створені обєкти
- Survivor space from/Survivor space to: Якщо в edem немає місця, gc проходиться по edem і знищує місор, всі, що залишилися переходять в Survivor space


### GC
![](../resources/img/6/3.png)


### GC
Коли в heap закінчється простір, можуть запуститися 3 різновиди GC:

- Minor: чистить young generation
- Major: чистить old generation
- Full: чистить young і old


### GC

![](../resources/img/6/4.png)


### GC
![](../resources/img/6/5.png)


### GC
![](../resources/img/6/6.png)


### GC
![](../resources/img/6/7.png)


### GC
![](../resources/img/6/8.png)


### GC
![](../resources/img/6/9.png)


### GC
![](../resources/img/6/10.png)


### GC
Переміщення між Survivor from до Survivor to, будуть відбуватися доки об'єкт не досягне певного значення, наприклад 16.


### GC
![](../resources/img/6/11.png)


### GC
Види GC:

- Serial collector: працює в тому потоці, що і додаток
- Concurrent collector: працює в іншому потоці. "Stop the world" на етапі mark/re-mark
- parallel collector: Використовує багато потоків і ядер для своєї роботи. Працює лише коли heap повний. "stops the world" коли працює


### GC
![](../resources/img/6/12.png)


### GC

Використовуйте concurent collector: 

- багато пам'яті
- багато CPU
- Додаток повинен зупинятися якомога менше


### GC

Використовуйте parallel collector: 

- мало пам'яті
- мало CPU
- додаток не вразливий до пауз


### GC
![](../resources/img/6/13.png)


### GC

finalizer:

```java
protected void finalize() throws Throwable
```

- Виконайється коли об'єкт знищуватиметься
- Нема упевненості, коли об'єкт буде знищено
- JDK 9, finilize deprecated
