---
title: "Cấu trúc cơ bản của một chương trình Java"
date: 2025-10-15
draft: false
description: "Tìm hiểu về cấu trúc cơ bản của chương trình Java, các kiểu dữ liệu cơ bản, cách khai báo và sử dụng biến trong Java với ví dụ chi tiết."
categories: ["Programming", "Java", "Basics"]
tags: ["Java", "Basic Syntax", "Data Types", "Variables", "Hello World", "Programming Fundamentals"]
author: "Phan Thị Huỳnh Ngọc"
slug: "cau-truc-co-ban-cua-mot-chuong-trinh-java"
---

Sau khi đã tìm hiểu về Java là gì, hôm nay chúng ta sẽ đi sâu vào **cấu trúc cơ bản của một chương trình Java**. Đây là nền tảng quan trọng mà bạn cần nắm vững để có thể viết và hiểu các chương trình Java phức tạp hơn.

<!--more-->

## 2.1 Cấu trúc một chương trình Java

Một chương trình Java cơ bản có thể khá đơn giản, nhưng nó phải tuân thủ một cấu trúc cụ thể. Chương trình Java luôn bắt đầu từ một **lớp (class)**, và một chương trình Java cần có **phương thức main** để thực thi.

Dưới đây là ví dụ đơn giản minh họa chương trình **"Hello World"** trong Java:

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Xin chào các bạn, đây là chương trình đầu tiên của tôi!");
    }
}
```

### 📝 **Giải thích chi tiết:**

#### 🏷️ **`public class HelloWorld`:**
- **`public`**: Từ khóa này cho phép lớp HelloWorld có thể được truy cập từ bất kỳ đâu trong chương trình.
- **`class`**: Từ khóa khai báo một lớp. Trong Java, tất cả mã nguồn đều phải được chứa trong lớp.
- **`HelloWorld`**: Tên của lớp, thường được đặt theo quy ước **CamelCase**, viết hoa chữ cái đầu tiên của mỗi từ. Tên lớp phải trùng với tên file chứa chương trình (ở đây là `HelloWorld.java`).

#### 🚀 **`public static void main(String[] args)`:**
- **`public`**: Từ khóa này cho phép phương thức main có thể được gọi từ bên ngoài lớp.
- **`static`**: Phương thức main phải là static, vì nó là điểm bắt đầu của chương trình và không cần tạo đối tượng của lớp để gọi phương thức này.
- **`void`**: Kiểu trả về của phương thức main. `void` có nghĩa là phương thức này không trả về giá trị nào.
- **`String[] args`**: Đây là một mảng các đối tượng kiểu String, cho phép nhận các đối số từ dòng lệnh khi chạy chương trình.

#### 🖨️ **`System.out.println("Xin chào các bạn, đây là chương trình đầu tiên của tôi!");`**
- **`System.out`**: Đối tượng `out` của lớp System, được sử dụng để xuất dữ liệu ra màn hình console.
- **`println()`**: Phương thức `println()` in chuỗi vào màn hình và chuyển dòng.

## 2.2 Các kiểu dữ liệu cơ bản trong Java

Trong Java, dữ liệu được phân thành các **kiểu cơ bản (primitive types)** và **kiểu tham chiếu (reference types)**. Các kiểu cơ bản trong Java là những kiểu dữ liệu cơ bản mà ngôn ngữ này hỗ trợ. Dưới đây là những kiểu dữ liệu cơ bản:

### 🔢 **`int`: Số nguyên**
- **Mục đích**: Dùng để lưu trữ các số nguyên.
- **Kích thước**: 4 byte.
- **Phạm vi**: -2,147,483,648 đến 2,147,483,647

```java
int age = 25;
int year = 2024;
System.out.println("Tuổi: " + age);
System.out.println("Năm: " + year);
```

### 📊 **`double`: Số thực**
- **Mục đích**: Dùng để lưu trữ các số thực (số có dấu thập phân).
- **Kích thước**: 8 byte.
- **Độ chính xác**: Khoảng 15-17 chữ số thập phân

```java
double price = 99.99;
double pi = 3.14159;
System.out.println("Giá sản phẩm: $" + price);
System.out.println("Số Pi: " + pi);
```

### 🔤 **`char`: Ký tự**
- **Mục đích**: Dùng để lưu trữ một ký tự.
- **Kích thước**: 2 byte.
- **Lưu ý**: Sử dụng dấu nháy đơn `''`

```java
char grade = 'A';
char symbol = '@';
System.out.println("Điểm: " + grade);
System.out.println("Ký hiệu: " + symbol);
```

### ✅ **`boolean`: Logic**
- **Mục đích**: Dùng để lưu trữ giá trị `true` hoặc `false`.
- **Kích thước**: 1 bit.
- **Ứng dụng**: Kiểm tra điều kiện, cờ trạng thái

```java
boolean isStudent = true;
boolean hasLicense = false;
System.out.println("Là sinh viên: " + isStudent);
System.out.println("Có bằng lái: " + hasLicense);
```

### 📝 **`String`: Chuỗi ký tự**
- **Lưu ý**: Mặc dù không phải là kiểu dữ liệu cơ bản (nó là một lớp trong Java), nhưng String thường được coi là một kiểu cơ bản trong Java vì sự sử dụng phổ biến của nó.
- **Sử dụng**: Dấu nháy kép `""`

```java
String name = "Nguyễn Văn An";
String message = "Chào mừng đến với Java!";
System.out.println("Tên: " + name);
System.out.println("Thông báo: " + message);
```

## 2.3 Khai báo và sử dụng biến

**Biến** trong Java được sử dụng để lưu trữ dữ liệu. Mỗi biến phải có một kiểu dữ liệu và có thể thay đổi giá trị trong quá trình thực thi chương trình. Để khai báo một biến, bạn cần chỉ định kiểu dữ liệu và tên của biến.

### 📋 **Cấu trúc khai báo biến:**
```java
<kiểu dữ liệu> <tên biến> = <giá trị>;
```

### 🌟 **Ví dụ khai báo biến:**

```java
public class VariableExample {
    public static void main(String[] args) {
        // Khai báo và gán giá trị
        int studentCount = 30;
        double averageScore = 8.5;
        char classGrade = 'A';
        boolean isActive = true;
        String schoolName = "Trường THPT ABC";
        
        // In thông tin
        System.out.println("=== THÔNG TIN LỚP HỌC ===");
        System.out.println("Tên trường: " + schoolName);
        System.out.println("Số học sinh: " + studentCount);
        System.out.println("Điểm trung bình: " + averageScore);
        System.out.println("Xếp loại: " + classGrade);
        System.out.println("Đang hoạt động: " + isActive);
    }
}
```

### 🔄 **Sử dụng biến:** 
Sau khi khai báo, bạn có thể sử dụng biến để thực hiện các phép toán hoặc in giá trị ra màn hình:

```java
public class Calculator {
    public static void main(String[] args) {
        // Khai báo biến
        int a = 10;
        int b = 5;
        
        // Thực hiện phép toán
        int sum = a + b;        // Phép cộng
        int difference = a - b; // Phép trừ
        int product = a * b;    // Phép nhân
        double quotient = (double)a / b; // Phép chia
        
        // Hiển thị kết quả
        System.out.println("Số thứ nhất: " + a);
        System.out.println("Số thứ hai: " + b);
        System.out.println("Tổng: " + sum);
        System.out.println("Hiệu: " + difference);
        System.out.println("Tích: " + product);
        System.out.println("Thương: " + quotient);
    }
}
```

### ⚠️ **Lưu ý khi sử dụng biến:**

#### 🚨 **Biến phải được khai báo trước khi sử dụng:**
Trong Java, bạn không thể sử dụng một biến trước khi khai báo nó.

```java
// ❌ SAI: Biến chưa được khai báo
System.out.println(myVariable);
int myVariable = 10;

// ✅ ĐÚNG: Khai báo trước khi sử dụng
int myVariable = 10;
System.out.println(myVariable);
```

#### 🔒 **Tính bất biến của biến kiểu `final`:**
Nếu bạn khai báo một biến với từ khóa `final`, giá trị của biến đó không thể thay đổi sau khi được gán.

```java
final double PI = 3.14159;
final String COMPANY_NAME = "ABC Corporation";

// ❌ Không thể thay đổi giá trị
// PI = 3.14; // Lỗi biên dịch
```

### 🎯 **Quy tắc đặt tên biến:**

| Quy tắc | Ví dụ đúng | Ví dụ sai |
|---------|------------|-----------|
| Bắt đầu bằng chữ cái, `_` hoặc `$` | `name`, `_count`, `$value` | `2name`, `-value` |
| Không chứa khoảng trắng | `firstName`, `student_age` | `first name` |
| Phân biệt hoa thường | `Name` ≠ `name` | |
| Không trùng từ khóa Java | `myClass`, `variable` | `class`, `int` |
| CamelCase cho biến | `firstName`, `totalAmount` | `firstname`, `total_amount` |

## Lời kết

Trong bài viết này, chúng ta đã làm quen với **cấu trúc cơ bản của một chương trình Java**, các **kiểu dữ liệu cơ bản** trong Java như `int`, `double`, `char`, `boolean`, và `String`, cũng như cách **khai báo và sử dụng biến** trong Java. 

### 🎯 **Những điểm quan trọng cần nhớ:**
- ✅ Mọi chương trình Java đều bắt đầu từ phương thức `main()`
- ✅ Java có 8 kiểu dữ liệu cơ bản (primitive types)
- ✅ Biến phải được khai báo với kiểu dữ liệu cụ thể
- ✅ Tên biến nên tuân theo quy tắc CamelCase
- ✅ Sử dụng `final` để tạo hằng số

**Đây là nền tảng quan trọng mà bạn sẽ sử dụng để xây dựng các ứng dụng Java trong tương lai.**

---

💡 **Hãy tiếp tục thực hành và thử viết các chương trình Java đơn giản để củng cố kiến thức của mình! Trong bài tiếp theo, chúng ta sẽ tìm hiểu về câu lệnh điều kiện và vòng lặp.**

## Tags
`Java` `Basic Syntax` `Data Types` `Variables` `Hello World` `Programming Fundamentals`
