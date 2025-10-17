---
title: "Các Khái Niệm Cơ Bản trong JavaScript"
date: 2025-10-17
draft: false
description: "Tìm hiểu các khái niệm cơ bản trong JavaScript: biến, kiểu dữ liệu, toán tử và câu lệnh điều kiện. Nền tảng quan trọng để bắt đầu lập trình JavaScript hiệu quả."
categories: ["Programming", "JavaScript", "Basics"]
tags: ["JavaScript", "Variables", "Data Types", "Operators", "Conditional Statements", "if-else", "switch", "Programming Basics"]
author: "Phan Thị Huỳnh Ngọc"
slug: "cac-khai-niem-co-ban-trong-javascript"
---

# Các Khái Niệm Cơ Bản trong JavaScript

JavaScript là một ngôn ngữ lập trình rất linh hoạt và mạnh mẽ. Để bắt đầu làm việc với JavaScript, bạn cần hiểu rõ các khái niệm cơ bản như **biến**, **kiểu dữ liệu**, **toán tử**, và **câu lệnh điều kiện**. Bài viết này sẽ cung cấp cho bạn cái nhìn tổng quan và chi tiết về những khái niệm này.

## 1. Biến và Các Kiểu Dữ Liệu trong JavaScript

Biến trong JavaScript là nơi bạn lưu trữ các giá trị, và chúng có thể thay đổi trong quá trình thực thi chương trình. Một trong những đặc điểm của JavaScript là không yêu cầu khai báo kiểu dữ liệu một cách chặt chẽ. Tuy nhiên, hiểu rõ các loại dữ liệu mà JavaScript hỗ trợ sẽ giúp bạn xử lý và tổ chức dữ liệu hiệu quả hơn.

### Cách khai báo biến trong JavaScript

```javascript
// ES6+ (Recommended)
let userName = "Nguyễn Văn A";     // Có thể thay đổi
const PI = 3.14159;               // Không thể thay đổi
let age;                          // Khai báo mà chưa gán giá trị

// Cách cũ (không khuyến khích)
var oldStyle = "Biến kiểu cũ";
```

### Các kiểu dữ liệu cơ bản trong JavaScript

#### 1. **Number**: Dùng để lưu trữ các số nguyên và số thực

```javascript
// Số nguyên
let age = 25;
let population = 98000000;

// Số thực
let price = 15.99;
let temperature = -5.5;

// Số đặc biệt
let infinity = Infinity;
let notANumber = NaN;

// Các phép toán với Number
let sum = 10 + 5;           // 15
let product = 4 * 3;        // 12
let division = 10 / 3;      // 3.3333333333333335
let remainder = 10 % 3;     // 1

console.log("Tuổi:", age);
console.log("Giá:", price);
console.log("Tổng:", sum);
```

#### 2. **String**: Dùng để lưu trữ chuỗi văn bản

```javascript
// Các cách khai báo string
let name = "Phan Thị Huỳnh Ngọc";
let message = 'Xin chào các bạn!';
let template = `Tên tôi là ${name}`;  // Template literal

// Các phương thức string phổ biến
let fullName = "Nguyễn Văn An";
console.log("Độ dài:", fullName.length);           // 13
console.log("Chữ hoa:", fullName.toUpperCase());   // NGUYỄN VĂN AN
console.log("Chữ thường:", fullName.toLowerCase()); // nguyễn văn an
console.log("Tách chuỗi:", fullName.split(" "));   // ["Nguyễn", "Văn", "An"]

// Nối chuỗi
let firstName = "Nguyễn";
let lastName = "An";
let fullName2 = firstName + " " + lastName;
let fullName3 = `${firstName} ${lastName}`;
console.log("Họ tên:", fullName3);
```

#### 3. **Boolean**: Dùng để lưu trữ giá trị true hoặc false

```javascript
let isStudent = true;
let isGraduated = false;
let hasJob = true;

// Các phép so sánh trả về boolean
let age = 20;
let isAdult = age >= 18;        // true
let isChild = age < 13;         // false
let isTeenager = age >= 13 && age < 20;  // false

console.log("Là học sinh:", isStudent);
console.log("Đã tốt nghiệp:", isGraduated);
console.log("Là người lớn:", isAdult);

// Chuyển đổi sang boolean
console.log(Boolean(1));        // true
console.log(Boolean(0));        // false
console.log(Boolean("hello"));  // true
console.log(Boolean(""));       // false
```

#### 4. **Undefined**: Khi một biến được khai báo nhưng chưa được gán giá trị

```javascript
let notAssigned;
console.log(notAssigned);       // undefined
console.log(typeof notAssigned); // "undefined"

// Hàm không return gì cũng trả về undefined
function noReturn() {
    let x = 5;
    // không có return statement
}
console.log(noReturn());        // undefined

// Truy cập thuộc tính không tồn tại
let person = { name: "An" };
console.log(person.age);        // undefined
```

#### 5. **Null**: Dùng để đại diện cho giá trị "không tồn tại" hoặc "không có giá trị"

```javascript
let data = null;                // Có ý định để trống
let response = null;            // Chưa nhận được dữ liệu

console.log(data);              // null
console.log(typeof data);       // "object" (đây là một bug cũ của JavaScript)

// So sánh null và undefined
console.log(null == undefined);  // true
console.log(null === undefined); // false

// Kiểm tra null
if (data === null) {
    console.log("Dữ liệu rỗng");
}
```

#### 6. **Object**: Dùng để lưu trữ các giá trị phức tạp hơn, bao gồm các cặp khóa-giá trị

```javascript
// Tạo object
let student = {
    name: "Nguyễn Văn B",
    age: 22,
    major: "Công nghệ thông tin",
    isActive: true,
    grades: [8.5, 9.0, 7.5]
};

// Truy cập thuộc tính
console.log("Tên:", student.name);
console.log("Tuổi:", student["age"]);

// Thêm thuộc tính mới
student.email = "nguyenvanb@email.com";
student.phone = "0123456789";

// Sửa thuộc tính
student.age = 23;

// Xóa thuộc tính
delete student.phone;

console.log("Thông tin sinh viên:", student);

// Object phức tạp hơn
let course = {
    title: "JavaScript Fundamentals",
    instructor: {
        name: "Thầy Minh",
        experience: 5
    },
    students: ["An", "Bình", "Chi"],
    duration: "3 tháng",
    getInfo: function() {
        return `Khóa học: ${this.title} - Giảng viên: ${this.instructor.name}`;
    }
};

console.log(course.getInfo());
```

#### 7. **Array**: Mảng trong JavaScript là một đối tượng đặc biệt giúp lưu trữ danh sách các giá trị

```javascript
// Tạo mảng
let fruits = ["táo", "cam", "chuối", "xoài"];
let numbers = [1, 2, 3, 4, 5];
let mixed = ["hello", 42, true, null, {name: "An"}];

// Truy cập phần tử
console.log("Trái cây đầu tiên:", fruits[0]);     // táo
console.log("Trái cây cuối cùng:", fruits[fruits.length - 1]); // xoài

// Thêm phần tử
fruits.push("dưa hấu");           // Thêm vào cuối
fruits.unshift("dâu tây");        // Thêm vào đầu
console.log("Danh sách trái cây:", fruits);

// Xóa phần tử
let lastFruit = fruits.pop();     // Xóa phần tử cuối
let firstFruit = fruits.shift();  // Xóa phần tử đầu
console.log("Đã xóa:", lastFruit, firstFruit);

// Các phương thức mảng hữu ích
let scores = [85, 92, 78, 96, 88];

// Tìm kiếm
console.log("Có điểm 92:", scores.includes(92));  // true
console.log("Vị trí điểm 78:", scores.indexOf(78)); // 2

// Lặp qua mảng
scores.forEach((score, index) => {
    console.log(`Điểm ${index + 1}: ${score}`);
});

// Lọc mảng
let highScores = scores.filter(score => score >= 90);
console.log("Điểm cao:", highScores);

// Chuyển đổi mảng
let doubledScores = scores.map(score => score * 2);
console.log("Điểm nhân đôi:", doubledScores);
```

## 2. Toán Tử trong JavaScript

Toán tử là những ký tự hoặc từ khóa được sử dụng để thực hiện các phép toán hoặc so sánh. JavaScript cung cấp nhiều loại toán tử, bao gồm toán tử số học, toán tử so sánh, và toán tử logic.

### Toán tử số học: Dùng để thực hiện các phép toán số học cơ bản

```javascript
let a = 10;
let b = 3;

// Các phép toán cơ bản
console.log("Cộng:", a + b);        // 13
console.log("Trừ:", a - b);         // 7
console.log("Nhân:", a * b);        // 30
console.log("Chia:", a / b);        // 3.3333333333333335
console.log("Chia lấy dư:", a % b); // 1
console.log("Lũy thừa:", a ** b);   // 1000

// Toán tử gán kết hợp
let x = 5;
x += 3;     // x = x + 3; → 8
x -= 2;     // x = x - 2; → 6
x *= 4;     // x = x * 4; → 24
x /= 3;     // x = x / 3; → 8
x %= 5;     // x = x % 5; → 3

console.log("Kết quả cuối:", x);

// Toán tử tăng/giảm
let count = 0;
console.log("count++:", count++);   // 0 (in ra rồi mới tăng)
console.log("count:", count);       // 1
console.log("++count:", ++count);   // 2 (tăng rồi mới in ra)
console.log("count--:", count--);   // 2 (in ra rồi mới giảm)
console.log("count:", count);       // 1
```

### Toán tử so sánh: Dùng để so sánh hai giá trị và trả về true hoặc false

```javascript
let num1 = 10;
let num2 = 5;
let str1 = "10";
let str2 = "5";

// So sánh giá trị (không quan tâm kiểu dữ liệu)
console.log("10 == '10':", num1 == str1);    // true
console.log("10 != 5:", num1 != num2);       // true

// So sánh giá trị và kiểu dữ liệu
console.log("10 === '10':", num1 === str1);  // false
console.log("10 !== '10':", num1 !== str1);  // true

// So sánh lớn nhỏ
console.log("10 > 5:", num1 > num2);         // true
console.log("10 < 5:", num1 < num2);         // false
console.log("10 >= 10:", num1 >= 10);        // true
console.log("5 <= 10:", num2 <= num1);       // true

// So sánh chuỗi (theo thứ tự alphabet)
console.log("'apple' > 'banana':", 'apple' > 'banana');  // false
console.log("'zebra' > 'apple':", 'zebra' > 'apple');    // true

// Ví dụ thực tế
let userAge = 20;
let minAge = 18;

if (userAge >= minAge) {
    console.log("Được phép vào!");
} else {
    console.log("Chưa đủ tuổi!");
}
```

### Toán tử logic: Dùng để thực hiện các phép toán logic với các giá trị boolean

```javascript
let isLoggedIn = true;
let isAdmin = false;
let hasPermission = true;
let age = 25;
let score = 85;

// Toán tử AND (&&) - Tất cả phải đúng
console.log("Logged in AND Admin:", isLoggedIn && isAdmin);        // false
console.log("Logged in AND Permission:", isLoggedIn && hasPermission); // true

// Toán tử OR (||) - Chỉ cần một cái đúng
console.log("Admin OR Permission:", isAdmin || hasPermission);     // true
console.log("Admin OR Logged in:", isAdmin || isLoggedIn);         // true

// Toán tử NOT (!) - Đảo ngược giá trị
console.log("NOT Admin:", !isAdmin);           // true
console.log("NOT Logged in:", !isLoggedIn);    // false

// Kết hợp các điều kiện phức tạp
let canAccess = (isLoggedIn && hasPermission) || isAdmin;
console.log("Có thể truy cập:", canAccess);    // true

// Ví dụ thực tế với điều kiện phức hợp
let canTakeExam = (age >= 18 && isLoggedIn) && (score >= 70 || hasPermission);
console.log("Có thể thi:", canTakeExam);       // true

// Short-circuit evaluation
let username = isLoggedIn && "Nguyễn Văn A";   // "Nguyễn Văn A" nếu đăng nhập
let defaultName = username || "Khách";          // "Nguyễn Văn A"

console.log("Tên hiển thị:", defaultName);
```

## 3. Câu Lệnh Điều Kiện (if, else, switch)

Câu lệnh điều kiện cho phép bạn kiểm tra một điều kiện và thực hiện các hành động khác nhau tùy thuộc vào kết quả của điều kiện đó. Trong JavaScript, bạn có thể sử dụng các câu lệnh như **if**, **else**, **else if**, và **switch** để xử lý các tình huống khác nhau.

### Câu lệnh if: Câu lệnh if giúp kiểm tra một điều kiện và thực thi mã nếu điều kiện đó đúng

```javascript
let temperature = 25;

// If đơn giản
if (temperature > 30) {
    console.log("Trời nóng quá!");
}

// If với else
if (temperature > 30) {
    console.log("Trời nóng!");
} else {
    console.log("Thời tiết dễ chịu!");
}

// Ví dụ thực tế - Kiểm tra tuổi
let userAge = 17;

if (userAge >= 18) {
    console.log("Bạn đã đủ tuổi bầu cử!");
} else {
    console.log(`Bạn còn ${18 - userAge} năm nữa mới đủ tuổi bầu cử.`);
}

// Ví dụ với multiple conditions
let isWeekend = true;
let hasWork = false;

if (isWeekend && !hasWork) {
    console.log("Có thể nghỉ ngơi!");
}
```

### Câu lệnh else if và else: Dùng để kiểm tra nhiều điều kiện khác nhau

```javascript
let score = 85;
let grade;

// Chuỗi if-else if-else
if (score >= 90) {
    grade = "A";
    console.log("Xuất sắc!");
} else if (score >= 80) {
    grade = "B";
    console.log("Giỏi!");
} else if (score >= 70) {
    grade = "C";
    console.log("Khá!");
} else if (score >= 60) {
    grade = "D";
    console.log("Trung bình!");
} else {
    grade = "F";
    console.log("Cần cố gắng thêm!");
}

console.log(`Điểm của bạn: ${score} - Xếp loại: ${grade}`);

// Ví dụ phức tạp hơn - Tính phí vận chuyển
function calculateShipping(weight, distance, isPriority) {
    let shippingCost = 0;
    
    if (weight <= 1) {
        shippingCost = 20000;
    } else if (weight <= 5) {
        shippingCost = 35000;
    } else if (weight <= 10) {
        shippingCost = 50000;
    } else {
        shippingCost = 70000;
    }
    
    // Phụ phí khoảng cách
    if (distance > 100) {
        shippingCost += 15000;
    } else if (distance > 50) {
        shippingCost += 10000;
    }
    
    // Phụ phí ưu tiên
    if (isPriority) {
        shippingCost *= 1.5;
    }
    
    return shippingCost;
}

console.log("Phí vận chuyển:", calculateShipping(3, 75, true), "VNĐ");
```

### Câu lệnh switch: Câu lệnh switch là một lựa chọn tốt khi bạn cần kiểm tra nhiều giá trị của một biến

```javascript
let day = 3;
let dayName;

switch (day) {
    case 1:
        dayName = "Thứ Hai";
        break;
    case 2:
        dayName = "Thứ Ba";
        break;
    case 3:
        dayName = "Thứ Tư";
        break;
    case 4:
        dayName = "Thứ Năm";
        break;
    case 5:
        dayName = "Thứ Sáu";
        break;
    case 6:
        dayName = "Thứ Bảy";
        break;
    case 7:
        dayName = "Chủ Nhật";
        break;
    default:
        dayName = "Ngày không hợp lệ";
}

console.log(`Hôm nay là: ${dayName}`);

// Ví dụ switch với multiple cases
let month = 12;
let season;

switch (month) {
    case 12:
    case 1:
    case 2:
        season = "Mùa Đông";
        break;
    case 3:
    case 4:
    case 5:
        season = "Mùa Xuân";
        break;
    case 6:
    case 7:
    case 8:
        season = "Mùa Hè";
        break;
    case 9:
    case 10:
    case 11:
        season = "Mùa Thu";
        break;
    default:
        season = "Tháng không hợp lệ";
}

console.log(`Tháng ${month} thuộc ${season}`);

// Ví dụ thực tế - Máy tính đơn giản
function calculator(num1, operator, num2) {
    let result;
    
    switch (operator) {
        case '+':
            result = num1 + num2;
            break;
        case '-':
            result = num1 - num2;
            break;
        case '*':
            result = num1 * num2;
            break;
        case '/':
            if (num2 !== 0) {
                result = num1 / num2;
            } else {
                return "Lỗi: Không thể chia cho 0";
            }
            break;
        case '%':
            result = num1 % num2;
            break;
        default:
            return "Lỗi: Toán tử không hợp lệ";
    }
    
    return `${num1} ${operator} ${num2} = ${result}`;
}

console.log(calculator(10, '+', 5));    // 10 + 5 = 15
console.log(calculator(20, '/', 4));    // 20 / 4 = 5
console.log(calculator(15, '%', 4));    // 15 % 4 = 3
```

### Trong ví dụ switch trên:
- Biến `day` được kiểm tra và so sánh với các giá trị trong `case`
- `break` được dùng để dừng kiểm tra sau khi tìm thấy giá trị phù hợp
- `default` sẽ được thực thi khi không có giá trị nào khớp

## 4. Ví dụ Tổng Hợp - Ứng dụng Quản lý Sinh viên Đơn giản

```javascript
// Tạo danh sách sinh viên
let students = [
    {
        id: 1,
        name: "Nguyễn Văn An",
        age: 20,
        scores: [8.5, 9.0, 7.5, 8.8],
        isActive: true
    },
    {
        id: 2,
        name: "Trần Thị Bình",
        age: 19,
        scores: [9.2, 8.7, 9.5, 9.0],
        isActive: true
    },
    {
        id: 3,
        name: "Lê Văn Cường",
        age: 21,
        scores: [6.5, 7.0, 6.8, 7.2],
        isActive: false
    }
];

// Hàm tính điểm trung bình
function calculateAverage(scores) {
    let sum = 0;
    for (let i = 0; i < scores.length; i++) {
        sum += scores[i];
    }
    return sum / scores.length;
}

// Hàm xếp loại học lực
function getGradeLevel(average) {
    if (average >= 9.0) {
        return "Xuất sắc";
    } else if (average >= 8.0) {
        return "Giỏi";
    } else if (average >= 7.0) {
        return "Khá";
    } else if (average >= 5.0) {
        return "Trung bình";
    } else {
        return "Yếu";
    }
}

// Xử lý thông tin sinh viên
students.forEach((student, index) => {
    console.log(`\n--- Sinh viên ${index + 1} ---`);
    console.log(`Tên: ${student.name}`);
    console.log(`Tuổi: ${student.age}`);
    console.log(`Trạng thái: ${student.isActive ? "Đang học" : "Đã nghỉ"}`);
    
    let average = calculateAverage(student.scores);
    let gradeLevel = getGradeLevel(average);
    
    console.log(`Điểm trung bình: ${average.toFixed(2)}`);
    console.log(`Xếp loại: ${gradeLevel}`);
    
    // Kiểm tra điều kiện học bổng
    if (student.isActive && average >= 8.5) {
        console.log("🎉 Đủ điều kiện nhận học bổng!");
    } else if (!student.isActive) {
        console.log("❌ Không thể nhận học bổng do đã nghỉ học");
    } else {
        console.log("📚 Cần cố gắng thêm để đạt học bổng");
    }
});
```

## Lời kết

Trong bài viết này, chúng ta đã tìm hiểu về những khái niệm cơ bản trong JavaScript, bao gồm:

### Những điều đã học:
- **Biến và Kiểu dữ liệu**: Number, String, Boolean, Undefined, Null, Object, Array
- **Toán tử**: Số học, so sánh, logic và cách sử dụng chúng
- **Câu lệnh điều kiện**: if-else, switch-case để điều khiển luồng chương trình

### Điểm quan trọng cần nhớ:
- JavaScript là ngôn ngữ **dynamic typing** - không cần khai báo kiểu dữ liệu
- Sử dụng `===` thay vì `==` để so sánh chính xác
- `let` và `const` thay cho `var` trong ES6+
- `switch` statement cần `break` để tránh fall-through

### Bước tiếp theo:
Đây là nền tảng quan trọng mà bạn sẽ sử dụng để xây dựng các ứng dụng JavaScript hiệu quả và linh hoạt. Hãy tiếp tục thực hành và áp dụng những kiến thức này vào các dự án thực tế để củng cố kỹ năng lập trình JavaScript của mình!

Trong bài viết tiếp theo, chúng ta sẽ tìm hiểu về **Functions và Scope** - hai khái niệm quan trọng giúp bạn tổ chức code hiệu quả hơn!

---

**Từ khóa**: JavaScript cơ bản, biến JavaScript, kiểu dữ liệu JavaScript, toán tử JavaScript, if-else JavaScript, switch-case JavaScript, lập trình JavaScript, học JavaScript.
