# Компилируем, пакуем и запускаем Java приложение

### 1. Пишем простую программу.
   
   Файл с кодом Demo.java

```java
public class Demo {
    public static void main(String[] args) {
        System.out.println("Hello Java!");
    }
}
```

### 2. Компилируем в байт-код для JVM.
   
   Если программа состоит из нескольких исходников, то перечисляем их через пробел, команда:

`javac Demo.java` 
   
   в той же директории на выходе появится новый файл `Demo.class`

### 3. Просмотр скомпилированного байт-кода в удобном для изучения формате.
   
   команда:
   
`javap -v Demo.class`

*    Байт-код также как и исходный код оперирует классами и методами.
*    На уровне байт-кода нет указателей и никакого прямого доступа к памяти.

### 4. Запуск программы. 
   
   Для этого нужно указать JVM главный класс программы `Demo.class`, содержащий метод `main` в текущей директории.
   
   команда:

`java Demo`

   Если класс находится в другой директории, то это нужно сообщить JVM при помощи параметра `classpath`
   
   команда:
   
`java -classpath dir Demo`


### 5. Пакуем в JAR-архив.

   Если программа состоит из нескольких файлов, то удобнее упаковать их в один JAR-архив.  
   JAR-архив это тот же ZIP-архив, только с одним дополнением, он содержит файл манифест с мето-информацией о программе.

`MANIFEST.MF` содержит следующую информацию:

```manifest
Manifest-Version: 1.0
Created-By: 1.8.0_281 (Oracle Corporation)
Main-Class: Demo

```

 - версия программы 1.0
 - имя главного класса Demo
 - и т.д.

команда:

`jar cfe demo.jar Demo Demo.class`

`demo.jar` - имя создаваемого архива  
`Demo` - имя главного класса, которое будет прописано в манифесте этого архива  
`Demo.class` - перечисляем все классы, которые хотим упаковать в архив

Просмотр содержимого JAR-архива, не распаковывая его, команда:

`jar tf demo.jar` 

```
META-INF/
META-INF/MANIFEST.MF
Demo.class
```

Распаковка JAR-архива, команда:

`jar xf demo.jar`

### 6. Запуск JAR-архива.

   Есл в JAR-e прописан главный класс, команда:

`java -jar demo.jar`

   Если в JAR-e НЕ прописан главный класс, команда:
   
`java -classpath demo.jar Demo`

`Demo` - имя главного класса

### 7. Упаковка JAR-архива вместе с другими jar-файлами (сторонними библиотеками)

   1. Компилируем для JVM, команда::

   `javac -classpath lib.jar Demo.java`
   
   2. Добавляем в JARб, команда:

   `java -classpath lib.jar;demo.jar Demo` - под Windows

   `java -classpath lib.jar:demo.jar Demo` - под Linux
