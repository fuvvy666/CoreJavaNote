# CoreJavaNote
Notes for JavaSE
- Fundamental Programming Structures in Java

. Java is case sensitive

. The range of the integer types do not depend on the machine on which you will be running the 

Java code

. Add underscores to number literals, such as 1_000_000
 just for human eyes only. Java compiler simply removes them.

. Never use the value of an uninitialized variable.

. "final" to denote a constant

. class constants: create a constant so it's available to multiple methods inside a single 

class. Definition appears outside the main method.

. Math class contains mathematical functions.
  e.g: double y = Math.sqrt(x)

. Math.pow() method's parameters are both of type double.

. Large integer such as 123456789 has more digits than the float type can represent -> lose 

precision

. two values are combined with a binary operator
  If either of the operand is of type double, float or long, the other one will be convert to 

double, float, long.
  Otherwise, both operands will be converted to an int.

. casts: conversion in which loss of information.

. A && B: the truth value of the A has beed determined to be false, then the value for the 

second expression is not calculated.
  A || B: automatically true if the A is true, without evaluating the second expression.

. condition ? expression1 : expression2

. bitwise operator: &("and") |("or") ^("xor") ~("not")    get at individual bits in a number.
  e.g: int fourthBitFromRight = (n & 0b1000) / 0b1000;

. >> and <<: shift a bit pattern to the right or left.
  >>>: fills the top bits with zero. There is no <<< operator.

. += associates right to left
  e.g: a += b += c -> a += (b += c)

. String greeting = "Hello";
  String s = greeting.substring(0,3); // s = "Hel"

. String all = String.join("/", "S", "M", "L", "XL") // all = "S/M/L/XL"

. cannot change the individual characters in a Java string.

. testing strings for equality: (do not use the == to test two string are equal -> it only 

determines whether or not the strings are stored in the same location)
  "Hello".equals("hello") 
  "Hello".equalsIgnoreCase("hello")

. replace a string with another string:
  char greeting = "Hello";
  char* temp = malloc(6);
  strncpy(temp, greeting, 3);
  strncpy(temp + 3, "p!", 3);
  greeting = temp; // greeting = "Help!"

. The char type is a code unit for representing Unicode code points in the UTF-16 coding.
  The length method yields the number of code units required for a given string in the UTF-16 

encoding:
  e.g: String greeting = "Hello";
       int n = greeting.length(); // n = 5
  To get the true length, the number of code points:
  e.g: int cpCount = greeting.codePointCount(0, greeting.length());

. call charAt(n) return the code unit at position n
  e.g: char first = greeting.charAt(0); // first = "H"

. to get the ith code point:
  e.g: int index = greeting.offsetByCodePoints(0,i);
       int cp = greeting.codePointAt(index);

. StringBuilder class
  If you need a build a string from many small pieces.
  First to construct an empty string builder.
  Each time you need to add another part, call the append method
  When you are done building the string, call the toString method.
  Advantages: eliminate the time consuming and waste memory.
  e.g: StringBuilder builder = new StringBuilder();
       builder.append(ch);
       builder.append(str);
       String completedString = builder.toString();

. Scanner class: read the input; need to import java.util.*;
  
  Scanner in = new Scanner(System.in);
  
  System.out.print("What is your name?");
  String name = in.nextLine() // input might contain spaces
  String firstName = in.next(); // read a single word(delimited by whitespace)
  String age = in.nextInt() // read an integer.

. the Scanner class is not suitable for reading a password from a console since the input is 

plainly visible to anyone.
  Console class specifically for this purpose, must read the input a line at a time, no methods 

for reading individuals words or numbers.
  e.g: Console cons = System.console();
       String username = cons.readLine("User name: ");
       char[] passwd = cons.readPassword("Password: ")

. System.out.printf("%8.2f", x); // prints x with a field width of 8 characters and a precision 

of 2 characters. -> the printout contains a leading space and seven characters.
  %d: decimal integer // 159
  %f: fixed-point floating-point // 15.9
  %e: exponential floating-point // 1.59e+01
  %s: string // Hello
  %c: character // H
  %b: boolean // true

. Specify flags control the appearance of the formatted output. 
  e.g: System.out.printf("%,.2f", 10000.0 / 3.0) // 3,333.33

. read from a file: Scanner in = new Scanner(Paths.get("myfile.txt"), "UTF-8");
  write to a file: PrintWriter out = new PrintWriter("myfile.txt", "UTF-8");

. If you construct a Scanner with a file that does not exist or a PrinteWriter with a file name 

that cannot be created, and exception occurs.
  -> Tagging the main method with a throws clause: 
	public static void main(String[] args) throws IOException{....}

. A block can be nested inside another block
  not declare identically named variables in two nested blocks.

. The while loop will never execute if the condition is false at the outset. -> test at the 

top.
  do/while loop: test at the bottom.

. if define a variable inside a for statement, you cannot use its value outside the loop.

. In switch statement, a case label can be type of char, byte, short, or int

. BigInteger class: implements arbitrary-precision integer arithmetic
  BigDecimal class: does the same for floating-point numbers.
  cannot use the familiar mathematical operators such as + and * to combine big numbers.
  e.g: BigInteger a = BigInteger.valueOf(100);
       BigInteger c = a.add(b)
       BigInteger d = c.multiply(b.add(BigInteger.valueOf(2))); // d = c * (b + 2)

. int[] a = new int[100];
  int a[] = new int[100];

. "for each" loop: loop through each element in an array:
  for(int element:a)
     System.out.println(element); // print each element of the array a on separate line.

. A common use to increase the size of an array:
  e.g: luckyNumbers = Arrays.copyOf(luckyNumbers, 2 * luckyNumbers.length)
  the additional elements are filled with 0 if the array contains numbers, false if the array 

contains boolean values.

- Objects and Classes

. The key to making encapsulation work is to have methods never directly access instance fields 

in a class other than their own.

. the most common relationships between classes are:
  1. Dependence
  2. Aggregation: object of class A contain objects of class B.
  3. Inheritance

. try to minimize the number of classes that depend on each other.

. an object variable doesn't acutally contain an object. It only refers to an object.

. local variables are not automatically initialized to null. You must initialize them, either 

by calling new or by setting them to null.

. LocalDate class:
  LocalDate newYearEve = LocalDate.of(1999, 12, 31);
  int year = newYearEve.getYear();  // 1999
  LocalDate aThousandDaysLater = newYearEve.plusDays(1000);
  year = aThousandDaysLater.getYear();   //2002

. The plusDays method does not mutate the object on which it is invoked.
  the .add method is a mutator method -> the state of the object has changed.

. accessor methods: only access objects without modifying them

. a constructor has the same name as the class.
  a class can have more than one constructor.
  a constructor can take zero, one, or more parameters.
  a constructor has no return value
  a constructor is always called with the new operator.

. field accessors: simply return the values of instance fields.

. Mutator methods can perform error checking, whereas code that simply assigns to a field may 

not go into the trouble.

. not to write accessor methods that return references to mutable objects.

. some methods can access the private data of all objects of its class. e.g: equals()

. define an instance field as final: the final field may not be modified again.

. static field: belong to the class, not to any individuals object.

. static method: do not operate on objects. -> don't have "this" parameter

. static factory methods
  LocalDate date = LocalDate.now()
  why use constructor?
  1. cannot give names to constructors.
  2. when use constructor, you cannot vary the type of the constructor object.

. Every class can have a main method for unit testing of classes
  if want to test the Employee class in isolation:
	execute: java Employee

