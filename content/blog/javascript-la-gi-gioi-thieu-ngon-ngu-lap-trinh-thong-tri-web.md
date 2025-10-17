---
title: "Các tính năng nâng cao trong Java"
date: 2025-10-15
draft: false
description: "Tìm hiểu về xử lý ngoại lệ (Exception Handling) và Java Collections Framework - các tính năng nâng cao quan trọng trong Java với ví dụ thực tế."
categories: ["Programming", "Java", "Advanced"]
tags: ["Java", "Exception Handling", "Collections", "List", "Set", "Map", "ArrayList", "HashMap", "HashSet"]
author: "Phan Thị Huỳnh Ngọc"
slug: "cac-tinh-nang-nang-cao-trong-java"
---

Java là một ngôn ngữ lập trình mạnh mẽ và linh hoạt. Trong quá trình phát triển ứng dụng, đôi khi bạn sẽ gặp phải những tình huống không lường trước được, ví dụ như khi dữ liệu không hợp lệ, hoặc khi kết nối với cơ sở dữ liệu gặp sự cố. Để xử lý những tình huống này, Java cung cấp các cơ chế như **Xử lý ngoại lệ (Exception Handling)** và **Bộ sưu tập (Collections)**. Bài viết này sẽ giúp bạn hiểu rõ về cách sử dụng chúng trong Java.

<!--more-->

## 1. Xử lý ngoại lệ (Exception Handling)

**Xử lý ngoại lệ (Exception Handling)** trong Java giúp chương trình không bị dừng đột ngột khi gặp lỗi. Java cung cấp một cơ chế mạnh mẽ để bắt và xử lý các ngoại lệ thông qua các từ khóa như `try`, `catch`, `throw`, `throws`, và `finally`.

### 📋 **Cấu trúc cơ bản của Exception Handling**

- **`try`**: Khối mã mà bạn muốn kiểm tra lỗi.
- **`catch`**: Khối mã để xử lý lỗi nếu có ngoại lệ xảy ra trong khối try.
- **`finally`**: (Tùy chọn) Khối mã sẽ luôn được thực thi sau khi khối try-catch kết thúc, bất kể có lỗi xảy ra hay không.
- **`throw`**: Được sử dụng để ném ngoại lệ.
- **`throws`**: Được sử dụng trong phương thức để khai báo rằng phương thức có thể ném ra một hoặc nhiều ngoại lệ.

### � **Ví dụ cơ bản về Exception Handling:**

```java
public class ExceptionExample {
    public static void main(String[] args) {
        try {
            // Phép chia có thể gây lỗi
            int result = 10 / 0;  // ArithmeticException
            System.out.println("Kết quả: " + result);
        } catch (ArithmeticException e) {
            System.out.println("Lỗi: Không thể chia cho 0!");
            System.out.println("Chi tiết lỗi: " + e.getMessage());
        } finally {
            System.out.println("Khối finally luôn được thực thi.");
        }
        
        System.out.println("Chương trình tiếp tục chạy bình thường.");
    }
}
```

**Giải thích:**
- Trong ví dụ trên, khi thực hiện phép chia `10 / 0`, chương trình sẽ gây ra một `ArithmeticException` (ngoại lệ chia cho 0).
- Khối `catch` sẽ bắt ngoại lệ này và in ra thông báo lỗi.
- Khối `finally` sẽ luôn được thực thi dù có lỗi xảy ra hay không.

### 🚀 **Ném ngoại lệ (Throw):**

Khi muốn ném một ngoại lệ từ bên trong chương trình, bạn sử dụng từ khóa `throw`.

```java
public class CustomExceptionExample {
    public static void checkAge(int age) {
        if (age < 18) {
            throw new IllegalArgumentException("Tuổi phải lớn hơn hoặc bằng 18!");
        }
        System.out.println("Tuổi hợp lệ: " + age);
    }
    
    public static void main(String[] args) {
        try {
            checkAge(16);  // Sẽ ném ngoại lệ
        } catch (IllegalArgumentException e) {
            System.out.println("Lỗi: " + e.getMessage());
        }
        
        try {
            checkAge(20);  // Hợp lệ
        } catch (IllegalArgumentException e) {
            System.out.println("Lỗi: " + e.getMessage());
        }
    }
}
```

**Giải thích:** Ở đây, phương thức `throw` dùng để ném một ngoại lệ tùy chỉnh, và ngoại lệ này được bắt và xử lý trong khối `catch`.

### 📢 **Khai báo ngoại lệ trong phương thức (Throws)**

Nếu phương thức có thể ném ra một ngoại lệ, bạn cần khai báo ngoại lệ đó bằng từ khóa `throws`:

```java
import java.io.*;

public class ThrowsExample {
    // Phương thức khai báo có thể ném IOException
    public static void readFile(String fileName) throws IOException {
        FileReader file = new FileReader(fileName);
        System.out.println("File đã được mở thành công!");
        file.close();
    }
    
    public static void main(String[] args) {
        try {
            readFile("nonexistent.txt");  // File không tồn tại
        } catch (IOException e) {
            System.out.println("Lỗi đọc file: " + e.getMessage());
        }
    }
}
```

**Giải thích:** Phương thức `readFile` khai báo rằng nó có thể ném ra một ngoại lệ, vì vậy khi gọi `readFile()` trong phương thức `main()`, chúng ta phải xử lý hoặc khai báo `throws` để thông báo rằng phương thức này có thể ném ra ngoại lệ.

## 2. Giới thiệu về Java Collections Framework

**Java Collections Framework** là một tập hợp các lớp và giao diện (interfaces) trong Java, cung cấp các cấu trúc dữ liệu mạnh mẽ và linh hoạt để xử lý các nhóm đối tượng. Nó giúp lập trình viên quản lý dữ liệu một cách dễ dàng và hiệu quả.

### 📊 **Các cấu trúc dữ liệu trong Java Collections Framework bao gồm:**

- **`List`**: Lưu trữ các phần tử theo thứ tự và có thể chứa các phần tử trùng lặp.
- **`Set`**: Lưu trữ các phần tử không trùng lặp và không theo thứ tự cụ thể.
- **`Map`**: Lưu trữ các cặp khóa-giá trị (key-value) với mỗi khóa duy nhất.

Java Collections cung cấp các lớp như `ArrayList`, `HashSet`, `HashMap`, giúp lập trình viên dễ dàng lựa chọn loại cấu trúc dữ liệu phù hợp với yêu cầu của bài toán.

### 🎯 **Sơ đồ phân cấp Collections:**

```
Collection Interface
├── List Interface
│   ├── ArrayList
│   ├── LinkedList
│   └── Vector
├── Set Interface
│   ├── HashSet
│   ├── LinkedHashSet
│   └── TreeSet
└── Queue Interface

Map Interface (riêng biệt)
├── HashMap
├── LinkedHashMap
└── TreeMap
```

## 3. Các loại cấu trúc dữ liệu trong Java Collections

### 📋 **a. List**

**List** là một giao diện trong Java Collections dùng để lưu trữ các phần tử theo thứ tự, cho phép truy cập bằng chỉ số (index). Các phần tử trong một List có thể trùng lặp và có thể thay đổi được.

**🎯 Ứng dụng:** Dùng khi cần lưu trữ và truy xuất dữ liệu theo thứ tự.  
**🏗️ Lớp triển khai:** ArrayList, LinkedList, Vector

**Ví dụ về List:**

```java
import java.util.*;

public class ListExample {
    public static void main(String[] args) {
        // Tạo ArrayList để lưu danh sách sinh viên
        List<String> students = new ArrayList<>();
        
        // Thêm phần tử vào List
        students.add("Nguyễn Văn An");
        students.add("Trần Thị Bình");
        students.add("Lê Văn Chi");
        students.add("Nguyễn Văn An"); // Có thể trùng lặp
        
        // Hiển thị danh sách
        System.out.println("=== DANH SÁCH SINH VIÊN ===");
        for (int i = 0; i < students.size(); i++) {
            System.out.println((i + 1) + ". " + students.get(i));
        }
        
        // Các phương thức phổ biến
        System.out.println("\nSố lượng sinh viên: " + students.size());
        System.out.println("Sinh viên đầu tiên: " + students.get(0));
        System.out.println("Sinh viên cuối cùng: " + students.get(students.size() - 1));
        
        // Kiểm tra tồn tại
        if (students.contains("Trần Thị Bình")) {
            System.out.println("Trần Thị Bình có trong danh sách");
        }
        
        // Xóa phần tử
        students.remove("Lê Văn Chi");
        System.out.println("Sau khi xóa Lê Văn Chi: " + students);
    }
}
```

### 🔗 **b. Set**

**Set** là một giao diện trong Java Collections dùng để lưu trữ các phần tử mà không có sự trùng lặp. Các phần tử trong một Set không có thứ tự xác định và không cho phép các giá trị trùng lặp.

**🎯 Ứng dụng:** Dùng khi không cần quan tâm đến thứ tự của các phần tử và muốn đảm bảo rằng mỗi phần tử chỉ xuất hiện một lần.  
**🏗️ Lớp triển khai:** HashSet, LinkedHashSet, TreeSet

**Ví dụ về Set:**

```java
import java.util.*;

public class SetExample {
    public static void main(String[] args) {
        // Tạo HashSet để lưu các môn học
        Set<String> subjects = new HashSet<>();
        
        // Thêm phần tử vào Set
        subjects.add("Toán học");
        subjects.add("Vật lý");
        subjects.add("Hóa học");
        subjects.add("Toán học"); // Trùng lặp - sẽ bị bỏ qua
        subjects.add("Sinh học");
        
        // Hiển thị danh sách (thứ tự không đảm bảo)
        System.out.println("=== DANH SÁCH MÔN HỌC ===");
        for (String subject : subjects) {
            System.out.println("- " + subject);
        }
        
        System.out.println("\nSố môn học: " + subjects.size());
        
        // Kiểm tra tồn tại
        if (subjects.contains("Toán học")) {
            System.out.println("Môn Toán học có trong danh sách");
        }
        
        // So sánh với List
        List<String> subjectList = Arrays.asList("Toán học", "Vật lý", "Toán học");
        Set<String> uniqueSubjects = new HashSet<>(subjectList);
        
        System.out.println("List gốc: " + subjectList + " (size: " + subjectList.size() + ")");
        System.out.println("Set unique: " + uniqueSubjects + " (size: " + uniqueSubjects.size() + ")");
    }
}
```

### 🗝️ **c. Map**

**Map** là một giao diện trong Java Collections, lưu trữ các cặp khóa-giá trị. Mỗi khóa trong một Map là duy nhất, nhưng giá trị có thể trùng lặp. Map không duy trì thứ tự của các phần tử.

**🎯 Ứng dụng:** Dùng khi bạn cần lưu trữ các mối quan hệ giữa khóa và giá trị, ví dụ như tra cứu thông tin hoặc lưu trữ cấu hình.  
**🏗️ Lớp triển khai:** HashMap, TreeMap, LinkedHashMap

**Ví dụ về Map:**

```java
import java.util.*;

public class MapExample {
    public static void main(String[] args) {
        // Tạo HashMap để lưu thông tin sinh viên (ID -> Tên)
        Map<String, String> studentMap = new HashMap<>();
        
        // Thêm cặp key-value
        studentMap.put("SV001", "Nguyễn Văn An");
        studentMap.put("SV002", "Trần Thị Bình");
        studentMap.put("SV003", "Lê Văn Chi");
        studentMap.put("SV004", "Phạm Thị Dung");
        
        // Hiển thị thông tin
        System.out.println("=== DANH SÁCH SINH VIÊN ===");
        for (Map.Entry<String, String> entry : studentMap.entrySet()) {
            System.out.println("ID: " + entry.getKey() + " - Tên: " + entry.getValue());
        }
        
        // Tra cứu theo key
        String studentId = "SV002";
        if (studentMap.containsKey(studentId)) {
            System.out.println("\nSinh viên " + studentId + ": " + studentMap.get(studentId));
        }
        
        // Ví dụ phức tạp hơn: Map lưu điểm số
        Map<String, Double> grades = new HashMap<>();
        grades.put("SV001", 8.5);
        grades.put("SV002", 9.0);
        grades.put("SV003", 7.5);
        grades.put("SV004", 8.8);
        
        System.out.println("\n=== BẢNG ĐIỂM ===");
        double totalGrade = 0;
        for (Map.Entry<String, Double> entry : grades.entrySet()) {
            String id = entry.getKey();
            Double grade = entry.getValue();
            String name = studentMap.get(id);
            System.out.printf("%s - %s: %.1f điểm%n", id, name, grade);
            totalGrade += grade;
        }
        
        double averageGrade = totalGrade / grades.size();
        System.out.printf("Điểm trung bình: %.2f%n", averageGrade);
    }
}
```

## 4. Khi nào nên sử dụng List, Set và Map?

Mỗi cấu trúc dữ liệu trong Java Collections có ứng dụng riêng tùy vào yêu cầu bài toán. Dưới đây là một số gợi ý:

### 📋 **List: Sử dụng khi bạn cần:**
- ✅ Lưu trữ các phần tử theo thứ tự (có thể truy xuất theo chỉ số)
- ✅ Cho phép phần tử trùng lặp
- ✅ **Ví dụ:** Danh sách sinh viên trong lớp, lịch trình công việc, lịch sử giao dịch

### � **Set: Sử dụng khi bạn cần:**
- ✅ Đảm bảo tính duy nhất của các phần tử (không có phần tử trùng lặp)
- ✅ Không cần quan tâm đến thứ tự của phần tử
- ✅ **Ví dụ:** Danh sách tên người tham gia sự kiện, tập hợp các từ trong văn bản, danh sách ID duy nhất

### 🗝️ **Map: Sử dụng khi bạn cần:**
- ✅ Lưu trữ các cặp khóa-giá trị, trong đó mỗi khóa là duy nhất
- ✅ Tra cứu nhanh giá trị tương ứng với khóa
- ✅ **Ví dụ:** Sổ điện thoại (tên-số điện thoại), từ điển (từ-định nghĩa), cache dữ liệu

### 📊 **Bảng so sánh nhanh:**

| Đặc điểm | List | Set | Map |
|----------|------|-----|-----|
| **Cho phép trùng lặp** | ✅ Có | ❌ Không | ✅ Giá trị có, Key không |
| **Truy cập theo index** | ✅ Có | ❌ Không | ❌ Không |
| **Tra cứu theo key** | ❌ Không | ❌ Không | ✅ Có |
| **Thứ tự phần tử** | ✅ Duy trì | ❓ Tùy loại | ❓ Tùy loại |
| **Hiệu suất tra cứu** | O(n) | O(1) | O(1) |

## 5. Kết luận

**Java Collections Framework** cung cấp các cấu trúc dữ liệu mạnh mẽ và linh hoạt giúp bạn giải quyết nhiều bài toán về quản lý và xử lý dữ liệu. Việc hiểu và lựa chọn đúng loại cấu trúc dữ liệu (`List`, `Set`, `Map`) tùy thuộc vào yêu cầu bài toán là rất quan trọng.

### 🎯 **Những điểm quan trọng cần nhớ:**

#### 🛡️ **Exception Handling:**
- ✅ Sử dụng `try-catch` để xử lý lỗi một cách an toàn
- ✅ `finally` luôn được thực thi, dùng để cleanup resources
- ✅ `throw` để ném ngoại lệ, `throws` để khai báo ngoại lệ có thể xảy ra

#### � **Collections Framework:**
- ✅ **List**: Thứ tự + cho phép trùng lặp (ArrayList phổ biến nhất)
- ✅ **Set**: Không trùng lặp + không quan tâm thứ tự (HashSet nhanh nhất)
- ✅ **Map**: Cặp key-value + key duy nhất (HashMap hiệu quả nhất)

**Sử dụng chúng một cách hợp lý sẽ giúp chương trình của bạn trở nên dễ dàng quản lý, bảo trì và tối ưu hiệu suất.**

---

💡 **Trong bài viết này, chúng ta đã tìm hiểu về Xử lý ngoại lệ (Exception Handling) và các loại cấu trúc dữ liệu phổ biến như List, Set, và Map trong Java. Xử lý ngoại lệ giúp chương trình Java trở nên ổn định và mạnh mẽ hơn, tránh được sự cố khi có lỗi xảy ra. Bộ sưu tập giúp tổ chức và quản lý dữ liệu hiệu quả, cho phép thao tác với các nhóm đối tượng như danh sách, tập hợp, và bản đồ.**

**Việc nắm vững các khái niệm này sẽ giúp bạn viết các chương trình Java mạnh mẽ, dễ dàng xử lý lỗi và làm việc với dữ liệu một cách hiệu quả.**

## Tags và từ khóa SEO
`Java Collections Framework` `List trong Java` `Set trong Java` `Map trong Java` `Java ArrayList` `Java HashMap` `Java LinkedHashSet` `Exception Handling` `Try Catch Java`
