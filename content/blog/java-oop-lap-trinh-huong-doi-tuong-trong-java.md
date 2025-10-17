---
title: "Java OOP: Lập trình Hướng đối tượng trong Java - Các nguyên lý cơ bản"
date: 2025-10-17
draft: false
description: "Tìm hiểu về lập trình hướng đối tượng trong Java: Class, Object và 4 trụ cột OOP - Kế thừa, Đa hình, Đóng gói với ví dụ chi tiết và dễ hiểu."
categories: ["Programming", "Java", "OOP"]
tags: ["Java", "OOP", "Object-Oriented", "Class", "Object", "Inheritance", "Polymorphism", "Encapsulation"]
author: "Phan Thị Huỳnh Ngọc"
slug: "java-oop-lap-trinh-huong-doi-tuong-trong-java"
---

Chào các bạn,

Ở bài trước, chúng ta đã tìm hiểu về Java và triết lý **"Viết một lần, chạy mọi nơi"**. Hôm nay, chúng ta sẽ đi sâu vào trái tim của Java: **Lập trình Hướng đối tượng** (Object-Oriented Programming - OOP). Đây là một mô hình lập trình giúp tổ chức code logic, dễ quản lý và tái sử dụng hơn.

<!--more-->

## 1. OOP là gì?

**Lập trình hướng đối tượng (OOP)** là một phương pháp lập trình dựa trên khái niệm **"đối tượng"**, chứa cả dữ liệu (thuộc tính) và code (phương thức). OOP mô phỏng thế giới thực, nơi mọi thứ đều là các đối tượng tương tác với nhau. 

Để làm chủ OOP, bạn cần hiểu **5 khái niệm cơ bản** sau:
- 🏗️ **Lớp (Class)**
- 📦 **Đối tượng (Object)**
- 🔗 **Kế thừa (Inheritance)**
- 🎭 **Đa hình (Polymorphism)**
- 🔒 **Đóng gói (Encapsulation)**

## 2. Hai Khái niệm Nền tảng: Class và Object

### 2.1. Lớp (Class) - Bản thiết kế

**Lớp (Class)** là một bản thiết kế, một khuôn mẫu (template) để tạo ra các đối tượng. Nó định nghĩa các thuộc tính (attributes) và hành vi (behaviors) mà đối tượng được tạo ra từ lớp đó sẽ có.

- **Thuộc tính**: Dữ liệu mô tả đối tượng (ví dụ: tên, màu sắc, tuổi)
- **Hành vi**: Các chức năng mà đối tượng có thể thực hiện (ví dụ: chạy, nói, học)

### 2.2. Đối tượng (Object) - Sản phẩm thực tế

**Đối tượng (Object)** là một thực thể được tạo ra từ Lớp. Nó là một thể hiện (instance) cụ thể của Lớp đó và chứa các giá trị cụ thể cho các thuộc tính.

### Ví dụ mã nguồn Class và Object:

```java
// Định nghĩa Class
public class Student {
    // Thuộc tính (attributes)
    private String name;
    private int age;
    private String major;
    
    // Constructor - Phương thức khởi tạo
    public Student(String name, int age, String major) {
        this.name = name;
        this.age = age;
        this.major = major;
    }
    
    // Phương thức (methods) - Hành vi
    public void study() {
        System.out.println(name + " đang học " + major);
    }
    
    public void introduce() {
        System.out.println("Xin chào, tôi là " + name + 
                          ", " + age + " tuổi, học " + major);
    }
    
    // Getter methods
    public String getName() { return name; }
    public int getAge() { return age; }
    public String getMajor() { return major; }
}

// Sử dụng Class để tạo Objects
public class Main {
    public static void main(String[] args) {
        // Tạo các đối tượng từ class Student
        Student student1 = new Student("Ngọc", 20, "Công nghệ thông tin");
        Student student2 = new Student("Minh", 21, "Kế toán");
        
        // Gọi phương thức của các đối tượng
        student1.introduce(); // Output: Xin chào, tôi là Ngọc, 20 tuổi, học Công nghệ thông tin
        student1.study();     // Output: Ngọc đang học Công nghệ thông tin
        
        student2.introduce(); // Output: Xin chào, tôi là Minh, 21 tuổi, học Kế toán
        student2.study();     // Output: Minh đang học Kế toán
    }
}
```

## 3. Bốn Trụ cột của OOP

Sau khi nắm vững Class và Object, chúng ta đến với **4 nguyên lý chính** giúp Java trở nên mạnh mẽ:

### a. 🔗 Kế thừa (Inheritance)

**Kế thừa** cho phép một lớp (gọi là lớp con) kế thừa các thuộc tính và phương thức từ một lớp khác (gọi là lớp cha). Điều này giúp tái sử dụng mã và tạo ra một cấu trúc phân cấp trong các đối tượng.

- **Lớp cha (superclass)** là lớp được kế thừa
- **Lớp con (subclass)** là lớp kế thừa từ lớp cha

#### Ví dụ về Kế thừa:

```java
// Lớp cha
public class Animal {
    protected String name;
    
    public Animal(String name) {
        this.name = name;
    }
    
    public void eat() {
        System.out.println(name + " đang ăn");
    }
    
    public void sleep() {
        System.out.println(name + " đang ngủ");
    }
}

// Lớp con kế thừa từ Animal
public class Dog extends Animal {
    private String breed;
    
    public Dog(String name, String breed) {
        super(name); // Gọi constructor của lớp cha
        this.breed = breed;
    }
    
    // Phương thức riêng của Dog
    public void bark() {
        System.out.println(name + " đang sủa: Gâu gâu!");
    }
    
    // Dog có thể sử dụng phương thức eat() từ Animal
}

// Sử dụng
public class Main {
    public static void main(String[] args) {
        Dog myDog = new Dog("Buddy", "Golden Retriever");
        myDog.eat();   // Kế thừa từ Animal
        myDog.sleep(); // Kế thừa từ Animal  
        myDog.bark();  // Phương thức riêng của Dog
    }
}
```

### b. 🎭 Đa hình (Polymorphism)

**Đa hình** cho phép các đối tượng thuộc các lớp khác nhau có thể gọi các phương thức có tên giống nhau nhưng thực hiện các hành vi khác nhau tùy vào loại đối tượng. Đa hình có thể thực hiện thông qua **overriding** (ghi đè) hoặc **overloading** (nạp chồng).

- **Overriding**: Khi lớp con cung cấp phương thức riêng của mình thay thế phương thức của lớp cha
- **Overloading**: Khi một phương thức có cùng tên nhưng khác tham số

#### Ví dụ về Đa hình (Overriding):

```java
// Lớp cha
public class Animal {
    protected String name;
    
    public Animal(String name) {
        this.name = name;
    }
    
    public void sound() {
        System.out.println(name + " tạo ra âm thanh");
    }
}

// Lớp con ghi đè phương thức sound()
public class Dog extends Animal {
    public Dog(String name) {
        super(name);
    }
    
    @Override
    public void sound() {
        System.out.println(name + " sủa: Gâu gâu!");
    }
}

public class Cat extends Animal {
    public Cat(String name) {
        super(name);
    }
    
    @Override
    public void sound() {
        System.out.println(name + " kêu: Meo meo!");
    }
}

// Sử dụng đa hình
public class Main {
    public static void main(String[] args) {
        Animal myAnimal = new Animal("Động vật");
        Animal myDog = new Dog("Buddy");
        Animal myCat = new Cat("Kitty");
        
        myAnimal.sound(); // Output: Động vật tạo ra âm thanh
        myDog.sound();    // Output: Buddy sủa: Gâu gâu!
        myCat.sound();    // Output: Kitty kêu: Meo meo!
    }
}
```

Lớp Dog và Cat đã ghi đè phương thức `sound()` của lớp Animal, cho phép mỗi đối tượng thực hiện hành vi khác nhau.

### c. 🔒 Đóng gói (Encapsulation)

**Đóng gói** là kỹ thuật ẩn các dữ liệu bên trong lớp và chỉ cung cấp các phương thức công khai (getter, setter) để truy cập và thay đổi chúng. Điều này giúp bảo vệ dữ liệu khỏi việc bị truy cập và thay đổi trái phép, đồng thời dễ dàng kiểm soát việc thay đổi dữ liệu.

- **Getter** là phương thức dùng để lấy giá trị của thuộc tính
- **Setter** là phương thức dùng để thiết lập giá trị cho thuộc tính

#### Ví dụ về Đóng gói:

```java
public class BankAccount {
    // Thuộc tính private - chỉ truy cập được trong class này
    private String accountNumber;
    private double balance;
    private String ownerName;
    
    // Constructor
    public BankAccount(String accountNumber, String ownerName) {
        this.accountNumber = accountNumber;
        this.ownerName = ownerName;
        this.balance = 0.0;
    }
    
    // Getter methods - để truy cập dữ liệu
    public String getAccountNumber() {
        return accountNumber;
    }
    
    public double getBalance() {
        return balance;
    }
    
    public String getOwnerName() {
        return ownerName;
    }
    
    // Setter methods với validation - để thay đổi dữ liệu an toàn
    public void setOwnerName(String ownerName) {
        if (ownerName != null && !ownerName.trim().isEmpty()) {
            this.ownerName = ownerName;
        } else {
            System.out.println("Tên chủ tài khoản không hợp lệ!");
        }
    }
    
    // Phương thức nghiệp vụ với validation
    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            System.out.println("Gửi tiền thành công. Số dư hiện tại: " + balance);
        } else {
            System.out.println("Số tiền gửi phải lớn hơn 0!");
        }
    }
    
    public void withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
            System.out.println("Rút tiền thành công. Số dư hiện tại: " + balance);
        } else {
            System.out.println("Số tiền rút không hợp lệ hoặc không đủ số dư!");
        }
    }
}

// Sử dụng
public class Main {
    public static void main(String[] args) {
        BankAccount account = new BankAccount("123456789", "Ngọc");
        
        // Không thể truy cập trực tiếp: account.balance = 1000000; // Lỗi!
        
        // Phải sử dụng phương thức public
        account.deposit(1000000);
        account.withdraw(200000);
        
        System.out.println("Chủ tài khoản: " + account.getOwnerName());
        System.out.println("Số dư: " + account.getBalance());
    }
}
```

Thuộc tính `balance` là private, chỉ có thể truy cập thông qua các phương thức getter và setter có validation.

## 4. Kết luận

**Lập trình hướng đối tượng (OOP)** là một trong những phương pháp lập trình phổ biến và mạnh mẽ, giúp cải thiện tính tái sử dụng mã nguồn, bảo mật và khả năng bảo trì. Các nguyên lý **Lớp (Class)**, **Đối tượng (Object)**, **Kế thừa (Inheritance)**, **Đa hình (Polymorphism)** và **Đóng gói (Encapsulation)** tạo nên cấu trúc vững chắc cho mọi chương trình Java.

### 🎯 **Tóm tắt các khái niệm:**

| Khái niệm | Mô tả | Lợi ích |
|-----------|-------|---------|
| **Class** | Bản thiết kế cho objects | Tái sử dụng code, tổ chức logic |
| **Object** | Thể hiện cụ thể của class | Mô phỏng thế giới thực |
| **Inheritance** | Lớp con kế thừa lớp cha | Tái sử dụng code, phân cấp logic |
| **Polymorphism** | Nhiều hình thái khác nhau | Linh hoạt, dễ mở rộng |
| **Encapsulation** | Ẩn dữ liệu, kiểm soát truy cập | Bảo mật, dữ liệu an toàn |

Việc hiểu và áp dụng tốt các nguyên lý này sẽ giúp bạn phát triển các ứng dụng Java dễ dàng, bảo mật và có thể mở rộng trong tương lai.

---

💡 **Hy vọng bài viết trên giúp bạn hiểu rõ hơn về Lập trình hướng đối tượng trong Java. Nếu bạn có câu hỏi hoặc muốn tìm hiểu sâu hơn về một trong các nguyên lý này, đừng ngần ngại để lại bình luận dưới bài viết!**

## Tags và từ khóa
`Java OOP` `Object-Oriented Programming` `Class Object` `Inheritance` `Polymorphism` `Encapsulation` `Java Tutorial`
