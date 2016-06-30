# Chapter 1 : Java Building Blocks

## 1. Generals

   * We have to avoid make a multi-line comment in another. it's cause a compilation error
      ```java
      /*
       * /* ferret */
      */
      ```
   * A java file have to  exactly contain one public class, and it could contain other classes but without access modifier (default).
   * The java file will be named with the public class' name.
   * The JVM accept three forms of main
      ```java

          public static void main(String []args)
          public static void main(String args[])
          public static void main(String ... args)
      ```
   * When executing a java class we could pass a string with space.
       ```java
          java Zoo "San Diego" Zoo
       ```
   * Import statements tell Java which packages to __look__ in for classes.
   * The java.lang is an automatically  imported package that conatain System ... so importing it is redundant.
   * import java.nio.*.*; // NO GOOD – you can only have one       // wildcard and it must be at the end
   * If we have a class that exist with same name in two or more impoted packages the compiler is going to give us an Exception
       ```java
           import java.util.*;
           import java.sql.*;

           #The type XXX is ambiguous
       ```
   * If we have the following code, the compiler with not throw an error , it will take util Date because it a wildcard has less priority
       ```java

            import java.util.Date;
            import java.sql.*;

       ```
   * To solve this problem there are two solutions with
    __fully qualiﬁ ed class name__
    ```java
    // solution 1 import one
    import java.util.Date;
    Date d1 = new Date(); // refer java util Date
    java.sql.Date d2 = new java.sql.Date();
    ```
    ```java
    // solution 2 no import
    java.util.Date d = new java.util.Date();
    java.sql.Date d2 = new java.sql.Date();
    ```
## 2. Javadoc
    * to generate javadoc by command:
      ```shell
      javadoc -d /path/to/output /path/to/*.java
      ```
     * to generate package level comment we shoud put a file with the package name .java the will contain  the javadoc and the package declaration  com/foo/package-info.java:
     ```java

     ```
     * javadoc annotations :
      @author name
      Author Name (class/interface only)
      @version major.minor.patch
      Version number (class/interface only)
      @param name description
      Description of parameter (method only)
      @return description
      Description (method only)
      @throws Throwable description
      Description of exception (exceptions are discussed in the next module)
      @deprecated explanation
      Explanation (method only)
      @see package.class#member label
      A hyperlink to a reference package/class/member or field. Or simple text for a “See Also” reference

## 3. Compiling and classpath
   * to compile a java class we use the javac compiler
   ```shell
   javac  <path-to-class_1> <path-to-class_2>
   javac packagea\ClassA.java packageb\ClassB.java
   ```
   * to run a java program we use two manners (jre / java __launcher__)
   ```shell
   java <package-to-class_1>
   java packagea.ClassA
   ```
   NB: package and not the path
   * classpath is a variable used for the JVM or the java compiler to look for other classes or packages that are used in the current program
   * how to set the class path
      1- in command line

      ```shell
         {java|javac} -{classpath|cp} [paths]* <path-to-class>
         java -classpath D:\myprogram;D:\myprogram\lib\supportLib.jar org.mypackage.HelloWorld
      ```
      2- environment variable
      ```shell
        set CLASSPATH=D:\myprogram
        java org.mypackage.HelloWorld
      ```
      NB: to separate paths we use ';' for windows and ':' for linux

      3- manifest file
      ```shell
        Main-Class: org.mypackage.HelloWorld
        Class-Path: lib/supportLib.jar path_2 ...
      ```
## 4. Objects
   * Initialization : instance Initialization run in this order
          1- Fields and _instance initializer_ blocks are run in the order in which they appear in the file.
          2- The constructor runs after all fields and instance initializer blocks have run.
          NB : instance initializer are all the code blocks out of methods
          * Local variables (variables in a method ) are not initialized by default ,we should initialize them before use or a compilation
            error will be throwed.
          * for instance variables or class variables (with static ) they will have default values if they are not initialized
            (boolean ==> false,byte, short, int, long ==> 0, float ,double ==> 0.0, object ==> null ,char ==> \u0000 'NUL')


   * References vs Primitives
          * key differences are:
            - Objects could have null value assigned to it, Primitive no (compilation error)
            - Objects could call methods.
   * Identifiers :
          * The name must begin with a letter or the symbol $ or _
          * Subsequent characters(unicode) may also be numbers.
   * Heap : the jvm has a memory part called _heap_ where objects are allocated there, also primitives in an object, but local primitives variables are allocated in the stack.
   * the garbage collector free the heap's object when they are no longer referenced, the System.gc() propose to the garbage collector to
     free the memory, but nothing make this action sure,because it could be ignored by the gc.
   * finalize(), this method is executed by the gc when the object is no longer referenced, it could be called zero or one time, because the
      gc will attempt to call it, but it the object has at least one refercence this operation will be filled, and then he will no longer call it.


## 5. Primitive types
