# Інформація

Конспект лекцій і методичні вказівки до виконання лабораторних робіт з дисципліни "Крос - платформне програмування" 1-й семестр: Java SE

# Вимоги

- Базові знання однієї із мов - python, c#, c/c++, Pascal/Object Pascal

# Зміст

|Лекція|Пояснення|Готовність лекції|
|-|-|-|
|01-intro|В даній лекції ми познайомимося з історією виникнення **Java** і її станом на даний момент. Розглянемо з чого складається і як працює **JVM**. Що таке **JDK** і **JRE**?|:heavy_check_mark:|
|02-oop|Задача лекції познайомити із **основними принципами ООП** і їх реалізацією в JAVA.|:heavy_check_mark:|
|03-boxing,unboxing,string|В java не все об'єкти, існують також примітивні типи. В даній лекції ми розглянемо як **конвертуються примітивні типи і їх відповідні класи обгортки**. Також розглянемо нюанси використання класу **String**.|:heavy_check_mark: (Конспект відсутній, лише презентація)|
|04-generics, collection framework|Вибір правильної **структури даних** для вирішення завдання є одним із ключових моментів. В даній лекції ми розглянемо структури даних в JAVA, які всі разом називаються **Java Collection Framework**. Також ми розглянемо **параметризовані класи - Generics**.|:heavy_check_mark: (Для дженеріків відсутній конспект)|
|05-exceptions, lambda|В даній лекції ми розглянемо механізм **виключень в Java**. Також темою даної лекці є те, як в Java можна використовувати елементи **функціонального програмування** за допомогою **лямбда - виразів**.|:heavy_check_mark:|
|06-gc,reflection,annotations|Темою даної лекції є два пов'язаних між собою механізма - **рефлексія і анотації**. Також ми розглянемо як в Java працює **Garbage Collector**.|:heavy_check_mark: (Для GC відсутній конспект)|
|07-concurrency, streams|В даній лекції ми розглянемо як можна пришвидшити виконання програми за допомогою **багатопоточного програмування**. Також ми розглянемо **Java Streams API**.|:heavy_check_mark: (Конспект лекцій відсутній. Інформація в презентації)|
|08-maven,lambok,junit|В даній лекції ми розглянемо як **будувати проекти** і підключати залежності із використанням **системи сборки - Maven**. Також познайомимося із **фреймворком для тестування JUnit**.|:heavy_check_mark:|
|09-jdbc|В даній лекції ми розглянемо як за допомогою **JDBC** можна взаємодіяти із **реляційними базами даних**.|:heavy_check_mark:|

# Колабораціонізм

Допомогти проектові, Ви можете 2 способами:
- Побачили синтаксичну помилку, або неточність створіть issue.
- Можете запропонувати власний Fix, або матеріал, який на Вашу думку відсутній. Створіть Pull Request.

# Будування

1. git clone https://github.com/endlesskwazar/java-se-workbook
2. cd java-se-workbook
3. npm i
4. npm run buid

Збудований проект буде доступний в директорії dist. Матеріали знаходяться в директорії workbook. Презентації - presentations.

# TODO

- [ ] Конспект лекцій для boxing, unboxing, string
- [ ] Конспект лекцій для дженеріків
- [ ] Конспект лекцій для GC
- [ ] Конспект лекцій для Concurrency, streams