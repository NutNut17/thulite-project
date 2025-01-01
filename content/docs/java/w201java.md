---
title: "Java Concept"
description: "Quick note for Java basic knowledge, concept and syntax"
summary: ""
date: 2024-10-08T19:53:05+08:00
lastmod: 2024-10-08T19:53:05+08:00
draft: false
weight: 201
toc: true
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

{{< inline-svg src="svgs/logos/java.svg" width="100px" height="79px" class="svg-inline-custom" >}}

Quick note for Java basic knowledge, concept and syntax. This notes assume you have basic understanding of general programming language.

### Intro

{{< details "Intro">}}
Java codes can be compied to bytecodes and each device can install a JVM to execute bytecodes. Hence, Java easy with multiplatform.

#### Standard Naming Convention

1. The first word in the name of variable are usually in small letter and the second word in the variable is in capital letter.
2. Verbal words are placed at the front of the variable name.
3. The name of the class usually use a capital letter as the first word.

#### Project and Developement

Download JDK(Java Developement Kit) to develope using Java. A Java project use to organize Java effectively.

A project can be managed by some tools like maven or gradle. Maven is simpler but gradle is preffered as it can fits multiple project in a project and have more capabilities.

IDE is preferred when developinng Java project, Intellij IDEA is well built for this, however VS Code is also a good Java IDE.

#### Project Structure

Package is a namespace that organized set of related classes and interface. Any folder inside the `src/` is considered a package. Each java file can only consists of one class with the same name for both class name and file name. JAR (Java ARchive) file is used to aggregate many files into one. Plugin adds tool to develope java.

{{< /details >}}

### Class and Interface

{{< details "Access Priority">}}

- `private` is only accessible within the same class, including nested class but not inherited class
- `public` member can be accessed from anywhere
- `protected` members can be accessed freely among inherited class but it cannot be access by class outside the inheritance
- Access priority: `public` > undeclared access specifier > `protected` > `private`

{{< /details >}}

{{< details "Instance">}}

- Assign null to delete an instance of a class
- Instance variable and instance function can only be called by it's instance
- `this` is an instance of a class and it was not limited to be in the first line
- `this()` can used to call a constructor in a constructor and only be in the first line of the block
- Since 'this' was an instance, 'this' can't be accessed by class function because 'this' is an instance and are non-static

{{< /details >}}
{{< details "Static">}}

- Class variable must be declared `static` and they are shared among all instance of a class
- Global class variable must be declared with `static`
- Class function must be declared `static` and they can be access by the name or instance of class
- Class function cannot access (store or read) non-static variable and function.

{{< /details >}}
{{< details "Final">}}

- `final` can be used to restrict inheritance, declare and initialize a constant variable, finish overriding. The syntax is silimar to `const`
  in C/C++.

{{< /details >}}
{{< details "Inheritance">}}

- `private` member of superclass can be accessed by superclass public method
- `super()` is similar to `this()` to access superclass of the instance and usually is used to call constructor of super class and only can be called at the first line
- `super` is the object, can be called anywhere
- Always declare a default constructor on superclass
- A subclass class instance can replace a superclass instance-
- Method in subclass may only override it's superclass when the access priority is higher or equal then it's superclass.

{{< /details >}}
{{< details "Abstract" >}}

- `abstract` is used to declare an abstract class or method
- An abstract must only be defined in the inherited part
- An abstract class cannot be an instance
- If an abstract method is still not defined in the inherited class, it must still declared as abstract in inherited class

{{< /details >}}

#### Class

{{< tabs "class">}}

{{< tab "Main.java" >}}

```java

public class Main {
    // Entry of the project
    public static void main(String[] arg) {
        BaseClass base = new BaseClass(0);
        DerivedClass derived = new DerivedClass(valD=2);

        base.start();
        System.out.println(base.getValue());

        // Overrided method
        derived.start()
        System.out.println(derived.getValue());

        // Perform polymorphism
        System.out.println(derived.add(10, 20));
        System.out.println(derived.add(10, 20, 30));
    }
}

```

{{< /tab >}}

{{< tab "BaseClass.java" >}}

```java
public class BaseClass {
    private int value;
    public BaseClass(int val) { this.value= val } // Constructor
    public int getValue() { return value; }
    public void setValue(int val) { this.value = val; }
    public void start() {
        System.out.println("Hello World from BaseClass");
    }
}

```

{{< /tab >}}

{{< tab "DerivedClass.java" >}}

```java
// Inherits BaseClass
public class DerivedClass extends BaseClass {
    private int valueD;

    // Constructor calls the parent class's constructor using 'super', just like this(). val = 1 is the default parameter
    public DerivedClas(int val = 1, int valD) {
        super(val);
        this.valueD = valD;
    }
    public int getValueD() { return valueD; }
    public void setValueD(int valD) { this.valueD = valD; }

    // Overloading(polymorphism): different function, but same function name, different parameters
    public static int add(int a, int b) { return a + b };
    public static int add(int a, int b, int c) { return a + b + c };

    // Overriding(polymorphism): replace parent class's method . '@' annotation is a metadata to provide additional information to the compiler. It will not affect the functionality of code and is useful for readability
    @Override
    public void start() {
        System.out.println("Hello World from Derived Class");
    }
}

```

{{< /tab >}}

{{< /tabs >}}

#### Interface

{{< tabs "interface" >}}

{{< tab "Class.java" >}}

```java
// Java does not support a derived of multiple super class. But multiple implementation and inherited of implements is posibble
public class Class {
    public static void main(String[] arg) {
        // Create array of class Implementation
        Implementation imp[] = new Implementation[2];
        imp[0] = new Implementation();
        imp[0].func1();
        imp[0].func2();
    }
}

class Implementation implements Interface1, Interface2 {
    // Must be public because the implementation are public
    public void func1() {
        System.out.println("Implemantation 1");
    }
    public void func2() {
        System.out.println("Implementataion 2");
    }
}
```

{{< /tab >}}
{{< tab "Interface1.java" >}}

```java
// Interface method must be abstact and the members must be initialised, final and public and it was set defaultly
interface Interface1 {
    int n = 10; // This is final and public
    void func1();// This is abstact and public
}

```

{{< /tab >}}
{{< tab "Interface2.java" >}}

```java
interface Interface2 {
    void func2();// This is abstact and public
}

```

{{< /tab >}}

{{< /tabs >}}

### Java Features

{{< details "Package" >}}

#### Package

Package is used to declare the namespace for a group of classes, and it organizes your classes into a hierarchical structure to avoid conflicts while import is used to import classes, interfaces, or static methods from other packages so that you don't have to use their full names every time.

```java
import packageName.className;
package packageName;
```

* A specific class from a package can be imported by using the keyword `import`
* Declare a package on top of a java file to make all of the classes in the java file as part of the package
* The same package declaration can be done on other java file to put multiple java files into the same package
* A class with no modifier can only be accessed by the same package

- A class must be public to be accessible to other package
- To access to a class in another package, use the syntax `packageName.className`
- If a member of a class is public but the class is not public, it can only be accessed by classes in the same package
- If a member of a class is public and the class is public, it can be accessed by classes on other package
- If a member of a class have no modifier, it could only be accessed by the same package

{{< /details >}}

{{< details "Lambda Function" >}}

#### Lambda Function

{{< tabs "lambda">}}
{{< tab "Example1.java" >}}

```java
// Anoymous inner class can define a new method that is not declared
public class Example1 {
    public static void main(String args[]) {
        (new Example1()
        {
            void start(int n)
            {
                num = n;
                System.out.println(num);
            }
        }).start(5);
    }
    static Example1 class { int num; }
}
// Output: 5
```

{{< /tab >}}
{{< tab "Example2.java" >}}

```java
// Lambda expression to provide implementation for operate method
@FunctionalInterface
interface Calculator {
    int operate(int a, int b);
}

public class Example2 implements Calculator {
    public static void main(String[] args) {
        Calculator addition = (a, b) -> a + b;
        Calculator multiplication = (a, b) -> a * b;

        System.out.println("Addition: " + addition.operate(5, 3));
        // Output: 8
        System.out.println("Multiplication: " + multiplication.operate(5, 3));
        // Output: 15
    }
}
```

{{< /tab >}}
{{< /tabs >}}

{{< /details >}}

{{< details "Operation" >}}

#### Operations

- The tilde (~) in Java is a bitwise NOT operator
- In `assert condition : errorMessage;` statement, if `assert` is `false`, error message will be shown
- `for(type n: numbers)` iterates all element in `number` as `n`
- `var` datatype dynamically determine the datatype and cannot be modified, `var` must be initialized at declaration

{{< /details >}}

{{< details "Input and Output" >}}

#### Input and Output

```java
import java.text.*;         // The "*" imports every package in java.text
import java.util.Scanner;
import java.lang.Math;
import java.util.String

public class className {
    public static void main(String args[]) {

        Scanner scn = new Scanner(System.in); // Decalre scanner
        DecimalFormat f1 = new DecimalFormat("#.00");
        String str = scn.next() // Reads next input
        double base = Double.parseDouble(str);
        double exponent = Double.parseDouble((scn.next()));
        System.out.println((f1.format(Math.pow(base, exponent))));
        System.out.println("Second input" + Double.toString(base));

        scn.close();
    }
    // Input: 2.0 3
    // Output: 8
}
```

{{< /details >}}

{{< details "String" >}}

#### String

Java have few data types to deal with strings. String, StringBuffer, StringBuilder. String is a read only data. While
StringBuffer is like a class, can add and remove char easily. StringBuilder is basically identical to StringBuffer and it's
more effcient but not suitable for multithread

```
String name = new String(args);

String Functions

length()        // Returns the length of string
toUpperCase()   // UpperCase all character in the string
toLowerCase()   // LowerCase all character in the string
int indexOf( String )           // Returns the index of the first argument string as the substring of the original string
int indexOf( String, int n )    // The same as above and start searching from the nth index
char chatAt(int n)  // Returns the character at nth index
String substring(int n) // Returns the substring starting from index n
String replace(char a, char b)  // Replace the first char a as b in the String
String concat(string) // Concatenate String
String trim() // Remove empty space at the head and end of String
int compareTo(string) // Returns 0 if the string are equivalent, return negative value when the argument string is greater

Double.parseDouble(string)  // Reads the double in the string and returns it
Double.toString(double)     // Convert double to String
String.valueOf(double)      // Convert double to String
split()     // Split the Strings seperated by empty spaces. Example: String[] tokens = str.split(" ");
```

String Tokenizer

```java
StringTokenizer st1 = new StringTokenizer(str);
while( st1.hasMoreTokens() ){ System.out.println(st1.nextToken());}
```

Format

```java
double i= 12345.67;

DecimalFormat f1 = new DecimalFormat("##,####.0000");
DecimalFormat f2 = new DecimalFormat("###,###.00");
DecimalFormat f3 = new DecimalFormat("0000,0000.0000");

System.out.println(f1~f3.format(i));

// Outputs:
// 1,2345.6700
// 12,345.67
// 0001,2345.6700
```

StringBuffer Functions

```java
StringBuffer str = new StringBuffer("1234567890");
str.insert(1,"--");
// Output: 1--234567890
```

{{< /details >}}

{{< details "Date" >}}

#### Date

```java
import java.text.DateFormat;
import java.text.SimpleDateFormat;
import java.util.Date;

public class Test {
    public static void main(String[] args) {
        Date date = new Date();
        DateFormat dateFormat = new SimpleDateFormat("EE-MM-dd-yyyy");
        DateFormat shortFormat = DateFormat.getDateTimeInstance(DateFormat.SHORT, DateFormat.SHORT);
        DateFormat mediumFormat = DateFormat.getDateTimeInstance(DateFormat.MEDIUM, DateFormat.MEDIUM);
        DateFormat longFormat = DateFormat.getDateTimeInstance(DateFormat.LONG, DateFormat.LONG);
        DateFormat fullFormat = DateFormat.getDateTimeInstance(DateFormat.FULL, DateFormat.FULL);

    System.out.println(date);
        System.out.println(dateFormat.format(date));
        System.out.println(shortFormat.format(date));
        System.out.println(mediumFormat.format(date));
        System.out.println(longFormat.format(date));
        System.out.println(fullFormat.format(date));
    }
}
// Output:

// Mon Oct 10 19:59:32 MYT 2022
// Mon-10-10-2022
// 10/10/22, 7:59 PM
// Oct 10, 2022, 7:59:32 PM
// October 10, 2022 at 7:59:32 PM MYT
// Monday, October 10, 2022 at 7:59:32 PM Malaysia Time
```

{{< /details >}}

{{< details "Object and Array" >}}

#### Object and Array

`Object` is the base of all class in Java. Even main class is inherited by Object class.

```java
Class getClass();		// Get the type of the class
boolean equals(Object object); 	// boolean bo = b.equals(a) returns true is a and b is the same class
String toString();		// Prints the repretation of class c as String
```

```java
int [][] arr = new int [X][Y];
int arr[][] = new int [X][Y];	// Y could be empty
arr.length()			// Get the length of array.
```

{{< /details >}}

{{< details "Exception" >}}

#### Exception

```java
try{
    // statement
    throw new exceptionName(); // call an exception
}
catch{
    // handling
}
finally{
    // statement when no exception is made
}

void func() throws exception1, exception2 {
    // This method throws exception when called
}
```

{{< /details >}}

{{< details "Method" >}}

#### Method

Parameter passed by objects will be a reference. `final` can be used to avoid the referred parameter to be modified. Below shows a variable parameter

```java
public class VarArgsExample {
    public void printNumbers(int... numbers) {  // Variable arguments of type int
        for (int number : numbers) {
            System.out.println(number);
        }
    }
}

```

{{< /details >}}

{{< details "File Operation" >}}

#### File Operation

```
File file1 = new File("C:\\test.txt");
file1.exists(); //  true if the file exist
file1.getName();
file1.getParent();
file1.getPath();
file1.length();
file1.lastModified();
file1.renameTo(file2);
file1.delete();

String list1[] = file1.list();  // return the name of every file in the directory

Reader class methods

void close()
int read(), read a character
int read(char[] buf), read and store in buf and return the length of characters
int read(char[] buf, int off, int len), read and store in buf from starting at index off for len characters
long skip(long n), skips n characters

Writer class methods

void close()
abstract void flush(), write all the characters in the buffer to the file
void write(char[] buf), write the buf to the file

FileReader(String filename) // A class to read file and the filename is the locaion of the file
FileWriter(String filename) // A class to write file, the original data will be erased
FileWriter(Strnf filename, Boolean a) // if a is true, it will not erase the file

BufferedReader class (BufferedWriter are basically the same, by changing read to write)

BufferedReader(Reader in) // Constructor
BufferedReader(Reader in, int size)

method

void close()
int read() // Read a character
String readLine()

Example:

FileReader fr = new FileReader("C:\\file.txt");
BufferedReader bfr = new BufferedReader(fr);
while(ch = bfr.read())
{
    System.out.print(ch);
}
fr.close();

The example above only work on text files. InputStream and OutputStream can work on both text file and binary file.

FileInputStream(String filename)

method

int available() // get the number of byte of the file
void close()
long skip(long n) // skip n bytes in the stream
int read() // read a byte in the stream
int read(byte[] b) // read the stream and store to b

Example:

public static void main(String args[]) throws IOException
{
    FileInputStream fi = new FileInputStream("C:\\file.txt");
    System.out.println("file size="+fi.available);
    byte ba[] = new byte[fi.available];
    fi.read(ba);
    System.out.println(new String(ba));
    fi.close();
}

FileOutputStream(String filename)// Constructor
FileOutputStream(String filename, Boolean a)// Erase the file in a is false
void write(byte []);
```

{{< /details >}}

{{< details "Multithreading" >}}

#### Multithreading

- Multithread can be done be inheriting `Thread` class or `Runnable` interface
- Newly Created State - When new Thread() is called
- Runnable State - When start() method is called on a new thread
- Blocked State - When wait(), sleep(), join() is called on a running state
- Dead State - when stop() method is called on a running state
- Add the keyword `synchronized` on the class to make sure that the thread will update the value of members correctly

sleep(int); // Must be in try-catch block. Sleep for millisecond
join();     // Must be in try-catch block. Force the thread to finish execute before moving to next line

```java
class CTest extends Thread {
    private String id;

    public CTest(String str) {
        id = str;
    }

    public void run() {
        for (int i = 0; i < 4; i++) {
            for (int j = 0; j < 4; j++) {
                System.out.println(id + " is running");
            }
        }
    }
}

public class T1 {
    public static void main(String[] arg) {
        CTest a = new CTest("a");
        CTest b = new CTest("b");
        a.start();  // Call method start() to do multithreading
        b.start();  // Put these two line code together to do multithreading
        System.out.println("Starting...");  // This line will finish first
    }
}

/**
* Output: (a.start() and b.start() run together)

* Starting...
* b is running
* a is running
* a is running
* b is running
* a is running
* ...
*/
```

{{< /details >}}

{{< details "Collection" >}}

#### Collection

Java Collection Framework insists of three part, Interface, Algorithms and Implementations. Generic is similar to template in
C++. For example we want to make a TreeSet of Integer, TreeSet `<Integer>` tset = new TreeSet `<Integer>`(); The `<Integer>` is generic

Common methods for collection (Returns true when the method success)

```
add(E o)                            // Add object o as new collection
addAll(Collection `<? extends E> c);  // Add all object c which is an element of collection of generic that are extended by E void clear();                       // Remove all elements in the collection contains(Object o); containsAll(Collection<?>` c);
isEmpty();
remove(Object o);
removeAll(Collection `<?> c); retainAll(Collection<?>` c);         // Except for collection c, remove all other elements of collection
int size();
Iterator `<E>` iterator()              // Get collection

SortedSet implements TreeSet. And here are the methods of SortedSet

TreeSet()                           // Construct a new TreeSet
TreeSet(Collection<? extends E> c)  // Construct a new TreeSet with c as elements
E first()   // Get the first element
SortedSet `<E>` headSet(E toElm)       // Get TreeSet that is smaller or equal than toElm
E last()    // Get the final element
SortedSet `<E>` tailSet(E fromElm)     // Get TreeSet that is larger or equal than fromElm
SortedSet `<E>` subSet(E fromElm, E toElm)// Get TreeSet that is between fromElm to toElm

Example: TreeSet ts = new Test `<Integer>`(); System.out.println("The First Element is: "+ts.first());

List belongs to ordered collection. Here are some methods of List

void add(int index, E ele)  // Add element ele at index
boolean addAll(int index, Collection<? extends E> c)    // Add collection at index
E get(int index)
int indexOf(Object o)
Iterator iterator() // Get the object of the set
int lastIndexOf(Object o)
E remove(int index)
E set(int index, E ele) // Set the element ar index to ele
List `<E>` subList(int frontIndex, int toIndex)

Here are some method for linked list and array list

LinkedList()
LinkedList(Collection<? extends E> c)
void addFirst(E o)
void addLast(E o)
E getFirst()
E getLast()
E removeFirst()
E removeLast()

ArrayList()
ArrayList(Collection<? extends E> c)
ArrayList(int initialCapacity)  // Create and set initial capacity
void ensureCapacity(int minCapacity)
void trimToSize()

Map<Key, Value> methods
void clear()
boolean containsKey(Object key)
boolean containsValue(Object value)
Value get(Object key)
boolean isEmpty()
Set `<K>` keySet()         // Convert keys to set
Collection `<V>` values()  // Convert values to collection
Value put(Key key, Value value)
Value remove(Object key)
int size()

HashMap()
HashMap(int initialCapacity)
HashMap(Map<? extends K, ? extends V> m)

SortedMap implementation - TreeMap

TreeMap()
TreeMap(Map<? extends K, ? extends V> m)
TreeMap(SortedMap<K, ? extends V> m)
K firstKey()
K lastKey()
SortedMap `<E>` subMap(K fromKey, K toKey)
SortedMap `<E>` tailMap(K fromKey)

Iterator methods

Iterator `<E>` iterator()
boolean hasNext()
E next()
void remove()
```

Example code

TreeSet `<String>` tset = new TreeSet `<String>`();
// Added some string
Iterator `<String>` ite = tset.iterator();
while(itr.hasNext())
    System.out.print(itr.next() + " ");
// is equal to
System.out.print(test);

ListIterator `<E>` listIterator()
ListIterator `<E>` listIterator(int index)
void add(E o)
boolean hasNext()
boolean hasPrevious()
E next()
E previous()
int nextIndex()
int previousIndex()
void remove()   // Remove the element
void set(E o)   // Set final element as o

ListIterator `<Integer>` litr = llist.listliterator();  // Get the iterator for the llist collection

Example:

```java
import java.util.*;

public class T1 {
    public static void main(String args[]) {
        LinkedList `<Integer>` llist = new LinkedList `<Integer>`();
        for (int i = 0; i <= 100; i += 10)
            llist.add(i);
        ListIterator `<Integer>` litr1 = llist.listIterator();
        System.out.print("Linked List: ");
        while (litr1.hasNext())
            System.out.print(litr1.next() + " ");
        ListIterator `<Integer>` litr2 = llist.listIterator(llist.size());
        System.out.print("\nInverted Linked List: ");
        while (litr2.hasPrevious())
            System.out.print(litr2.previous() + " ");
    }
}
// Output:

// Linked List: 0 10 20 30 40 50 60 70 80 90 100
// Inverted Linked List: 100 90 80 70 60 50 40 30 20 10 0
```

{{< /details >}}

### Java with SQL

{{< details "Database" >}}

#### Database

How to pack JDBC into jar file

1. Download and decompress the JDBC Driver, move the specific jar file to the correct directory.
2. Edit the manifest file by adding all of the jar file and make sure Main-Class is correct.
   Example:

Class-Path: mysql-connector-java-5.0.5-bin.jar
Main-Class: C1
3. Pack the manifest, class, and any other files into single jar.

I) Using Access Database

Class.forName("net.ucanaccess.jdbc.UcanaccessDriver"); // Load the JDBC driver
Connection con = DriverManager.getConnection("jdbc:ucanaccess://c:/java/db2.mdb");// Connect to the databse
// Alternative
DriverManager.registerDriver (new net.ucanaccess.jdbc.UcanaccessDriver());
Connection con = DriverManager.getConnection("jdbc:ucanaccess://c:/java/db2.mdb");// Connect to the databse

II) Using MySQL Database

Class.forName("com.mysql.jdbc.Driver"); // Load the JDBC driver
// Connect to the databse
Connection con=DriverManager.getConnection("jdbc:mysql://host:port/db","account","password");
or
Connection con=DriverManager.getConnection("jdbc:mysql://host:port/db?user=account&password=password");
// In Case of using UNICODE
jdbc:mysql://localhost/school?user=root&password=123&useUnicode=true&characterEncoding=Big5

III) Using Oracle Database

Class.forName("oracle.jdbc.driver.OracleDriver"); // Load the JDBC driver
Connection con = DriverManager.getConnection ("jdbc:oracle:thin:account/password@host:port:db");// Connect to the databse

{{< /details >}}

{{< details "SQL" >}}

#### SQL

```java
Statement stmt=con.createStatement(); // Create Statement object
ResultSet rs=stmt.executeQuery("select * from table1");
int cnt=stmt.executeUpdate("insert into table1 values('xxx','xxx')"); // inser,、update, delete must use executeUpdate method
```

Implementation:

The jar file must have a manifest to set the main class and include all JDBC related jar files as the Class-Path. Then, the
query can be executed from the jar file that are created at the end.

```java
import java.sql.*;

public class Jdbc_access_1
{
  public static void main(String[] args)
  {
    try
    {
      Class.forName("net.ucanaccess.jdbc.UcanaccessDriver"); // Load the JDBC driver
      Connection con = DriverManager.getConnection("jdbc:ucanaccess://c:/java/db1.mdb");//Connect to the databse
      Statement stmt = con.createStatement();
      ResultSet rs = stmt.executeQuery("select * from students");
      while(rs.next())
      {
        String stud_no=rs.getString(1);
        String stud_name=rs.getString(2);
        String stud_sex=rs.getString("stud_sex");
        String stud_addr=rs.getString("stud_addr");
        System.out.println(stud_no+","+stud_name+","+stud_sex+","+stud_addr);
      }
      con.close();
    }
    catch(ClassNotFoundException e)
    {
      System.out.println("Can't find JDBC driver");
      e.printStackTrace();
    }
    catch(SQLException e)
    {
      e.printStackTrace();
    }
  }
}
```

Classes for SQL

```
Statement st; // To execute SQL commands
ResultSet rs; // Used to collect data from database
```

Every set has n column. rs.getString(i) gets the ith column of the current set.
rs.next(), rs.previous(), re.first(), re.last(), re.beforeFirst(), re.afterLast()
If we want to use other method than next(), we need to add the statement:stmt = con.createStatement(ResultSet.TYPE_SCROLL_SENSITIVE,ResultSet.CONCUR_READ_ONLY);

```
rs.absolute(n); // Move to the nth data in the set, if n<0 move to the final nth data
rs.relative(n); // Move like above but in a relative way
rs.deleteRow(); rs.updateRow(); rs.updateString("col_name","str");
```

To execute same SQL statement repeatly, use this

```java
String sqlstr="insert into students (stud_no,stud_name,stud_sex,stud_addr) values (?,?,?,?)";
      PreparedStatement pstmt=con.prepareStatement(sqlstr);
      pstmt.setInt(1,960001);
      pstmt.setString(2,"王小明");
      pstmt.setInt(3,"M");
      pstmt.setString(4,"彰化縣");
      pstmt.executeUpdate();
```

To execute multiple SQL statement at once, use addBatch() and executeBatch()

```java
Statement stmt=con.createStatement();
      stmt.addBatch("insert into students (stud_no,stud_name) values ('960002','王小明')");
      stmt.addBatch("update students set stud_addr='台東' where stud_no='960004' ");
      stmt.executeBatch();
```

To combine the previous two:

```java
String sqlstr="insert into students (stud_no,stud_name) values (?,?)";
      PreparedStatement pstmt = con.prepareStatement(sqlstr);
      pstmt.setString(1,"960001");
      pstmt.setString(2, "王小明");
      pstmt.addBatch();
      pstmt.setString(1,"960002");
      pstmt.setString(2, "陳大器");
      pstmt.addBatch();
      pstmt.executeBatch();

ResultSetMetaData rsmd  = rs.getMetaData(); // Meta data is the data of column itself, but not any row
rsmd.getColumnCount(), rsmd.getColumnName(i), rsmd.getColumnDisplaySize(i)
```

JTable

```java
DefaultTableModel tableModel = new DefaultTableModel();
tableModel.addColumn("str");
JTable jTable1 = new JTable();
jTable1.setModel(tableModel);
jTable1.setFont(new Font("Dialog", 0, 13));
tableModel.addRow(rowData);// rowData is type of String[]
```

{{< /details >}}

{{< details "SQL Syntax" >}}

#### SQL Syntax

SELECT - extracts data from a database
UPDATE - updates data in a database
UPDATE Customers SET ContactName = 'Alfred Schmidt', City= 'Frankfurt' WHERE CustomerID = 1;

DELETE - deletes data from a database
DELETE FROM table_name WHERE condition;

INSERT INTO - inserts new data into a database

insert into table_name (column1, column2, column3, ...) VALUES (value1, value2, value3, ...);
insert into table_name VALUES (value1, value2, value3, ...);

CREATE DATABASE - creates a new database
ALTER DATABASE - modifies a database
CREATE TABLE - creates a new table
ALTER TABLE - modifies a table
DROP TABLE - deletes a table
CREATE INDEX - creates an index (search key)
DROP INDEX - deletes an index
SELECT DISTINCT - used to return only distinct values

select A from B; // We can think of B is primaty set of data in the mdb file.
select column1, column2, ... FROM table_name;
select * from table_name where condition; // condition example: Country = 'Malaysia', Year = 1957

Operator Description Example
=         Equal

> Greater than
> <         Less than
> =         Greater than or equal
> <=         Less than or equal
> <>         Not equal. Note: In some versions of SQL this operator may be written as !=
> BETWEEN     Between a certain range
> LIKE     Search for a pattern
> IN         To specify multiple possible values for a column
> AND
> OR
> NOT

ORDER BY - SELECT * FROM A ORDER BY ... ASC|DESC; // col1 ASC, col2 DESC (col3 ascending, col4 descending)

{{< /details >}}
