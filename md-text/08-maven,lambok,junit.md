# Зміст

${toc}

# Jigsaw - модулі

Минуло вісім років після зародження проекту Jigsaw, завдання якого полягає в модулярізаціі платформи Java і зводиться до впровадження загальної системи модулів. Jigsaw вперше з'явився у версії Java 9. Цей реліз раніше планувався і до виходу Java 7, і до Java 8.

Першопочатковою ціллю Jigsaw було не надати програмістам систему модулів, а розбити моноліт java платформи. Пысля появи JIgsaw і мудульної Java можна скласти власну версію платформи не включаючи ті модулі, що Вам не потрібно використовувати, що зменшить розмір самої платформи.

Подивится перелік модулів:

![](../resources/img/8/2.png)

Показати їх загальну кількість:

![](../resources/img/8/3.png)

Що таке модуль?

Описати модуль просто: це одиниця в складі програми, причому кожен модуль відразу містить відповіді на три питання. Ці відповіді записані в файлі module-info.java, Який є у кожного модуля і містить наступну інформацію:

- Як називається модуль?
- Що він експортує?
- Що для цього потрібно?

![](../resources/img/8/1.png)



# Lombok

Java - одина із найпопулярніших мов JVM, але не єдиниа. В останні роки конкуренцію їй складають Scala, Clojure і Kotlin, які забезпечують нову функціональність і оптимізовані функції мови. Коротше кажучи, вони дозволяють робити більше з більш лаконічним кодом.

Ці інновації в екосистемі JVM дуже цікаві. Через конкуренцію Java змушена змінюватися, щоб зберегти конкурентоспроможність. Новий шестимісячний графік випуску і кілька JEP (JDK enhancement proposals) в Java 8 (Valhalla, local-Variable Type Inference, Loom) - доказ того, що Java на довгі роки залишиться конкурентноспроможною мовою.

Проте, розмір і масштаб Java означають, що розробка просувається повільніше, ніж ми хотіли б, не кажучи вже про сильне бажання за всяку ціну підтримувати зворотну сумісність. У будь-розробці першим пріоритетом повинні бути функції, однак тут необхідні функції занадто довго розробляються, якщо взагалі потрапляють в мову. Тому існують сторонні інструменти, які вже надають кращу Java. Один із них - **Project Lombok**.

**Project Lombok** - проект по додаванню додаткової функціональності в Java c допомогою зміни вихідного коду перед Java компіляцією.

По суті, проект Lombok дозволяє позбутися від багатослівності Java в більшості випадків і перестати писати величезні простирадла коду з гетер, сеттерів, equals, hashcode і toString (та їх зазвичай генерує IDE, але читати і змінювати все одно доводиться програмісту), в результаті Java ставати майже такий же короткій як Kotlin, Scala або C#.

## Установка Labmok в Eclipse

Перейдіть на [projectlombok.org]() та перейдіть на вкладку Download, завантажте lombok.jar. Запустіть завантажений labmok.jar(з парави адміністратора, sudo для unix - like) і інсталюйте lombok:


![](../resources/img/8/4.png)

![](../resources/img/8/5.png)

Далі потрібно додати lombok.jar до Build Path проекту:

![](../resources/img/8/6.png)

![](../resources/img/8/7.png)


## Вивчення анотацій Lambok

Давайте створимо клас:

```java
class Student {
	private String name;
	private int age;
	private int cardNumber;
}
```

Звісно цього не достатньо: якщо цей класу буде використаний як модель для ORM потрібно мати пустий конструктор, і взагалі скоріш за все потрібно мати конструктор, який використовує параметри для ініціалізації об'єкта. І це звісно не все, потрібно перевизначити методи equals, toString, hashCode і додати геттери і сеттери:

```java
class Student {
	private String name;
	private int age;
	private int cardNumber;
	
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public int getAge() {
		return age;
	}
	public void setAge(int age) {
		this.age = age;
	}
	public int getCardNumber() {
		return cardNumber;
	}
	public void setCardNumber(int cardNumber) {
		this.cardNumber = cardNumber;
	}
	@Override
	public int hashCode() {
		final int prime = 31;
		int result = 1;
		result = prime * result + age;
		result = prime * result + cardNumber;
		result = prime * result + ((name == null) ? 0 : name.hashCode());
		return result;
	}
	@Override
	public boolean equals(Object obj) {
		if (this == obj)
			return true;
		if (obj == null)
			return false;
		if (getClass() != obj.getClass())
			return false;
		Student other = (Student) obj;
		if (age != other.age)
			return false;
		if (cardNumber != other.cardNumber)
			return false;
		if (name == null) {
			if (other.name != null)
				return false;
		} else if (!name.equals(other.name))
			return false;
		return true;
	}
	@Override
	public String toString() {
		return "Student [name=" + name + ", age=" + age + ", cardNumber=" + cardNumber + "]";
	}
	public Student(String name, int age, int cardNumber) {
		super();
		this.name = name;
		this.age = age;
		this.cardNumber = cardNumber;
	}
	public Student() {
		super();
	}
	
}
```

Тепер розгляньмо як ламбок нам може допомоги, для цього повернімося до першопочаткового класу і додамо анотацію **@AllArgsConstructor**:

```java
@AllArgsConstructor
class Student {
	private String name;
	private int age;
	private int cardNumber;
}
```

Ця анотацію згенерує для конструктор, який використовує всі поля класу:

```java
import lombok.AllArgsConstructor;

@AllArgsConstructor
class Student {
	private String name;
	private int age;
	private int cardNumber;
}

class Main {
    public static void main(String[] args) {
    	Student s = new Student("Alex", 23, 123123);
    }
}
```

Додамо іншу анотацію **@ToString**. Як можна здогадатися із назви вона згенерує для нас методу toString():

```java
import lombok.AllArgsConstructor;
import lombok.ToString;

@AllArgsConstructor
@ToString
class Student {
	private String name;
	private int age;
	private int cardNumber;
}

class Main {
    public static void main(String[] args) {
    	Student s = new Student("Alex", 23, 123123);
    	System.out.println(s);
    }
}
```

Додамо ще антації **@Getter/@Setter**, але уже не на класові, а полі класа:

```java
@AllArgsConstructor
@ToString
class Student {
	@Getter @Setter private String name;
	private int age;
	private int cardNumber;
}

class Main {
    public static void main(String[] args) {
    	Student s = new Student("Alex", 23, 123123);
    	System.out.println(s.getName());
    }
}
```

Ми також можемо додати **@Getter/@Setter** на сам клас, що зенерує геттери і сеттери для всіх допкстимих полів:

```java
import lombok.AllArgsConstructor;
import lombok.Getter;
import lombok.Setter;
import lombok.ToString;

@AllArgsConstructor
@ToString
@Getter
@Setter
class Student {
	private String name;
	private int age;
	private int cardNumber;
}

class Main {
    public static void main(String[] args) {
    	Student s = new Student("Alex", 23, 123123);
    	System.out.println(s.getName() + s.getAge() + s.getCardNumber());
    }
}
```

Додамо анотацію **@EqualsAndHashCode**, вона згенерує для нас equeals, hashCode():

```java
import lombok.AllArgsConstructor;
import lombok.EqualsAndHashCode;
import lombok.Getter;
import lombok.Setter;
import lombok.ToString;

@AllArgsConstructor
@ToString
@Getter
@Setter
@EqualsAndHashCode
class Student {
	private String name;
	private int age;
	private int cardNumber;
}

class Main {
    public static void main(String[] args) {
    	Student s = new Student("Alex", 23, 123123);
    	System.out.println(s.hashCode());
    }
}
```

Щось анотацій стає дедалі більше, в такому випадку, ми можемо використати анотацію **@Data**, які містить в собі **@ToString**, **@EqualsAndHashCode**, **@Getter** на всіх полях, і **@Setter** на всіх не final - полях, і **@RequiredArgsConstructor**! 

```java
import lombok.Data;

@Data
class Student {
	private String name;
	private int age;
	private int cardNumber;
}

class Main {
    public static void main(String[] args) {
    	Student s = new Student();
    	s.setName("Alex");
    	System.out.println(s);
    }
}
```

Всі анотації lombok можна подивитися на [projectlombok.org](https://projectlombok.org/features/all)

# maven

# junit

# Домашнє завдання

# Контрольні запитання

1. фів
2. ів
3. фів
4. віа
5. іваі