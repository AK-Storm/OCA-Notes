# Chapter 2 : Operators and Statements

## 1. Operators and operations

  * when we use component assignment we don't need to make casting.
   ```java
    long x = 10;
    int y = 5;
    y = y * x;  // DOES NOT COMPILE long ---> int
    y*= x; // the cast is made automatically

   ```
   * the assignment operator is that the result of the assignment is an expression in and of itself.
   ```java
   long x = 5;
   long y = (x=3); // x has 3 and y has 3

   ```
   * also while using relational operators or equality operators we could have types promotion.
   ```java
   int a = 15;
   long b=18;
   if(a<=b) // here a will be promoted to long before comparing
   if(a==b)// the same thing
   if(a!=b)// the same thing
   ```
   * a instanceof b is an relational operator.
   * short circuit operators && and || are not like & and | because if the first operand is true we the second operand will not be evaluated.

## 2. branching and conditions
   * for ternary expressions only one expression is evaluated
   ```java
      // booleanExpression ? expression1:expression2
      int y = 1;
      int z = 1;
      final int x = y<10 ? y++ : z++;
      System.out.println(y+","+z); // Outputs 2,1
   ```
  * Switch support the following types :
    * int and Integer
    * byte and Byte
    * short and Short
    * char and Character
    * int and Integer
    * String
    * enum values
  * to have a valid switch we have to :
    * the data type for case statements must all match the data type of the switch variable.
    *  the case statement value must also be a literal, enum constant, or final constant variable (final with value).
 NB: notice that boolean type is not supported neither Boolean his wrapper class, the same thing for long
  * since jdk 5 the for-each (enhanced for) is used, but the compiler convert it to a normal for (extra time for the compiler).
  * for-each support only arrays and any class that implements  java.lang.Iterable.
  * we can use label to make branching, but it's not a good practice to use it.
  ```java
    // we prefere to put it in uppercase
   OUT_LABEL : for (int i : ar){
      ...
   }
  ```
