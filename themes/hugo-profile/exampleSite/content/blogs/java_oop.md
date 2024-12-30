---
title: "Lập trình hướng đối tượng trong Java"
date: 2017-10-31T12:00:00+07:00
summary: Lập trình hướng đối tượng (OOP) là một phương pháp lập trình mạnh mẽ và linh hoạt, cho phép lập trình viên tổ chức mã nguồn một cách có cấu trúc và dễ quản lý. OOP không chỉ giúp cải thiện khả năng tái sử dụng mã mà còn làm cho việc bảo trì và mở rộng ứng dụng trở nên dễ dàng hơn. Trong bối cảnh phát triển phần mềm hiện đại, OOP đã trở thành một tiêu chuẩn quan trọng, và Java là một trong những ngôn ngữ lập trình hàng đầu hỗ trợ các nguyên lý này.
image: /images/post/java_oop.jpg 
---

# Lập Trình Hướng Đối Tượng (OOP) trong Java

Lập trình hướng đối tượng (OOP) là một phương pháp lập trình mạnh mẽ và linh hoạt, cho phép lập trình viên tổ chức mã nguồn một cách có cấu trúc và dễ quản lý. OOP không chỉ giúp cải thiện khả năng tái sử dụng mã mà còn làm cho việc bảo trì và mở rộng ứng dụng trở nên dễ dàng hơn. Trong bối cảnh phát triển phần mềm hiện đại, OOP đã trở thành một tiêu chuẩn quan trọng, và Java là một trong những ngôn ngữ lập trình hàng đầu hỗ trợ các nguyên lý này.

Trong bài viết này, chúng ta sẽ tìm hiểu các nguyên lý cơ bản của lập trình hướng đối tượng trong Java và cách Java áp dụng chúng.

## 1. **Lớp (Class) và Đối Tượng (Object)**

### Lớp (Class)

Lớp là một khuôn mẫu (template) để tạo ra các đối tượng. Lớp định nghĩa các thuộc tính (fields) và phương thức (methods) mà đối tượng của lớp đó sẽ có. Lớp là cấu trúc cơ bản trong OOP và mọi đối tượng đều là thể hiện của một lớp.

```java
class Car {
    String color;
    String model;

    void drive() {
        System.out.println("Car is driving");
    }
}
```

### Đối Tượng (Object)

Đối tượng là một thể hiện của lớp. Khi bạn tạo một đối tượng từ lớp, bạn có thể truy cập các thuộc tính và phương thức đã được định nghĩa trong lớp đó.

```java
public class Main {
    public static void main(String[] args) {
        Car myCar = new Car();  // Tạo đối tượng Car
        myCar.color = "Red";
        myCar.model = "Toyota";
        myCar.drive();  // Gọi phương thức drive
    }
}
```

## 2. **Kế Thừa (Inheritance)**

Kế thừa là một tính năng mạnh mẽ của OOP, cho phép một lớp con (subclass) kế thừa các thuộc tính và phương thức từ lớp cha (superclass). Điều này giúp giảm thiểu sự lặp lại mã nguồn và tăng tính tái sử dụng.

```java
class Vehicle {
    void start() {
        System.out.println("Vehicle is starting");
    }
}

class Car extends Vehicle {
    void drive() {
        System.out.println("Car is driving");
    }
}

public class Main {
    public static void main(String[] args) {
        Car myCar = new Car();
        myCar.start();  // Phương thức kế thừa từ Vehicle
        myCar.drive();  // Phương thức riêng của Car
    }
}
```

Trong ví dụ trên, lớp `Car` kế thừa phương thức `start()` từ lớp `Vehicle`, nhưng cũng có thể định nghĩa các phương thức riêng của mình.

## 3. **Đa Hình (Polymorphism)**

Tính đa hình là một trong những tính năng quan trọng của lập trình hướng đối tượng (OOP). Nó cho phép các đối tượng của các lớp khác nhau có thể được xử lý thông qua một interface chung. Đặc biệt, đa hình cho phép các đối tượng của các lớp khác nhau có thể thực thi các phương thức có cùng tên nhưng thực hiện hành động khác nhau. Điều này giúp mã trở nên linh hoạt, dễ mở rộng và bảo trì hơn. Có 2 loại đa hình trong Java:

### Đa hình thông qua kế thừa (Compile-time Polymorphism) 
   Đây là loại đa hình được thực hiện tại thời điểm biên dịch. Trong Java, đa hình ở thời điểm biên dịch thường được thực hiện qua **phương thức nạp chồng** (method overloading) và **toán tử nạp chồng** (operator overloading). Tuy nhiên, Java không hỗ trợ toán tử nạp chồng, nhưng có thể thực hiện nạp chồng phương thức trong cùng một lớp hoặc lớp con.

   Ví dụ:
   ```java
   class Calculator {
       public int add(int a, int b) {
           return a + b;
       }

       public double add(double a, double b) {
           return a + b;
       }
   }

   public class Main {
       public static void main(String[] args) {
           Calculator calc = new Calculator();
           System.out.println(calc.add(2, 3));       // In ra 5
           System.out.println(calc.add(2.5, 3.7));   // In ra 6.2
       }
   }
   ```

   Trong ví dụ trên, phương thức `add` có thể chấp nhận hai tham số `int` hoặc `double`, điều này cho thấy tính đa hình của phương thức nạp chồng.

### Đa hình thông qua kế thừa (Runtime Polymorphism)
   Đây là loại đa hình được thực hiện tại thời điểm chạy, thông qua cơ chế **override** phương thức của lớp con. Khi một phương thức trong lớp con có cùng tên và chữ ký với phương thức trong lớp cha, phương thức trong lớp con sẽ "ghi đè" phương thức trong lớp cha. Tính đa hình ở đây cho phép một đối tượng lớp con thực thi phương thức của lớp cha nhưng với hành động của lớp con.

   Ví dụ:
   ```java
   class Animal {
       public void sound() {
           System.out.println("Animal makes a sound");
       }
   }

   class Dog extends Animal {
       @Override
       public void sound() {
           System.out.println("Dog barks");
       }
   }

   class Cat extends Animal {
       @Override
       public void sound() {
           System.out.println("Cat meows");
       }
   }

   public class Main {
       public static void main(String[] args) {
           Animal myAnimal = new Animal();
           Animal myDog = new Dog();
           Animal myCat = new Cat();

           myAnimal.sound();  
           myDog.sound();     
           myCat.sound();    
       }
   }
   ```

   Trong ví dụ trên, mặc dù tất cả các đối tượng đều có kiểu `Animal`, phương thức `sound` được thực thi khác nhau tùy theo đối tượng thực tế (Dog, Cat hoặc Animal). Đây chính là tính đa hình trong OOP.

## Lợi ích của đa hình:
- **Tăng tính linh hoạt**: Chúng ta có thể viết mã xử lý các đối tượng của nhiều lớp khác nhau mà không cần phải biết chính xác lớp của đối tượng.
- **Mở rộng dễ dàng**: Việc thêm các lớp mới vào hệ thống mà không làm thay đổi mã hiện tại.
- **Dễ bảo trì**: Mã trở nên dễ bảo trì hơn khi các thay đổi chỉ cần thực hiện ở các lớp con thay vì thay đổi mã trong toàn bộ chương trình.

Tính đa hình là một phần không thể thiếu trong lập trình hướng đối tượng, giúp các lập trình viên xây dựng các ứng dụng dễ bảo trì, mở rộng và linh hoạt.

## 4. **Đóng Gói (Encapsulation)**

Đóng gói là cơ chế bảo vệ dữ liệu bên trong đối tượng, ngăn chặn sự truy cập trực tiếp từ bên ngoài và chỉ cung cấp các phương thức công khai để thao tác với dữ liệu. Điều này giúp bảo vệ dữ liệu và giữ mã nguồn sạch sẽ hơn.

```java
class Person {
    private String name;
    private int age;

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
        if (age > 0) {
            this.age = age;
        }
    }
}

public class Main {
    public static void main(String[] args) {
        Person person = new Person();
        person.setName("John");
        person.setAge(25);
        System.out.println(person.getName() + " is " + person.getAge() + " years old");
    }
}
```

Trong ví dụ trên, thuộc tính `name` và `age` được đóng gói dưới dạng private, chỉ có thể truy cập và thay đổi thông qua các phương thức getter và setter công khai.

## 5. **Trừu Tượng (Abstraction)**

Trừu tượng là quá trình che giấu chi tiết thực thi và chỉ cung cấp các phương thức và giao diện mà người dùng có thể sử dụng. Java hỗ trợ trừu tượng qua lớp trừu tượng (abstract class) và giao diện (interface).

### Lớp trừu tượng (Abstract Class)

```java
abstract class Animal {
    abstract void sound();
}

class Dog extends Animal {
    @Override
    void sound() {
        System.out.println("Dog barks");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal myDog = new Dog();
        myDog.sound();  // Dog barks
    }
}
```

### Giao diện (Interface)

```java
interface Animal {
    void sound();
}

class Dog implements Animal {
    @Override
    public void sound() {
        System.out.println("Dog barks");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal myDog = new Dog();
        myDog.sound();  // Dog barks
    }
}
```

### Tóm Tắt Lập Trình Hướng Đối Tượng trong Java

- **Lớp và Đối Tượng**: Mọi ứng dụng Java đều được xây dựng từ các lớp và đối tượng.
- **Kế Thừa**: Giúp tái sử dụng mã và mở rộng các lớp hiện có.
- **Đa Hình**: Cho phép một phương thức hoặc đối tượng có thể có nhiều hành vi khác nhau.
- **Đóng Gói**: Giúp bảo vệ dữ liệu và quản lý cách thức truy cập và thay đổi dữ liệu.
- **Trừu Tượng**: Giúp ẩn các chi tiết thực thi và chỉ cung cấp các giao diện cho người dùng.

Java với các nguyên lý OOP này giúp lập trình viên có thể xây dựng những ứng dụng mạnh mẽ, dễ bảo trì, dễ mở rộng và bảo mật cao.
