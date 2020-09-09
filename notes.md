# Java Virtual Machine

It is an _abstract computing machine_

- Instruction set &rarr; Java bytecode
- Manipulates memory at runtime

**Core Responsibilities**

- Loading and interpreting Java bytecode
- Security
- Automatic memory management

### Just-in-time (JIT) Compilation

- Identify frequently exected bytecode: hotpots
- JIT compiler converts "hot spots" to machine code
- Cache machine code
- Cached machine code &rarr; faster execution
- Also called dynamic compilation

# Java main() method

- Program starts with main()
- java HelloWorld
  - JVM loads bytecodes of HelloWorld.class into memory
  - Invokes main()
- Must be declared as **public**, **static** and **void**
- From main() we invoke other code
- Program ends with main()

# OOP Concepts

- Private variables with getter and setter
- Getter and setter to update the values
- Constructor to create the values

# Access Modifiers

### 4 types of Access modifers

- **private**  
  Can only be accessed by the class itself
- **protected**  
  Can be accessed by classes within the same package, or by inheritance
- **public**  
  Can be accessed anywhere in the application
- **\<package>**  
  \<package> is the default Access modifier, can be accessed within the same package  
  Modifers can be used with _class_, _variable_, _methods_ and _constructor_

# Abstraction

The **abstract** method/class is the process of hiding information. Once a class is mark as abstract, we can't create an instance of the class.

Any class that extends an abstract class should provide an implementation for all the methods in the abstract class.

# Interface

Interface can only have abstract methods. Variables in an interface are by default final

None of the methods will have any implementation. All methods are abstract.  
**Advantages**

- Multiple inheritance
- Complete Abstraction

# Polymorphism

2 types of polymorphism

- Method overloading (Compile time polymorphism)

```Java
class DemoOverload{
    public int add(int x, int y){  //method 1
    return x+y;
    }

    public int add(int x, int y, int z){ //method 2
    return x+y+z;
    }

    public int add(double x, int y){ //method 3
    return (int)x+y;
    }

    public int add(int x, double y){ //method 4
    return x+(int)y;
    }
}

class Test{
    public static void main(String[] args){
    DemoOverload demo=new DemoOverload();
    System.out.println(demo.add(2,3));      //method 1 called
    System.out.println(demo.add(2,3,4));    //method 2 called
    System.out.println(demo.add(2,3.4));    //method 4 called
    System.out.println(demo.add(2.5,3));    //method 3 called
    }
}
```

- Method overriding (Runtime polymorphism)

```Java
class Vehicle{
    public void move(){
    System.out.println(“Vehicles can move!!”);
    }
}

class MotorBike extends Vehicle{
    public void move(){
    System.out.println(“MotorBike can move and accelerate too!!”);
    }
}

class Test{
    public static void main(String[] args){
    Vehicle vh=new MotorBike();
    vh.move();    // prints MotorBike can move and accelerate too!!
    vh=new Vehicle();
    vh.move();    // prints Vehicles can move!!
    }
}
```

# Exception Handling

**Exception is a class**

## Compile Time Errors

- Cannot find symbol
- Incompatible Types
- Invalid Method Declaration
- this cannot be used in a static context

```Java
	if (expectedSalary < 10000) {
			throw new InvalidSalaryException("Registration Failed. Salary cannot be less than 10000.");
		} else {
			System.out.println("Registration Successful");
		}
```

```Java

public class InvalidSalaryException extends Exception {
	public InvalidSalaryException(String message) {
		super(message);
	}
}
```

By declaring **throws** keyword on a method, the compiler will expect the programme that is calling the method to handle the exception instead:

```Java
import java.io.FileInputStream;

public class CheckedException {
  void readFile() throws FileNotFoundException{
    FileInputStream fis = new FileInputStream("");
  }
  public static void main(String[] args){
    CheckedException ce = new CheckedException();
    try{
      ce.readFile();
    }
    catch(FileNotFoundException e){
      System.out.println("File Not Found");
    }
  }
}
```

## Logical Errors

```Java
int i = 567;
byte b = (byte) i;
System.out.println(b*14);
```

- Expecting 567 x 14 but casted 567 with byte

## Runtime Errors

Such exceptions will cause:

- Abnormal termination of a program
- Unfriendly error message to the end user
- Improper shutdown of the resource

# Collections Framework

- List
  - ArrayList
  - LinkedList
- Set
  - HashSet
    - LinkedHashSet
  - SortedSet
    - TreeSet
- Queue
  - PriorityQueue
- Map
  - HashMap
    - LinkedHashMap
  - SortedMap
    - TreeMap
- Legacy
  - Vector
  - Hashtable

## ArrayList

Fast access, it can internally use the array index to locate an object.  
Insertion and deletion is slow

- Not a great data structure if doing many insertion and deletion
- Use when alot of read operations
- Default Capacity: 10

If it goes past the default capacity, it will create another array and copy over the elements into the new array. Good practice - to initialize with a size

```Java
List<String> list = new ArrayList<String>();
```

## LinkedList

Stores elements in the form of nodes. Each node will have 3 fields namely:

1. Points to the previous node
2. Store actual object
3. Points to the next node  
   The advantage of linked list is **deletion and insertion** are very fast  
   The disadvantage are it takes more memory and slow random access.

```Java
List<String> list = new LinkedList<String>();
```

## Set

Is a collection or data structure where duplicates are not allowed.  
Elements stored in a set are unordered and _Collections.sort_ will only work on Lists.  
A LinkedHashSet will retain the order of the elements that was put into the set  
A TreeHashSet will sort the elements in ascending order

```Java
Set<String> linkedSet = new LinkedHashSet<>();
Set<String> treeSet = new TreeSet<>();
```

## Iterator

Iterator is an interface in the Collections framework that lets you iterator through the elements of the collection:

```Java
Set<Integer> set = new TreeSet<>();
set.add(10);
set.add(20);
set.add(30);
Iterator<Integer> itr = set.iterator();
while(itr.hasNext()){
  System.out.println(itr.next());
  itr.remove();
}
System.out.println(set);
```

```bash
Output:
10
20
30
[]
```

## ListIterator vs Iterator

| Basis For Comparison | Iterator                                                                     | ListIterator                                                                                         |
| -------------------- | ---------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| Basic                | Iterator can traverse the elements in a collection only in forward direction | ListIterator can traverse the elements in a collection in forward as well as the backwards direction |
| Add                  | Iterator is unable to add elements to a collection.                          | ListIteror can add elements to a collection.                                                         |
| Modify               | Iterator can not modify the elements in a collection.                        | ListIterator can modify the elements in a collection using set().                                    |
| Traverse             | Iterator can traverse Map, List and Set.                                     | ListIterator can traverse List objects only.                                                         |
| Index                | Iterator has no method to obtain an index of the element in a collection.    | Using ListIterator, you can obtain an index of the element in a collection.                          |
