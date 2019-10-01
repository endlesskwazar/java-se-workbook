## Tasks


### Tasks
```java
class Box< T > {
	private T value;

	public T getValue() {
		return value;
	}

	public void setValue(T value) {
		this.value = value;
	}
}

public class Main {

	public static void main(String[] args) {
		Box<int> b = new Box<>();
	}
}
```

1. Все ок
2. Все погано


### Tasks
```java
class Box< T > {
	private T value;

	public T getValue() {
		return value;
	}

	public void setValue(T value) {
		this.value = value;
	}
}

public class Main {

	public static void main(String[] args) {
		Box b = new Box();
		b.setValue(13);
	}
}
```

1. Все ок
2. Все погано


### Tasks
```java
class Box< T > {
	private T value;

	public T getValue() {
		return value;
	}

	public void setValue(T value) {
		this.value = value;
	}
}

public class Main {

	public static void main(String[] args) {
		Box b = new Box();
		b.setValue(13);
	}
}
```

1. Все ок
2. Все погано


### Tasks
```java
class Box< T > {
	private T value;

	public T getValue() {
		return value;
	}

	public void setValue(T value) {
		this.value = value;
	}
}

public class Main {

	public static void main(String[] args) {
		Box b = new Box();
		b.setValue(13);
		var res = (String)b.getValue();
	}
}
```

1. Все ок
2. Все погано


### Tasks
```java
class Box< T extends Number > {
	private T value;

	public T getValue() {
		return value;
	}

	public void setValue(T value) {
		this.value = value;
	}
}

public class Main {

	public static void main(String[] args) {
		Box< String > b = new Box<>();
	}
}
```

1. Все ок
2. Все погано



## Exceptions


### Exception

