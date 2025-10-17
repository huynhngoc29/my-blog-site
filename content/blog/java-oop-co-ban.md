---
title: "Java OOP: Lập trình Hướng đối tượng trong Java - Các nguyên lý cơ bản"
date: 2025-10-16
draft: false
description: "Tìm hiểu về lập trình hướng đối tượng trong Java: Class, Object và 4 trụ cột OOP - Kế thừa, Đa hình, Đóng gói với ví dụ chi tiết và dễ hiểu."
categories: ["Programming", "Java", "OOP"]
tags: ["Java", "OOP", "Object-Oriented", "Class", "Object", "Inheritance", "Polymorphism", "Encapsulation"]
author: "Phan Thị Huỳnh Ngọc"
slug: "java-oop-co-ban"
---

Chào các bạn,

Ở bài trước, chúng ta đã tìm hiểu về Java và triết lý **"Viết một lần, chạy mọi nơi"**. Hôm nay, chúng ta sẽ đi sâu vào trái tim của Java: **Lập trình Hướng đối tượng (Object-Oriented Programming - OOP)**. Đây là một mô hình lập trình giúp tổ chức code logic, dễ quản lý và tái sử dụng hơn.

<!--more-->

## 1. OOP là gì?

**Lập trình hướng đối tượng (OOP)** là một phương pháp lập trình dựa trên khái niệm **"đối tượng"**, chứa cả dữ liệu (thuộc tính) và code (phương thức). OOP mô phỏng thế giới thực, nơi mọi thứ đều là các đối tượng tương tác với nhau. 

Để làm chủ OOP, bạn cần hiểu **5 khái niệm cơ bản** sau: **Lớp (Class)**, **Đối tượng (Object)**, và **4 Trụ cột chính**: **Đóng gói (Encapsulation)**, **Kế thừa (Inheritance)**, **Đa hình (Polymorphism)**.

### 🎯 **Ưu điểm của OOP:**
- ✅ **Tái sử dụng code**: Viết một lần, dùng nhiều nơi
- ✅ **Dễ bảo trì**: Code được tổ chức rõ ràng theo đối tượng
- ✅ **Bảo mật**: Ẩn dữ liệu quan trọng qua Encapsulation
- ✅ **Mở rộng dễ dàng**: Thêm tính năng mới không ảnh hưởng code cũ

## 2. Hai Khái niệm Nền tảng: Class và Object

### 🏗️ **2.1. Lớp (Class) - Bản thiết kế**

**Lớp (Class)** là một bản thiết kế, một khuôn mẫu (template) để tạo ra các đối tượng. Nó định nghĩa các thuộc tính (attributes) và hành vi (behaviors) mà đối tượng được tạo ra từ lớp đó sẽ có.

- **Thuộc tính**: Dữ liệu mô tả đối tượng (ví dụ: tên, màu sắc, tuổi).
- **Hành vi**: Các chức năng mà đối tượng có thể thực hiện (ví dụ: chạy, nói, học).

### 🎭 **2.2. Đối tượng (Object) - Sản phẩm thực tế**

**Đối tượng (Object)** là một thực thể được tạo ra từ Lớp. Nó là một thể hiện (instance) cụ thể của Lớp đó và chứa các giá trị cụ thể cho các thuộc tính.

### 💻 **Ví dụ mã nguồn Class và Object:**

```java
// Định nghĩa Class Student
public class Student {
    // Thuộc tính (Properties/Attributes)
    private String name;
    private int age;
    private String studentId;
    private double gpa;
    
    // Constructor - Phương thức khởi tạo
    public Student(String name, int age, String studentId) {
        this.name = name;
        this.age = age;
        this.studentId = studentId;
        this.gpa = 0.0; // GPA mặc định
    }
    
    // Phương thức (Methods/Behaviors)
    public void study(String subject) {
        System.out.println(name + " đang học môn " + subject);
    }
    
    public void takeExam(String subject, double score) {
        System.out.println(name + " đã thi môn " + subject + " và đạt " + score + " điểm");
        updateGPA(score);
    }
    
    private void updateGPA(double score) {
        // Logic tính GPA đơn giản
        this.gpa = (this.gpa + score) / 2;
        System.out.println("GPA hiện tại của " + name + ": " + String.format("%.2f", gpa));
    }
    
    public void displayInfo() {
        System.out.println("=== THÔNG TIN SINH VIÊN ===");
        System.out.println("Tên: " + name);
        System.out.println("Tuổi: " + age);
        System.out.println("Mã SV: " + studentId);
        System.out.println("GPA: " + String.format("%.2f", gpa));
        System.out.println("========================");
    }
    
    // Getter và Setter methods
    public String getName() { return name; }
    public void setName(String name) { this.name = name; }
    
    public int getAge() { return age; }
    public void setAge(int age) { this.age = age; }
    
    public String getStudentId() { return studentId; }
    public double getGpa() { return gpa; }
}

// Sử dụng Class để tạo Objects
public class StudentDemo {
    public static void main(String[] args) {
        // Tạo các Objects từ Class Student
        Student student1 = new Student("Nguyễn Văn An", 20, "SV001");
        Student student2 = new Student("Trần Thị Bình", 19, "SV002");
        Student student3 = new Student("Lê Văn Chi", 21, "SV003");
        
        // Gọi các phương thức của Objects
        student1.study("Java Programming");
        student1.takeExam("Java Programming", 8.5);
        student1.displayInfo();
        
        System.out.println(); // Dòng trống
        
        student2.study("Data Structures");
        student2.takeExam("Data Structures", 9.0);
        student2.displayInfo();
        
        System.out.println(); // Dòng trống
        
        student3.study("Algorithms");
        student3.takeExam("Algorithms", 7.5);
        student3.displayInfo();
        
        // So sánh Objects
        System.out.println("Sinh viên có GPA cao nhất:");
        if (student1.getGpa() > student2.getGpa() && student1.getGpa() > student3.getGpa()) {
            System.out.println(student1.getName() + " - GPA: " + String.format("%.2f", student1.getGpa()));
        } else if (student2.getGpa() > student3.getGpa()) {
            System.out.println(student2.getName() + " - GPA: " + String.format("%.2f", student2.getGpa()));
        } else {
            System.out.println(student3.getName() + " - GPA: " + String.format("%.2f", student3.getGpa()));
        }
    }
}
```

**🔍 Giải thích:**
- **Class Student**: Là bản thiết kế định nghĩa cấu trúc của một sinh viên
- **Objects (student1, student2, student3)**: Là các thể hiện cụ thể của lớp Student
- Mỗi object có dữ liệu riêng nhưng cùng cấu trúc và hành vi

## 3. Bốn Trụ cột của OOP

Sau khi nắm vững Class và Object, chúng ta đến với **4 nguyên lý chính** giúp Java trở nên mạnh mẽ:

### 🔗 **a. Kế thừa (Inheritance)**

**Kế thừa** cho phép một lớp (gọi là lớp con) kế thừa các thuộc tính và phương thức từ một lớp khác (gọi là lớp cha). Điều này giúp tái sử dụng mã và tạo ra một cấu trúc phân cấp trong các đối tượng.

- **Lớp cha (superclass)** là lớp được kế thừa.
- **Lớp con (subclass)** là lớp kế thừa từ lớp cha.

#### **Ví dụ về Kế thừa:**

```java
// Lớp cha (Parent class)
class Animal {
    protected String name;
    protected int age;
    
    public Animal(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    public void eat() {
        System.out.println(name + " đang ăn");
    }
    
    public void sleep() {
        System.out.println(name + " đang ngủ");
    }
    
    public void displayInfo() {
        System.out.println("Tên: " + name + ", Tuổi: " + age);
    }
}

// Lớp con (Child class) kế thừa từ Animal
class Dog extends Animal {
    private String breed;
    
    public Dog(String name, int age, String breed) {
        super(name, age); // Gọi constructor của lớp cha
        this.breed = breed;
    }
    
    // Phương thức riêng của Dog
    public void bark() {
        System.out.println(name + " đang sủa: Woof! Woof!");
    }
    
    public void playFetch() {
        System.out.println(name + " đang chơi bắt bóng");
    }
    
    // Ghi đè phương thức của lớp cha
    @Override
    public void displayInfo() {
        super.displayInfo(); // Gọi phương thức của lớp cha
        System.out.println("Giống: " + breed);
    }
}
```

**Lớp Dog kế thừa phương thức eat() từ lớp Animal.**

### 🎭 **b. Đa hình (Polymorphism)**

**Đa hình** cho phép các đối tượng thuộc các lớp khác nhau có thể gọi các phương thức có tên giống nhau nhưng thực hiện các hành vi khác nhau tùy vào loại đối tượng. Đa hình có thể thực hiện thông qua **overriding** (ghi đè) hoặc **overloading** (nạp chồng).

- **Overriding**: Khi lớp con cung cấp phương thức riêng của mình thay thế phương thức của lớp cha.
- **Overloading**: Khi một phương thức có cùng tên nhưng khác tham số.

#### **Ví dụ về Đa hình (Overriding):**

```java
// Lớp cha
class Animal {
    protected String name;
    
    public Animal(String name) {
        this.name = name;
    }
    
    // Phương thức sẽ được override bởi các lớp con
    public void makeSound() {
        System.out.println(name + " tạo ra âm thanh nào đó");
    }
}

// Các lớp con override phương thức makeSound()
class Dog extends Animal {
    public Dog(String name) {
        super(name);
    }
    
    @Override
    public void makeSound() {
        System.out.println(name + " sủa: Woof! Woof!");
    }
}

class Cat extends Animal {
    public Cat(String name) {
        super(name);
    }
    
    @Override
    public void makeSound() {
        System.out.println(name + " kêu: Meow! Meow!");
    }
}
```

**Lớp Dog đã ghi đè phương thức sound() của lớp Animal, cho phép phương thức sound() của đối tượng myDog thực hiện hành vi khác với myAnimal.**

### 🔒 **c. Đóng gói (Encapsulation)**

**Đóng gói** là kỹ thuật ẩn các dữ liệu bên trong lớp và chỉ cung cấp các phương thức công khai (getter, setter) để truy cập và thay đổi chúng. Điều này giúp bảo vệ dữ liệu khỏi việc bị truy cập và thay đổi trái phép, đồng thời dễ dàng kiểm soát việc thay đổi dữ liệu.

- **Getter** là phương thức dùng để lấy giá trị của thuộc tính.
- **Setter** là phương thức dùng để thiết lập giá trị cho thuộc tính.

#### **Ví dụ về Đóng gói:**

```java
public class Person {
    // Thuộc tính private - không thể truy cập trực tiếp từ bên ngoài
    private String name;
    private int age;
    
    // Constructor
    public Person(String name, int age) {
        this.name = name;
        setAge(age); // Sử dụng setter để validation
    }
    
    // Getter method để lấy giá trị
    public String getName() {
        return name;
    }
    
    public int getAge() {
        return age;
    }
    
    // Setter method với validation
    public void setName(String name) {
        if (name != null && !name.trim().isEmpty()) {
            this.name = name;
        } else {
            System.out.println("Tên không hợp lệ!");
        }
    }
    
    public void setAge(int age) {
        if (age >= 0 && age <= 120) {
            this.age = age;
        } else {
            System.out.println("Tuổi phải từ 0 đến 120!");
        }
    }
    
    public void displayInfo() {
        System.out.println("Tên: " + name + ", Tuổi: " + age);
    }
}
```

**name là thuộc tính private, chỉ có thể truy cập thông qua các phương thức getter và setter.**

## 4. Kết luận

**Lập trình hướng đối tượng (OOP)** là một trong những phương pháp lập trình phổ biến và mạnh mẽ, giúp cải thiện tính tái sử dụng mã nguồn, bảo mật và khả năng bảo trì. Các nguyên lý **Lớp (Class)**, **Đối tượng (Object)**, **Kế thừa (Inheritance)**, **Đa hình (Polymorphism)** và **Đóng gói (Encapsulation)** tạo nên cấu trúc vững chắc cho mọi chương trình Java.

### 🎯 **Tóm tắt 4 trụ cột OOP:**

| Nguyên lý | Mô tả | Lợi ích chính |
|-----------|--------|---------------|
| **🔗 Inheritance** | Lớp con kế thừa từ lớp cha | Tái sử dụng code, cấu trúc phân cấp |
| **🎭 Polymorphism** | Cùng tên method, khác hành vi | Linh hoạt, dễ mở rộng |
| **🔒 Encapsulation** | Ẩn dữ liệu, public methods | Bảo mật, kiểm soát truy cập |

### 💡 **Lời khuyên khi áp dụng OOP:**
- ✅ **Thiết kế trước khi code**: Vẽ sơ đồ class, xác định mối quan hệ
- ✅ **Tuân thủ nguyên tắc**: Single Responsibility, DRY (Don't Repeat Yourself)
- ✅ **Sử dụng naming convention**: Class viết hoa, method camelCase
- ✅ **Comment và document**: Giải thích logic phức tạp

**Việc hiểu và áp dụng tốt các nguyên lý này sẽ giúp bạn phát triển các ứng dụng Java dễ dàng, bảo mật và có thể mở rộng trong tương lai.**

---

💡 **Hy vọng bài viết trên giúp bạn hiểu rõ hơn về Lập trình hướng đối tượng trong Java. Nếu bạn có câu hỏi hoặc muốn tìm hiểu sâu hơn về một trong các nguyên lý này, đừng ngần ngại để lại bình luận dưới bài viết!**

## Tags và từ khóa SEO
`Lập trình hướng đối tượng trong Java` `OOP trong Java` `Java class object inheritance` `Polymorphism trong Java` `Encapsulation Java` `Java tutorial`
