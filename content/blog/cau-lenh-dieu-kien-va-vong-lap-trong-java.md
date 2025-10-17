---
title: "Câu lệnh điều kiện và vòng lặp trong Java"
date: 2025-10-15
draft: false
description: "Học cách sử dụng câu lệnh điều kiện (if-else, switch) và vòng lặp (for, while, do-while) trong Java để điều khiển luồng chương trình một cách hiệu quả."
categories: ["Programming", "Java", "Control Flow"]
tags: ["Java", "if-else", "switch", "for loop", "while loop", "do-while", "break", "continue"]
author: "Phan Thị Huỳnh Ngọc"
slug: "cau-lenh-dieu-kien-va-vong-lap-trong-java"
---

Trong lập trình, **câu lệnh điều kiện** và **vòng lặp** là hai cấu trúc quan trọng giúp điều khiển luồng thực thi của chương trình. Trong Java, chúng giúp bạn kiểm tra các điều kiện và thực hiện các thao tác lặp đi lặp lại. Hãy cùng tìm hiểu chi tiết về chúng trong bài viết này.

<!--more-->

## 1. Câu lệnh điều kiện (if, else if, else)

**Câu lệnh điều kiện** cho phép chương trình kiểm tra một điều kiện và thực hiện các hành động khác nhau tùy thuộc vào kết quả của điều kiện đó. Trong Java, chúng ta thường sử dụng các câu lệnh như `if`, `else if`, và `else` để kiểm tra và xử lý các tình huống khác nhau.

### 🔍 **Cấu trúc câu lệnh `if`:**

Câu lệnh `if` giúp kiểm tra một điều kiện, nếu điều kiện đúng, mã bên trong khối `if` sẽ được thực thi.

**Cấu trúc:**
```java
if (condition) {
    // thực thi khi điều kiện đúng
}
```

**Ví dụ:**
```java
public class AgeChecker {
    public static void main(String[] args) {
        int age = 20;
        
        if (age >= 18) {
            System.out.println("You are an adult.");
            System.out.println("Bạn đã đủ tuổi trưởng thành!");
        }
        
        System.out.println("Chương trình kết thúc.");
    }
}
```

**Trong ví dụ trên:**
- Điều kiện là `age >= 18`.
- Nếu điều kiện đúng (tức là tuổi lớn hơn hoặc bằng 18), chương trình sẽ in ra "You are an adult.".

### 🔄 **Câu lệnh `else if`:**

Câu lệnh `else if` cho phép bạn kiểm tra nhiều điều kiện. Nếu điều kiện `if` đầu tiên không đúng, chương trình sẽ kiểm tra các điều kiện tiếp theo trong các khối `else if`.

**Cấu trúc:**
```java
if (condition1) {
    // thực thi khi condition1 đúng
} else if (condition2) {
    // thực thi khi condition2 đúng
} else if (condition3) {
    // thực thi khi condition3 đúng
}
```

**Ví dụ:**
```java
public class AgeCategory {
    public static void main(String[] args) {
        int age = 16;
        
        if (age >= 18) {
            System.out.println("You are an adult.");
            System.out.println("Bạn là người trưởng thành.");
        } else if (age >= 13) {
            System.out.println("You are a teenager.");
            System.out.println("Bạn là thiếu niên.");
        } else if (age >= 6) {
            System.out.println("You are a child.");
            System.out.println("Bạn là trẻ em.");
        } else {
            System.out.println("You are a toddler.");
            System.out.println("Bạn là trẻ nhỏ.");
        }
    }
}
```

**Trong ví dụ trên:**
- Nếu `age >= 18`, chương trình in ra "You are an adult."
- Nếu `age < 18` nhưng `age >= 13`, chương trình sẽ in ra "You are a teenager."
- Nếu cả hai điều kiện đều không đúng nhưng `age >= 6`, chương trình in ra "You are a child."
- Nếu tất cả điều kiện đều không đúng, chương trình in ra "You are a toddler."

### ✅ **Câu lệnh `else`:**

Câu lệnh `else` được sử dụng để thực thi một hành động mặc định khi không có điều kiện nào trong khối `if` hoặc `else if` được thỏa mãn.

**Cấu trúc:**
```java
if (condition) {
    // thực thi khi điều kiện đúng
} else {
    // thực thi khi điều kiện sai
}
```

**Ví dụ:**
```java
public class EvenOddChecker {
    public static void main(String[] args) {
        int number = 7;
        
        if (number % 2 == 0) {
            System.out.println(number + " là số chẵn");
        } else {
            System.out.println(number + " là số lẻ");
        }
    }
}
```

**Trong ví dụ trên:**
- Nếu số chia hết cho 2 (số chẵn), chương trình in ra "Số chẵn"
- Nếu không (số lẻ), chương trình in ra "Số lẻ"

## 2. Các vòng lặp (for, while)

**Vòng lặp** là một cấu trúc lặp lại một hành động nhiều lần. Trong Java, có ba loại vòng lặp phổ biến: `for`, `while`, và `do-while`. Dưới đây, chúng ta sẽ tìm hiểu về hai loại vòng lặp cơ bản là `for` và `while`.

### 🔁 **Vòng lặp `for`:**

Vòng lặp `for` được sử dụng khi bạn biết số lần lặp trước. Cấu trúc của vòng lặp `for` bao gồm ba phần: khởi tạo, điều kiện, và cập nhật.

**Cấu trúc:**
```java
for (initialization; condition; update) {
    // mã cần lặp
}
```

- **`initialization`**: Khởi tạo giá trị biến điều khiển (thường là chỉ số i).
- **`condition`**: Điều kiện để tiếp tục vòng lặp. Khi điều kiện sai, vòng lặp dừng lại.
- **`update`**: Cập nhật giá trị của biến điều khiển sau mỗi lần lặp.

**Ví dụ:**
```java
public class ForLoopExample {
    public static void main(String[] args) {
        System.out.println("=== Đếm từ 0 đến 4 ===");
        for (int i = 0; i < 5; i++) {
            System.out.println("Lần lặp thứ " + i + ": Giá trị i = " + i);
        }
        
        System.out.println("\n=== Bảng cửu chương 5 ===");
        for (int i = 1; i <= 10; i++) {
            int result = 5 * i;
            System.out.println("5 x " + i + " = " + result);
        }
    }
}
```

**Trong ví dụ trên:**
- **Khởi tạo**: `int i = 0` (biến i bắt đầu từ 0)
- **Điều kiện**: `i < 5` (vòng lặp tiếp tục khi i nhỏ hơn 5)
- **Cập nhật**: `i++` (biến i được tăng lên 1 sau mỗi lần lặp)

### 🔄 **Vòng lặp `while`:**

Vòng lặp `while` được sử dụng khi bạn không biết số lần lặp trước, và điều kiện lặp có thể thay đổi trong quá trình thực thi.

**Cấu trúc:**
```java
while (condition) {
    // mã cần lặp
    // cập nhật điều kiện
}
```

**Ví dụ:**
```java
public class WhileLoopExample {
    public static void main(String[] args) {
        int i = 0;
        
        System.out.println("=== Đếm với While Loop ===");
        while (i < 5) {
            System.out.println("Giá trị i = " + i);
            i++; // Quan trọng: phải cập nhật i để tránh vòng lặp vô hạn
        }
        
        System.out.println("\n=== Tính giai thừa của 5 ===");
        int number = 5;
        int factorial = 1;
        int counter = 1;
        
        while (counter <= number) {
            factorial *= counter;
            System.out.println("Bước " + counter + ": " + factorial);
            counter++;
        }
        
        System.out.println("Giai thừa của " + number + " = " + factorial);
    }
}
```

**Trong ví dụ trên:**
- Vòng lặp sẽ tiếp tục cho đến khi giá trị của `i` không còn thỏa mãn điều kiện `i < 5`.

### 🔄 **Vòng lặp `do-while`:**

Mặc dù không được đề cập chi tiết trong bài này, nhưng nếu cần, bạn cũng có thể sử dụng vòng lặp `do-while`, vòng lặp này đảm bảo rằng mã trong khối lặp sẽ được thực thi **ít nhất một lần**.

**Cấu trúc:**
```java
do {
    // mã cần lặp
} while (condition);
```

**Ví dụ:**
```java
public class DoWhileExample {
    public static void main(String[] args) {
        int number = 0;
        
        do {
            System.out.println("Số hiện tại: " + number);
            number++;
        } while (number < 3);
        
        System.out.println("Vòng lặp kết thúc!");
    }
}
```

## 3. Ví dụ tổng hợp

Hãy xem một ví dụ kết hợp cả câu lệnh điều kiện và vòng lặp:

```java
public class GradeCalculator {
    public static void main(String[] args) {
        // Mảng điểm số của học sinh
        double[] scores = {85.5, 92.0, 78.5, 96.0, 88.5, 73.0, 91.5};
        String[] names = {"An", "Bình", "Chi", "Dương", "Em", "Phong", "Giang"};
        
        System.out.println("=== BẢNG ĐIỂM VÀ XẾP LOẠI ===");
        
        double totalScore = 0;
        int excellentCount = 0;
        int goodCount = 0;
        int averageCount = 0;
        int belowAverageCount = 0;
        
        // Duyệt qua từng học sinh
        for (int i = 0; i < scores.length; i++) {
            double score = scores[i];
            String name = names[i];
            String grade;
            
            // Xác định xếp loại
            if (score >= 90) {
                grade = "Xuất sắc";
                excellentCount++;
            } else if (score >= 80) {
                grade = "Giỏi";
                goodCount++;
            } else if (score >= 70) {
                grade = "Khá";
                averageCount++;
            } else {
                grade = "Trung bình";
                belowAverageCount++;
            }
            
            // In thông tin học sinh
            System.out.printf("%-8s: %.1f điểm - %s%n", name, score, grade);
            totalScore += score;
        }
        
        // Tính điểm trung bình
        double averageScore = totalScore / scores.length;
        
        System.out.println("\n=== THỐNG KÊ ===");
        System.out.printf("Điểm trung bình lớp: %.2f%n", averageScore);
        System.out.println("Số học sinh xuất sắc: " + excellentCount);
        System.out.println("Số học sinh giỏi: " + goodCount);
        System.out.println("Số học sinh khá: " + averageCount);
        System.out.println("Số học sinh trung bình: " + belowAverageCount);
    }
}
```

## Lời kết

Trong bài viết này, chúng ta đã tìm hiểu về **câu lệnh điều kiện** và các **vòng lặp** trong Java. 

### 🎯 **Những điểm quan trọng:**

#### 📋 **Câu lệnh điều kiện (if, else if, else):**
- ✅ Giúp bạn kiểm tra các điều kiện và quyết định hành động tiếp theo
- ✅ Có thể kiểm tra nhiều điều kiện với `else if`
- ✅ Sử dụng `else` cho trường hợp mặc định

#### 🔄 **Vòng lặp (for, while):**
- ✅ `for`: Dùng khi biết trước số lần lặp
- ✅ `while`: Dùng khi điều kiện lặp có thể thay đổi
- ✅ `do-while`: Đảm bảo thực thi ít nhất một lần

### 💡 **Lời khuyên khi sử dụng:**
- 🚨 **Tránh vòng lặp vô hạn**: Luôn đảm bảo điều kiện sẽ trở thành `false`
- 🎯 **Chọn vòng lặp phù hợp**: `for` cho số lần cố định, `while` cho điều kiện linh hoạt
- 📝 **Code rõ ràng**: Sử dụng tên biến có ý nghĩa và comment khi cần

**Việc sử dụng hiệu quả các câu lệnh điều kiện và vòng lặp sẽ giúp bạn viết các chương trình Java linh hoạt và mạnh mẽ.**

---

💡 **Hãy tiếp tục thực hành để làm quen với các khái niệm này và sử dụng chúng trong các dự án thực tế! Trong bài tiếp theo, chúng ta sẽ tìm hiểu về các tính năng nâng cao trong Java.**

## Tags
`Java` `If Statement` `Loops` `For Loop` `While Loop` `Control Flow` `Conditional Statements`
