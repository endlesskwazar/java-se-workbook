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

**Apache Maven** - фреймворк для автоматизації збирання проектів на основі опису їх структури в файлах на мові POM (англ. Project Object Model), що є підмножиною XML.

Maven забезпечує декларативну, а не імперативну (на відміну від засобу автоматизації збирання Apache Ant) збірку проекту. У файлах опису проекту міститься його специфікація, а не окремі команди виконання. Всі завдання по обробці файлів, описані в специфікації, Maven виконує за допомогою їх обробки послідовністю вбудованих і зовнішніх плагінів.

Серед примітних альтернатив - система автоматичного складання Gradle, побудована на принципах Apache Ant і Maven, але використовує спеціалізований DSL на Groovy замість POM-конфігурації.

![](../resources/img/8/8.png)

[Завантажити](https://maven.apache.org/download.cgi) Maven можна з офіційної сторінки проекту.

Перевірити правильність інсталяції можна за допомогою команди:

![](../resources/img/8/9.png)

## Простий проект

Створимо наступну структуру директорій:

![](../resources/img/8/12.png)

Вміст Main.java:

```java
package demo;

class Main {

    public static void main(String[] args) {
        System.out.println("Hello maven");
    }

}
```

Тут цікавого нічого немає.

Вміст pom.xml:

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>demo</groupId>
    <artifactId>demo-app</artifactId>
    <version>1.0-SNAPSHOT</version>

    <properties>
        <maven.compiler.source>1.8</maven.compiler.source>
        <maven.compiler.target>1.8</maven.compiler.target>
    </properties>

    <build>
        <plugins>
            <plugin>
                <!-- Build an executable JAR -->
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-jar-plugin</artifactId>
                <version>3.1.0</version>
                <configuration>
                  <archive>
                    <manifest>
                      <mainClass>demo.Main</mainClass>
                    </manifest>
                  </archive>
                </configuration>
              </plugin>
        </plugins>
    </build>

</project>
```

pom.xml містить один рутовий тег project із XSD - інформацією. Всередині цього тегу містяться інші теги, які описують складання проекту.

- groupId - id пов'язаних проектів. Наприклад, com.company.bank.
- artifactId - id - проекту
- version - вкрсія проекту
- maven.compiler.source - на якій версії JDK написана программа, може викинути помилку, якщо використана фіча, якої немає в JDK
- maven.compiler.target - для якої версії платформи складаємо

Для того, щоб побудувати проект і отримати jar на виході виконаємо команду:

```bash
mvn package
```

![](../resources/img/8/10.png)

Це згенерує директорію target із jar - файлом:

![](../resources/img/8/11.png)

## Maven architypes

Звісно створювати maven - проекти вручну буває доволі довго і важко. Тому в Maven існує система Archetypes.

Якщо коротко, то Archetypes - це шаблони проектів для maven.

Наприклад запустимо наступну команду:

```bash
mvn archetype:generate -DarchetypeGroupId=org.apache.maven.archetypes -Darchet
ypeArtifactId=maven-archetype-quickstart -DarchetypeVersion=1.3 
```

![](../resources/img/8/13.png)

Що згенерує для нас наступний проект:

![](../resources/img/8/14.png)

Перегляну список [archetypes](https://gist.github.com/zbigniewTomczak/4235871)

Тепер детальніше про структуру maven-проекту:

|Директорія|Призначення|
|-|-|
|Джерельний код|${basedir}/src/main/java|
|Ресурси|${basedir}/src/main/resources|
|Тести|${basedir}/src/test|
|Збудований проект|${basedir}/target|

## Стадії складання Maven

Це, звісно, не повний список, але найпоширеніші фази тут присутні.

|Фаза|Пояснення|
|-|-|
|validate|Перевірка правильності проекту і наявності всієї необхідної інформації|
|compile|Компіляція джерельного коду|
|test|Тестування скопільованого коду, використовуючи сумісний тестовий фреймворк|
|package|Компіляція і пакування джерельного коду|
|verify|Перевірка скомпільованого пакету|
|install|Встановлення проекту в локальний репозиторій, щоб його можна було використати як залежність|

## Maven і Eclipse

Використовую IDE, нам не потрібно вводити команди в терміналі, так-як найпоширеніші java IDE мають інтеграцію із maven. Нам навіть непотрібно встановлювати сам maven, оскільки, він сам часто поставляється із самою IDE.

Створення нового maven - проекту в exlipse:

![](../resources/img/8/15.png)

![](../resources/img/8/16.png)

![](../resources/img/8/17.png)

![](../resources/img/8/18.png)

## Залежності

maven дозволяє легко отримувати залежності для нашого проекту. Вони перераховуються в dependencies файлу pom.xml:

Наприклад:

```xml
<dependencies>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>3.8.1</version>
      <scope>test</scope>
    </dependency>
    <dependency>
		<groupId>org.projectlombok</groupId>
		<artifactId>lombok</artifactId>
		<version>1.18.10</version>
		<scope>provided</scope>
	</dependency>
  </dependencies>
```

Знайти залежності можна на [Maven Central Repository](https://search.maven.org/)

Scope - залежностей це область видимості залежності в залежності від фази будування проекту:

|Область видимості|Пояснення|
|-|-|
|test|Якщо залежність junit має область дії test, то ця залежність буде використана maven'ом при виконанні компіляції тієї частини проекту, яка містить тести, а також при запуску тестів на виконання і побудові звіту з результатами тестування коду. Спроба послатися на який-небудь клас або функцію бібліотеки junit в основній частині програми (каталог src / main) викличе помилку.|
|compile|До найбільш часто використовуваної області відносять compile (використовується за умовчанням). Тобто dependency, позначена як compile, або для якої не вказано scope, буде доступна як для компіляції основного додатки і його тестів, так і на стадіях запуску основного додатка або тестів.|
|runtime|Область дії runtime не потрібна для компіляції проекту і використовується тільки на стадії виконання програми.|
|provided|Область дії provided аналогічна compile, за винятком того, що артефакт використовується на етапі компіляції і тестування, а в збірку не включається.|

# junit

# Домашнє завдання

# Контрольні запитання

1. Що таке Jigsaw - модулі, яка їх відмінність від classPath?
2. Для чого використовується lombok? Перелічіть анотації lombok, які ви знаєте.
3. Що таке Maven?
4. Поясніть структуру maven - проекту.
5. Перелічіть стадії складання maven.
6. Яка різницця між groupId і artifactId?
7. Перелічіть і поясніть область видимості залежностей maven.