---
title: "Hàm và Lập Trình Hàm trong JavaScript"
date: 2025-10-17
draft: false
description: "Tìm hiểu về các loại hàm trong JavaScript: hàm truyền thống, hàm ẩn danh, arrow functions và lập trình hàm. Nắm vững khái niệm cốt lõi để viết code hiệu quả."
categories: ["Programming", "JavaScript", "Functions"]
tags: ["JavaScript", "Functions", "Arrow Functions", "Anonymous Functions", "Functional Programming", "ES6", "Callbacks"]
author: "Phan Thị Huỳnh Ngọc"
slug: "ham-va-lap-trinh-ham-trong-javascript"
---

# Hàm và Lập Trình Hàm trong JavaScript

JavaScript là một ngôn ngữ rất linh hoạt và mạnh mẽ, đặc biệt trong việc sử dụng hàm. **Hàm** giúp bạn đóng gói các đoạn mã lại, cho phép tái sử dụng chúng nhiều lần trong chương trình. Bài viết này sẽ giúp bạn hiểu cách khai báo và sử dụng hàm trong JavaScript, cũng như những khái niệm nâng cao như **hàm ẩn danh**, **hàm mũi tên**, và **lập trình hàm**.

## 1. Khai Báo và Sử Dụng Hàm

Trong JavaScript, hàm là một đoạn mã có thể được gọi lại nhiều lần. Bạn có thể khai báo hàm bằng từ khóa `function`, theo cú pháp sau:

```javascript
function functionName(parameters) {
    // Thân hàm - code logic
    return value; // Tùy chọn
}
```

Trong đó:
- `parameters` là các giá trị mà bạn truyền vào hàm
- `functionName` là tên của hàm
- `return` là giá trị mà hàm trả về sau khi thực thi (nếu có)

### Ví dụ về hàm không có giá trị trả về:

```javascript
// Khai báo hàm chào hỏi
function greet(name) {
    console.log(`Xin chào, ${name}!`);
    console.log("Chào mừng bạn đến với JavaScript!");
}

// Gọi hàm
greet("Alice");     // Output: Xin chào, Alice!
greet("Bob");       // Output: Xin chào, Bob!
greet("Charlie");   // Output: Xin chào, Charlie!

// Hàm hiển thị thông tin người dùng
function showUserInfo(name, age, city) {
    console.log("=== THÔNG TIN NGƯỜI DÙNG ===");
    console.log(`Tên: ${name}`);
    console.log(`Tuổi: ${age}`);
    console.log(`Thành phố: ${city}`);
    console.log("========================");
}

showUserInfo("Nguyễn Văn A", 25, "Hà Nội");
```

- Hàm `greet` nhận một tham số `name` và in ra lời chào
- Khi gọi `greet("Alice")`, JavaScript sẽ in ra "Xin chào, Alice!"

### Ví dụ về hàm có giá trị trả về:

```javascript
// Hàm tính tổng hai số
function add(a, b) {
    return a + b;
}

// Sử dụng hàm và lưu kết quả
let result = add(5, 3);
console.log(`Kết quả: ${result}`); // Output: Kết quả: 8

// Hàm tính diện tích hình chữ nhật
function calculateArea(width, height) {
    let area = width * height;
    return area;
}

let roomArea = calculateArea(5, 4);
console.log(`Diện tích phòng: ${roomArea} m²`); // Output: Diện tích phòng: 20 m²

// Hàm kiểm tra số chẵn lẻ
function isEven(number) {
    return number % 2 === 0;
}

console.log(`10 là số chẵn: ${isEven(10)}`); // true
console.log(`7 là số chẵn: ${isEven(7)}`);   // false

// Hàm tìm số lớn nhất
function findMax(a, b, c) {
    if (a >= b && a >= c) {
        return a;
    } else if (b >= a && b >= c) {
        return b;
    } else {
        return c;
    }
}

let maxNumber = findMax(15, 8, 23);
console.log(`Số lớn nhất: ${maxNumber}`); // Output: Số lớn nhất: 23
```

- Hàm `add` nhận hai tham số `a` và `b`, sau đó trả về tổng của chúng
- Giá trị trả về của hàm sẽ được lưu vào biến `result` và in ra kết quả

### Parameters và Arguments

```javascript
// Hàm với tham số mặc định (ES6)
function greetWithDefault(name = "Bạn", greeting = "Xin chào") {
    return `${greeting}, ${name}!`;
}

console.log(greetWithDefault());                    // "Xin chào, Bạn!"
console.log(greetWithDefault("An"));                // "Xin chào, An!"
console.log(greetWithDefault("Bình", "Chào bạn")); // "Chào bạn, Bình!"

// Rest parameters - nhận nhiều tham số
function sum(...numbers) {
    let total = 0;
    for (let number of numbers) {
        total += number;
    }
    return total;
}

console.log(sum(1, 2, 3));          // 6
console.log(sum(1, 2, 3, 4, 5));    // 15
console.log(sum(10));               // 10

// Hàm với object parameter
function createStudent(studentInfo) {
    return {
        id: Date.now(),
        name: studentInfo.name,
        age: studentInfo.age,
        major: studentInfo.major,
        gpa: studentInfo.gpa || 0,
        isActive: true
    };
}

let newStudent = createStudent({
    name: "Trần Thị C",
    age: 20,
    major: "Công nghệ thông tin",
    gpa: 3.5
});

console.log(newStudent);
```

## 2. Hàm Ẩn Danh (Anonymous Functions)

Một **hàm ẩn danh** là một hàm không có tên, thường được sử dụng như một đối tượng hoặc được truyền vào các hàm khác làm đối số. Hàm ẩn danh là một tính năng mạnh mẽ trong JavaScript.

### Cấu trúc của hàm ẩn danh:

```javascript
let variableName = function(parameters) {
    // Thân hàm
    return value;
};
```

### Ví dụ cơ bản:

```javascript
// Hàm ẩn danh được gán vào biến
let greet = function(name) {
    console.log(`Hello, ${name}!`);
};

// Gọi hàm thông qua biến
greet("Bob"); // Output: Hello, Bob!

// Hàm ẩn danh tính toán
let multiply = function(x, y) {
    return x * y;
};

console.log(multiply(4, 5)); // Output: 20

// Hàm ẩn danh phức tạp hơn
let calculator = function(operation, a, b) {
    switch(operation) {
        case 'add':
            return a + b;
        case 'subtract':
            return a - b;
        case 'multiply':
            return a * b;
        case 'divide':
            return b !== 0 ? a / b : 'Không thể chia cho 0';
        default:
            return 'Phép toán không hợp lệ';
    }
};

console.log(calculator('add', 10, 5));      // 15
console.log(calculator('multiply', 3, 4));  // 12
```

### Hàm ẩn danh trong Callback Functions:

```javascript
// Sử dụng với setTimeout
setTimeout(function() {
    console.log("Tin nhắn này xuất hiện sau 2 giây");
}, 2000);

// Sử dụng với Array methods
let numbers = [1, 2, 3, 4, 5];

// map với hàm ẩn danh
let doubled = numbers.map(function(num) {
    return num * 2;
});
console.log("Số gấp đôi:", doubled); // [2, 4, 6, 8, 10]

// filter với hàm ẩn danh
let evenNumbers = numbers.filter(function(num) {
    return num % 2 === 0;
});
console.log("Số chẵn:", evenNumbers); // [2, 4]

// forEach với hàm ẩn danh
let students = ["An", "Bình", "Chi", "Dũng"];
students.forEach(function(student, index) {
    console.log(`${index + 1}. ${student}`);
});

// Event handling với hàm ẩn danh
document.getElementById('myButton').addEventListener('click', function() {
    console.log('Button được click!');
});
```

### Immediately Invoked Function Expression (IIFE):

```javascript
// IIFE - Hàm tự gọi ngay lập tức
(function() {
    console.log("Hàm này chạy ngay lập tức!");
    let privateVariable = "Biến này chỉ tồn tại trong hàm";
    console.log(privateVariable);
})();

// IIFE với tham số
(function(message) {
    console.log(`Thông điệp: ${message}`);
})("Xin chào từ IIFE!");

// IIFE trả về giá trị
let result = (function(a, b) {
    return a + b;
})(10, 20);

console.log(`Kết quả IIFE: ${result}`); // 30
```

## 3. Hàm Mũi Tên (Arrow Functions)

JavaScript ES6 giới thiệu **hàm mũi tên**, giúp viết hàm ngắn gọn và dễ đọc hơn. Cú pháp của hàm mũi tên có sự thay đổi so với cú pháp hàm truyền thống.

### Cấu trúc của hàm mũi tên:

```javascript
// Cú pháp cơ bản
let functionName = (parameters) => {
    // Thân hàm
    return value;
};

// Cú pháp ngắn gọn (một dòng)
let functionName = (parameters) => expression;
```

### Ví dụ về hàm mũi tên:

```javascript
// Hàm truyền thống
function traditionalAdd(a, b) {
    return a + b;
}

// Hàm mũi tên tương đương
let arrowAdd = (a, b) => {
    return a + b;
};

// Hàm mũi tên ngắn gọn (một biểu thức)
let add = (a, b) => a + b;

console.log(add(5, 3)); // Output: 8

// Hàm mũi tên với một tham số (có thể bỏ dấu ngoặc)
let square = x => x * x;
let double = x => x * 2;

console.log(square(4)); // 16
console.log(double(7)); // 14

// Hàm mũi tên không có tham số
let sayHello = () => console.log("Xin chào!");
let getCurrentTime = () => new Date().toLocaleString();

sayHello(); // Output: Xin chào!
console.log(getCurrentTime()); // Output: thời gian hiện tại
```

### Hàm mũi tên có giá trị trả về:

```javascript
// Trả về object (cần dấu ngoặc tròn)
let createPerson = (name, age) => ({
    name: name,
    age: age,
    greet: function() {
        return `Xin chào, tôi là ${this.name}`;
    }
});

let person = createPerson("An", 25);
console.log(person.greet()); // "Xin chào, tôi là An"

// Hàm mũi tên với logic phức tạp
let calculateGrade = (score) => {
    if (score >= 90) return 'A';
    if (score >= 80) return 'B';
    if (score >= 70) return 'C';
    if (score >= 60) return 'D';
    return 'F';
};

console.log(calculateGrade(85)); // "B"
console.log(calculateGrade(92)); // "A"

// Hàm mũi tên trong array methods
let numbers = [1, 2, 3, 4, 5];

let squared = numbers.map(n => n * n);
let evens = numbers.filter(n => n % 2 === 0);
let sum = numbers.reduce((acc, n) => acc + n, 0);

console.log("Bình phương:", squared); // [1, 4, 9, 16, 25]
console.log("Số chẵn:", evens);       // [2, 4]
console.log("Tổng:", sum);            // 15
```

### Ưu điểm của hàm mũi tên:

```javascript
// 1. Cú pháp ngắn gọn, dễ đọc
let students = ['An', 'Bình', 'Chi'];

// Cách cũ
students.forEach(function(student) {
    console.log(student);
});

// Cách mới với arrow function
students.forEach(student => console.log(student));

// 2. Không có 'this' riêng - kế thừa từ scope bao quanh
let counter = {
    count: 0,
    
    // Regular function - có 'this' riêng
    increment: function() {
        this.count++;
        console.log(`Count: ${this.count}`);
    },
    
    // Arrow function - kế thừa 'this' từ object
    start: function() {
        setInterval(() => {
            this.count++; // 'this' tham chiếu đến counter object
            console.log(`Auto count: ${this.count}`);
        }, 1000);
    }
};

counter.increment(); // Count: 1
counter.start();     // Auto count sẽ tăng mỗi giây
```

### Khi nào nên sử dụng Arrow Functions:

```javascript
// ✅ Tốt cho: Callback functions
let numbers = [1, 2, 3, 4, 5];
let doubled = numbers.map(n => n * 2);

// ✅ Tốt cho: Short functions
let isPositive = x => x > 0;
let getLength = str => str.length;

// ✅ Tốt cho: Event handlers (khi cần preserve 'this')
class Button {
    constructor(element) {
        this.element = element;
        this.clickCount = 0;
        
        // Arrow function preserves 'this'
        this.element.addEventListener('click', () => {
            this.clickCount++;
            console.log(`Clicked ${this.clickCount} times`);
        });
    }
}

// ❌ Không nên dùng cho: Object methods
let person = {
    name: 'An',
    // Không nên dùng arrow function cho method
    greet: () => {
        console.log(`Hello, ${this.name}`); // 'this' không tham chiếu đến person
    }
};
```

## 4. Lập Trình Hàm (Functional Programming)

**Lập trình hàm** là một phương pháp lập trình trong đó hàm được coi là công dân bậc một và có thể được truyền làm tham số hoặc trả về từ các hàm khác. JavaScript hỗ trợ lập trình hàm, cho phép bạn truyền và trả về các hàm như đối tượng.

### Higher-Order Functions:

```javascript
// Hàm nhận hàm khác làm tham số
function calculate(a, b, operation) {
    return operation(a, b);
}

// Các hàm operation
let add = (x, y) => x + y;
let multiply = (x, y) => x * y;
let subtract = (x, y) => x - y;

// Sử dụng higher-order function
console.log(calculate(10, 5, add));      // 15
console.log(calculate(10, 5, multiply)); // 50
console.log(calculate(10, 5, subtract)); // 5

// Ví dụ thực tế - Tính lương với các phương thức khác nhau
function calculateSalary(baseSalary, calculator) {
    return calculator(baseSalary);
}

let fullTimeCalculator = (base) => base;
let partTimeCalculator = (base) => base * 0.6;
let freelanceCalculator = (base) => base * 0.8;

let baseSalary = 10000000;

console.log("Full-time:", calculateSalary(baseSalary, fullTimeCalculator)); // 10,000,000
console.log("Part-time:", calculateSalary(baseSalary, partTimeCalculator)); // 6,000,000
console.log("Freelance:", calculateSalary(baseSalary, freelanceCalculator)); // 8,000,000
```

### Functions returning Functions:

```javascript
// Hàm trả về hàm khác
function createMultiplier(factor) {
    return function(number) {
        return number * factor;
    };
}

// Tạo các hàm nhân với factor khác nhau
let double = createMultiplier(2);
let triple = createMultiplier(3);
let quadruple = createMultiplier(4);

console.log(double(5));    // 10
console.log(triple(4));    // 12
console.log(quadruple(3)); // 12

// Ví dụ với Arrow Functions
let createGreeter = (greeting) => (name) => `${greeting}, ${name}!`;

let sayHello = createGreeter("Xin chào");
let sayGoodbye = createGreeter("Tạm biệt");

console.log(sayHello("An"));    // "Xin chào, An!"
console.log(sayGoodbye("Bình")); // "Tạm biệt, Bình!"

// Closure example - Hàm counter
function createCounter() {
    let count = 0;
    
    return {
        increment: () => ++count,
        decrement: () => --count,
        getValue: () => count,
        reset: () => count = 0
    };
}

let counter1 = createCounter();
let counter2 = createCounter();

console.log(counter1.increment()); // 1
console.log(counter1.increment()); // 2
console.log(counter2.increment()); // 1 (independent counter)
console.log(counter1.getValue());  // 2
```

### Functional Array Methods:

```javascript
let students = [
    { name: 'An', score: 85, subject: 'Math' },
    { name: 'Bình', score: 92, subject: 'Physics' },
    { name: 'Chi', score: 78, subject: 'Math' },
    { name: 'Dũng', score: 88, subject: 'Physics' },
    { name: 'Em', score: 95, subject: 'Math' }
];

// map - Transform data
let studentNames = students.map(student => student.name);
console.log("Tên học sinh:", studentNames);

let scoresWithBonus = students.map(student => ({
    ...student,
    finalScore: student.score + 5
}));

// filter - Select data
let highScorers = students.filter(student => student.score >= 90);
console.log("Học sinh điểm cao:", highScorers);

let mathStudents = students.filter(student => student.subject === 'Math');
console.log("Học sinh môn Toán:", mathStudents);

// reduce - Aggregate data
let totalScore = students.reduce((sum, student) => sum + student.score, 0);
let averageScore = totalScore / students.length;
console.log(`Điểm trung bình: ${averageScore.toFixed(2)}`);

// find - Find single item
let topStudent = students.find(student => student.score >= 95);
console.log("Học sinh xuất sắc:", topStudent);

// some & every - Boolean checks
let hasHighScorer = students.some(student => student.score >= 90);
let allPassed = students.every(student => student.score >= 60);

console.log("Có học sinh điểm cao:", hasHighScorer); // true
console.log("Tất cả đều đạt:", allPassed); // true
```

### Composition Functions:

```javascript
// Function composition - Kết hợp nhiều hàm
let add1 = x => x + 1;
let multiply2 = x => x * 2;
let square = x => x * x;

// Manual composition
let result1 = square(multiply2(add1(3))); // ((3+1)*2)^2 = 64

// Compose function helper
let compose = (f, g) => x => f(g(x));
let pipe = (...fns) => x => fns.reduce((acc, fn) => fn(acc), x);

// Sử dụng compose
let addThenMultiply = compose(multiply2, add1);
console.log(addThenMultiply(3)); // (3+1)*2 = 8

// Sử dụng pipe
let transform = pipe(add1, multiply2, square);
console.log(transform(3)); // ((3+1)*2)^2 = 64

// Ví dụ thực tế - Xử lý dữ liệu
let processData = pipe(
    data => data.filter(item => item.active),
    data => data.map(item => ({ ...item, processed: true })),
    data => data.sort((a, b) => b.score - a.score)
);

let data = [
    { name: 'A', score: 85, active: true },
    { name: 'B', score: 92, active: false },
    { name: 'C', score: 78, active: true }
];

console.log(processData(data));
```

### Lợi ích của lập trình hàm:

```javascript
// 1. Reusability - Tái sử dụng
let validators = {
    isNotEmpty: value => value && value.trim().length > 0,
    isEmail: value => /\S+@\S+\.\S+/.test(value),
    isMinLength: min => value => value && value.length >= min,
    isMaxLength: max => value => value && value.length <= max
};

let validateField = (value, ...validatorFns) => {
    for (let validator of validatorFns) {
        if (!validator(value)) return false;
    }
    return true;
};

// Sử dụng validators
let email = "user@example.com";
let isValidEmail = validateField(
    email,
    validators.isNotEmpty,
    validators.isEmail,
    validators.isMinLength(5)
);

console.log("Email hợp lệ:", isValidEmail); // true

// 2. Immutability - Không thay đổi dữ liệu gốc
let originalArray = [1, 2, 3, 4, 5];

// Bad - mutates original array
// originalArray.push(6);

// Good - returns new array
let newArray = [...originalArray, 6];
let doubled = originalArray.map(x => x * 2);

console.log("Original:", originalArray); // [1, 2, 3, 4, 5]
console.log("New:", newArray);          // [1, 2, 3, 4, 5, 6]
console.log("Doubled:", doubled);       // [2, 4, 6, 8, 10]

// 3. Pure Functions - Không có side effects
// Pure function - same input always gives same output
let pureAdd = (a, b) => a + b;

// Impure function - depends on external state
let counter = 0;
let impureAdd = (a, b) => {
    counter++; // side effect
    return a + b + counter;
};

console.log(pureAdd(2, 3));   // Always 5
console.log(pureAdd(2, 3));   // Always 5

console.log(impureAdd(2, 3)); // 6 (2+3+1)
console.log(impureAdd(2, 3)); // 7 (2+3+2)
```

## 5. Ví dụ Tổng Hợp - Hệ thống Quản lý Sản phẩm

```javascript
// Functional approach to product management
const ProductManager = {
    // Pure functions for data transformation
    createProduct: (name, price, category) => ({
        id: Date.now(),
        name,
        price,
        category,
        active: true,
        createdAt: new Date().toISOString()
    }),

    // Higher-order functions
    createFilter: (field, value) => (product) => product[field] === value,
    createSorter: (field, direction = 'asc') => (a, b) => {
        if (direction === 'asc') {
            return a[field] > b[field] ? 1 : -1;
        }
        return a[field] < b[field] ? 1 : -1;
    },

    // Function composition for complex operations
    processProducts: (products, filters = [], sorters = []) => {
        return products
            .filter(product => filters.every(filter => filter(product)))
            .sort((a, b) => {
                for (let sorter of sorters) {
                    let result = sorter(a, b);
                    if (result !== 0) return result;
                }
                return 0;
            });
    },

    // Utility functions
    calculateTotal: (products) => products.reduce((sum, p) => sum + p.price, 0),
    getCategories: (products) => [...new Set(products.map(p => p.category))],
    
    // Analytics functions
    getStatistics: (products) => ({
        total: products.length,
        active: products.filter(p => p.active).length,
        totalValue: products.reduce((sum, p) => sum + p.price, 0),
        avgPrice: products.length > 0 
            ? products.reduce((sum, p) => sum + p.price, 0) / products.length 
            : 0,
        categories: [...new Set(products.map(p => p.category))].length
    })
};

// Usage example
let products = [
    ProductManager.createProduct("Laptop Dell", 15000000, "Electronics"),
    ProductManager.createProduct("iPhone 15", 25000000, "Electronics"),
    ProductManager.createProduct("Áo thun", 200000, "Fashion"),
    ProductManager.createProduct("Giày Nike", 2000000, "Fashion"),
    ProductManager.createProduct("Sách JavaScript", 300000, "Books")
];

console.log("=== TẤT CẢ SẢN PHẨM ===");
products.forEach(p => console.log(`${p.name}: ${p.price.toLocaleString()} VNĐ`));

// Filter and sort
let electronicsFilter = ProductManager.createFilter("category", "Electronics");
let priceSorter = ProductManager.createSorter("price", "desc");

let expensiveElectronics = ProductManager.processProducts(
    products,
    [electronicsFilter],
    [priceSorter]
);

console.log("\n=== ĐIỆN TỬ (GIÁ CAO ĐẾN THẤP) ===");
expensiveElectronics.forEach(p => console.log(`${p.name}: ${p.price.toLocaleString()} VNĐ`));

// Analytics
let stats = ProductManager.getStatistics(products);
console.log("\n=== THỐNG KÊ ===");
console.log(`Tổng số sản phẩm: ${stats.total}`);
console.log(`Sản phẩm hoạt động: ${stats.active}`);
console.log(`Tổng giá trị: ${stats.totalValue.toLocaleString()} VNĐ`);
console.log(`Giá trung bình: ${stats.avgPrice.toLocaleString()} VNĐ`);
console.log(`Số danh mục: ${stats.categories}`);
```

## Kết luận

JavaScript hỗ trợ nhiều kiểu hàm khác nhau, từ **hàm truyền thống**, **hàm ẩn danh**, đến **hàm mũi tên**. Việc hiểu và sử dụng đúng các loại hàm này sẽ giúp bạn viết mã dễ đọc, dễ bảo trì và hiệu quả hơn.

### Tóm tắt những điều quan trọng:

#### **1. Function Declaration vs Function Expression:**
- **Function Declaration**: Có thể gọi trước khi khai báo (hoisting)
- **Function Expression**: Chỉ có thể gọi sau khi khai báo

#### **2. Arrow Functions:**
- ✅ Ngắn gọn, dễ đọc
- ✅ Không có `this` riêng
- ✅ Tốt cho callbacks và functional programming
- ❌ Không nên dùng cho object methods

#### **3. Functional Programming Benefits:**
- **Reusability**: Code có thể tái sử dụng
- **Maintainability**: Dễ bảo trì và debug
- **Testability**: Dễ test với pure functions
- **Scalability**: Dễ mở rộng và tổ chức code

#### **4. Best Practices:**
- Sử dụng **pure functions** khi có thể
- Tránh **side effects** không cần thiết
- Áp dụng **function composition** cho logic phức tạp
- Sử dụng **arrow functions** cho callbacks đơn giản

**Lập trình hàm** là một phương pháp mạnh mẽ trong JavaScript, giúp bạn xử lý dữ liệu và xây dựng các ứng dụng linh hoạt hơn. Hãy tiếp tục thực hành và thử nghiệm với các loại hàm trong JavaScript để nâng cao kỹ năng lập trình của mình.

Trong bài viết tiếp theo, chúng ta sẽ tìm hiểu về **DOM Manipulation** - cách JavaScript tương tác với HTML để tạo ra các trang web động và tương tác!

---

**Từ khóa**: JavaScript Functions, Arrow Functions, Anonymous Functions, Functional Programming, Higher-order Functions, Callbacks, Pure Functions, Function Composition, ES6 Functions.
