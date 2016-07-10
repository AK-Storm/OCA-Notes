# Chapter 1 : Java Building Blocks

## 1. Generals

   * We have to avoid put a multi-line comment into another. it's cause a compilation error
      ```java
      /*
       * /* ferret */
      */
      ```
   * A java file have to  exactly contain one public class, and it could contain other classes but without access modifier (default).
   * The java file will be named with the public class's name.
   * The JVM accept three forms of main
      ```java

          public static void main(String []args)
          public static void main(String args[])
          public static void main(String ... args)
      ```
   * When executing a java class we could pass a string with space.
       ```java
          java Zoo "San Diego" param_2
       ```
   * Import statements tell Java which packages to __look__ in for classes.
   * The java.lang is an automatically  imported package that contains System ... so importing it is redundant.
   * import java.nio.*.*; // NO GOOD – you can only have one       // wildcard and it must be at the end
   * If we have a class that exist with the same name in two or more imported packages the compiler is going to give us an Exception
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
    __fully qualiﬁed class name__
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
     * to generate package level comment we shoud put a file with the package name package-info.java that will contains the javadoc and the package declaration  com/foo/package-info.java:
     ```java
      package com.foo;
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
   NB: we use the package and not the path
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
      gc will attempt to call it, but it the object has at least one reference this operation will be filled, and then he will no longer call it.


## 5. Primitive types and Literals
   __Primitives__
   * Java has 8 primitive types :
        * Integers : byte, short ,int ,long
        * Floating-point numbers : float ,double
        * Characters : char
        * Boolean: boolean
   * Q\R why a pure OOP language like java has primitive types ?
        -->  for performance .
   * _Integers_:  
        * all integers types in java a signed no unsigned
        * long 64 bits ,int 32 bits,short 16 bits ,byte 8 bits
   * _Floating point numbers_ : java implements IEE-754 standard double 64 bits , float 32 bits.
   * _Characters_ : 16 bits unicode , ASCII(0-127) is a subset of unicode, char is considered as an unsigned 16 integer .
   * _Boolean_ : true,false.

   __Literals__
   * _Integer literals_ :
        * by default integer literals are **int** .
        * forms: decimal : 1234; hexa : 0XA52,0xa54; octal: 012; binary : 10101010.
        * we could use _ in integer literals, but not in the start or at the end 06_03_06_15,1010_0010_1100.
        * to assigned an integer literal to a long we use l or L ex ; long a = 12l;
        * to assign an integer literal to short or byte the JVM convert it automatically but the value should be in range.

    * _Floating point literals_ :
        * by default floating point literals are **double**.
        * forms: - standard notation : 12.365 .
                 - scientific notation : 1.235(e|E)123.
        * we could use _ in floating point literals in the both notation with the same restriction told in integer literals.
        * we could use hexadecimal but it's rare we use _binary exponent_ p|P in stead of  _exponent_ e|E .

  * _Characters literals_  :
        * forms:  - quoted literals 'C'
                  - hexa notation \uxxxx \ua1235 **4 digits**
                  - ocal notation \ooo  \123 **3 digits**
                  - escaped sequences : \\,\',\",\f,\r,\n...
        * NB: char c = 41; the 41 literal is integer (int) not a character literal form.
  * _String literals_ : Java String must begin and end in the same line there is no line continuation.
  * _Boolean literals_ only two values false , true.

## 6. Types auto conversion , casting , promotion
  NB : we are talking about variables' values not literals values .
  * Java do auto conversion if we have the following conditions
    * the two types are compatible (Characters,Integers,Floating-point are compatible).
    * the destination type is larger than the source(widening conversion).
     ex byte --> short --> int --> long --> float --> double
     ```java
        int a = 100;
        long b = a; // Implicit cast, an int value always fits in a long
     ```
  * We need to do a type casting if we are doing an (narrowing | truncation ) or the types are not compatible
      ```java
        float a = 100.001f;
        int b = (int)a; // Explicit cast, the float could lose info
      ```
  * promotion are the implicit conversion done in expressions.
      * all byte ,short,char operands are promoted to int at any time (even there is no int operand).note that unary operators are excluded from this rule.
      ```java
      short a = 1;
      short b = a++; // there is no promotion
      int c = 12;
      int d = a + c // here the a is promoted to int after we made the operation

      ```
      NB : the following statements cause a compilation error
      ```java

      short a = 10,b=11;
      short c = a + b; // because the result is an int and we are trying to put a larger type into shorter

      ```
      * if one operator is int ,float ,double JVM will promote other operators to this type.
      ```java
      int a = 1;
      short b = 2;
      float c = 1.1f;
      double d = 1.2;
      double z = (a+b)*(c/d);
      // b short ---> int
      // c float ---> double
      // (a+b) int ---> double
      // z is double
      ```

      * promotion is done step by step (operation by operation).
  * No conversion is allowed to or from boolean types.
