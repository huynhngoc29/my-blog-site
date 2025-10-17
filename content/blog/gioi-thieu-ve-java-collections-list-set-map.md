---
title: "Giới thiệu về Java Collections: List, Set, Map"
date: 2025-10-16
draft: falsetitle: "Giới thiệu về Java Collections: List, Set, và Map"
date: 2025-10-17
draft: false
description: "Tìm hiểu về Java Collections Framework - các cấu trúc dữ liệu quan trọng: List, Set, Map với ví dụ thực tế và cách ứng dụng trong lập trình Java."
categories: ["Programming", "Java", "Collections"]
tags: ["Java", "Collections", "ArrayList", "HashMap", "HashSet", "List", "Set", "Map", "Data Structures"]
author: "Phan Thị Huỳnh Ngọc"
slug: "gioi-thieu-ve-java-collections-list-set-map"
---

Chào các bạn,

Sau khi làm quen với **OOP**, hôm nay chúng ta sẽ tìm hiểu về cách Java giúp chúng ta quản lý và xử lý dữ liệu một cách hiệu quả: **Java Collections Framework (JCF)**. Đây là một tập hợp các giao diện và lớp giúp lưu trữ và thao tác với các nhóm đối tượng.

<!--more-->

Trong bài này, chúng ta sẽ tập trung vào **ba giao diện cốt lõi** (Core Interfaces) của JCF: **List**, **Set**, và **Map**. Mỗi loại có quy tắc và ứng dụng riêng, phù hợp với các yêu cầu bài toán khác nhau.

## 1. Giới thiệu về Java Collections Framework

**Java Collections Framework** là một tập hợp các lớp và giao diện (interfaces) trong Java, cung cấp các cấu trúc dữ liệu mạnh mẽ và linh hoạt để xử lý các nhóm đối tượng. Nó giúp lập trình viên quản lý dữ liệu một cách dễ dàng và hiệu quả.

### 🗂️ **Các cấu trúc dữ liệu trong Java Collections Framework:**

- **📋 List**: Lưu trữ các phần tử theo thứ tự và có thể chứa các phần tử trùng lặp
- **🔹 Set**: Lưu trữ các phần tử không trùng lặp và không theo thứ tự cụ thể  
- **🗝️ Map**: Lưu trữ các cặp khóa-giá trị (key-value) với mỗi khóa duy nhất

Java Collections cung cấp các lớp như **ArrayList**, **HashSet**, **HashMap**, giúp lập trình viên dễ dàng lựa chọn loại cấu trúc dữ liệu phù hợp với yêu cầu của bài toán.

## 2. Các loại cấu trúc dữ liệu trong Java Collections

### a. 📋 List

**List** là một giao diện trong Java Collections dùng để lưu trữ các phần tử theo thứ tự, cho phép truy cập bằng chỉ số (index). Các phần tử trong một List có thể trùng lặp và có thể thay đổi được.

- **Ứng dụng**: Dùng khi cần lưu trữ và truy xuất dữ liệu theo thứ tự
- **Lớp triển khai**: `ArrayList`, `LinkedList`, `Vector`

#### Ví dụ về List:

```java
import java.util.ArrayList;
import java.util.List;

public class ListExample {
    public static void main(String[] args) {
        // Tạo một ArrayList để lưu danh sách sinh viên
        List<String> students = new ArrayList<>();
        
        // Thêm phần tử vào List
        students.add("Ngọc");
        students.add("Minh");
        students.add("Lan");
        students.add("Ngọc"); // Cho phép trùng lặp
        
        System.out.println("Danh sách sinh viên: " + students);
        // Output: [Ngọc, Minh, Lan, Ngọc]
        
        // Truy cập phần tử theo index
        System.out.println("Sinh viên đầu tiên: " + students.get(0));
        // Output: Ngọc
        
        // Thay đổi phần tử theo index
        students.set(1, "Hùng");
        System.out.println("Sau khi thay đổi: " + students);
        // Output: [Ngọc, Hùng, Lan, Ngọc]
        
        // Kiểm tra size và contains
        System.out.println("Số lượng sinh viên: " + students.size());
        System.out.println("Có Lan không? " + students.contains("Lan"));
        
        // Duyệt qua tất cả phần tử
        System.out.println("Danh sách chi tiết:");
        for (int i = 0; i < students.size(); i++) {
            System.out.println((i + 1) + ". " + students.get(i));
        }
    }
}
```

Ở ví dụ trên, **ArrayList** là một lớp triển khai của List, cho phép thêm và truy cập các phần tử theo chỉ số.

### b. 🔹 Set

**Set** là một giao diện trong Java Collections dùng để lưu trữ các phần tử mà không có sự trùng lặp. Các phần tử trong một Set không có thứ tự xác định và không cho phép các giá trị trùng lặp.

- **Ứng dụng**: Dùng khi không cần quan tâm đến thứ tự của các phần tử và muốn đảm bảo rằng mỗi phần tử chỉ xuất hiện một lần
- **Lớp triển khai**: `HashSet`, `LinkedHashSet`, `TreeSet`

#### Ví dụ về Set:

```java
import java.util.HashSet;
import java.util.Set;

public class SetExample {
    public static void main(String[] args) {
        // Tạo một HashSet để lưu các môn học
        Set<String> subjects = new HashSet<>();
        
        // Thêm phần tử vào Set
        subjects.add("Java");
        subjects.add("Python");
        subjects.add("JavaScript");
        subjects.add("Java"); // Sẽ bị bỏ qua vì đã tồn tại
        
        System.out.println("Danh sách môn học: " + subjects);
        // Output: [Java, Python, JavaScript] (thứ tự có thể khác)
        
        // Kiểm tra phần tử có tồn tại
        System.out.println("Có môn Java không? " + subjects.contains("Java"));
        
        // Thêm nhiều môn học cùng lúc
        subjects.add("C++");
        subjects.add("Go");
        
        System.out.println("Số lượng môn học: " + subjects.size());
        
        // Duyệt qua tất cả phần tử
        System.out.println("Các môn học:");
        for (String subject : subjects) {
            System.out.println("- " + subject);
        }
        
        // Xóa một môn học
        subjects.remove("Python");
        System.out.println("Sau khi xóa Python: " + subjects);
    }
}
```

Ở ví dụ trên, **HashSet** là lớp triển khai của Set, và nó tự động loại bỏ các phần tử trùng lặp, đảm bảo tính duy nhất.

### c. 🗝️ Map

**Map** là một giao diện trong Java Collections, lưu trữ các cặp khóa-giá trị. Mỗi khóa trong một Map là duy nhất, nhưng giá trị có thể trùng lặp. Map không duy trì thứ tự của các phần tử.

- **Ứng dụng**: Dùng khi bạn cần lưu trữ các mối quan hệ giữa khóa và giá trị, ví dụ như tra cứu thông tin hoặc lưu trữ cấu hình
- **Lớp triển khai**: `HashMap`, `TreeMap`, `LinkedHashMap`

#### Ví dụ về Map:

```java
import java.util.HashMap;
import java.util.Map;

public class MapExample {
    public static void main(String[] args) {
        // Tạo một HashMap để lưu thông tin sinh viên (ID -> Tên)
        Map<String, String> studentDirectory = new HashMap<>();
        
        // Thêm cặp key-value vào Map
        studentDirectory.put("SV001", "Phan Thị Huỳnh Ngọc");
        studentDirectory.put("SV002", "Nguyễn Văn Minh");
        studentDirectory.put("SV003", "Trần Thị Lan");
        studentDirectory.put("SV001", "Phan Huỳnh Ngọc"); // Ghi đè giá trị cũ
        
        System.out.println("Danh bạ sinh viên: " + studentDirectory);
        
        // Truy cập giá trị bằng key
        String studentName = studentDirectory.get("SV002");
        System.out.println("Sinh viên SV002: " + studentName);
        
        // Kiểm tra key hoặc value có tồn tại
        System.out.println("Có mã SV003? " + studentDirectory.containsKey("SV003"));
        System.out.println("Có sinh viên tên Lan? " + 
                          studentDirectory.containsValue("Trần Thị Lan"));
        
        // Tạo Map lưu điểm số (Tên -> Điểm)
        Map<String, Double> scores = new HashMap<>();
        scores.put("Ngọc", 8.5);
        scores.put("Minh", 7.2);
        scores.put("Lan", 9.0);
        
        System.out.println("\nBảng điểm:");
        // Duyệt qua tất cả entries
        for (Map.Entry<String, Double> entry : scores.entrySet()) {
            System.out.println(entry.getKey() + ": " + entry.getValue() + " điểm");
        }
        
        // Hoặc duyệt qua keys
        System.out.println("\nDanh sách sinh viên có điểm:");
        for (String name : scores.keySet()) {
            System.out.println("- " + name + ": " + scores.get(name));
        }
    }
}
```

## 3. Khi nào nên sử dụng List, Set và Map?

Mỗi cấu trúc dữ liệu trong Java Collections có ứng dụng riêng tùy vào yêu cầu bài toán. Dưới đây là một số gợi ý:

### 📋 **List**: Sử dụng khi bạn cần:
- ✅ Lưu trữ các phần tử theo thứ tự (có thể truy xuất theo chỉ số)
- ✅ Cho phép phần tử trùng lặp
- **Ví dụ**: Danh sách sinh viên trong lớp, lịch trình công việc, lịch sử giao dịch

### 🔹 **Set**: Sử dụng khi bạn cần:
- ✅ Đảm bảo tính duy nhất của các phần tử (không có phần tử trùng lặp)
- ✅ Không cần quan tâm đến thứ tự của phần tử
- **Ví dụ**: Danh sách tên người tham gia sự kiện, tập hợp các từ trong một văn bản, danh sách tag

### 🗝️ **Map**: Sử dụng khi bạn cần:
- ✅ Lưu trữ các cặp khóa-giá trị, trong đó mỗi khóa là duy nhất
- ✅ Tra cứu giá trị tương ứng với khóa đó một cách nhanh chóng
- **Ví dụ**: Sổ điện thoại (khóa là tên, giá trị là số điện thoại), từ điển (khóa là từ, giá trị là định nghĩa), cache dữ liệu

## 4. So sánh nhanh các Collections

| Loại | Trùng lặp | Thứ tự | Truy cập | Ứng dụng chính |
|------|-----------|---------|----------|----------------|
| **List** | ✅ Có | ✅ Có | Index | Danh sách có thứ tự |
| **Set** | ❌ Không | ❌ Không | Iteration | Tập hợp duy nhất |
| **Map** | ❌ Key không<br>✅ Value có | ❌ Không | Key | Tra cứu key-value |

## 5. Kết luận

**Java Collections Framework** cung cấp các cấu trúc dữ liệu mạnh mẽ và linh hoạt giúp bạn giải quyết nhiều bài toán về quản lý và xử lý dữ liệu. Việc hiểu và lựa chọn đúng loại cấu trúc dữ liệu (**List**, **Set**, **Map**) tùy thuộc vào yêu cầu bài toán là rất quan trọng.

### 🎯 **Lời khuyên thực tế:**
- **Bắt đầu với ArrayList** nếu bạn cần list đơn giản
- **Dùng HashSet** khi cần loại bỏ duplicate
- **Chọn HashMap** cho việc tra cứu nhanh theo key
- **Luôn sử dụng Generics** (như `List<String>`) để đảm bảo type safety

Sử dụng chúng một cách hợp lý sẽ giúp chương trình của bạn trở nên dễ dàng quản lý, bảo trì và tối ưu hiệu suất.

---

💡 **Bài viết trên đã giới thiệu về Java Collections và các loại cấu trúc dữ liệu phổ biến như List, Set, và Map. Bạn có thể sử dụng các ví dụ và lý thuyết này để áp dụng vào các dự án thực tế của mình.**

## Tags và từ khóa
`Java Collections` `ArrayList` `HashMap` `HashSet` `List` `Set` `Map` `Data Structures` `Java Framework`
