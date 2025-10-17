---
title: "Lập Trình Bất Đồng Bộ (Asynchronous Programming) trong JavaScript"
date: 2025-10-17
draft: false
description: "Tìm hiểu về lập trình bất đồng bộ trong JavaScript: Callback Functions, Promise và Async/Await. Học cách xử lý các tác vụ dài mà không làm đóng băng ứng dụng."
categories: ["Programming", "JavaScript", "Async"]
tags: ["JavaScript", "Asynchronous", "Callbacks", "Promise", "Async/Await", "API", "Async Programming", "ES6", "ES8"]
author: "Phan Thị Huỳnh Ngọc"
slug: "lap-trinh-bat-dong-bo-asynchronous-programming-trong-javascript"
---

# Lập Trình Bất Đồng Bộ (Asynchronous Programming) trong JavaScript

Trong khi **lập trình đồng bộ** (synchronous programming) thực thi các lệnh theo thứ tự, **lập trình bất đồng bộ** (asynchronous programming) cho phép chương trình tiếp tục chạy mà không phải chờ đợi kết quả của các phép toán hoặc thao tác khác. 

Điều này rất hữu ích trong các tình huống như đọc tệp, gọi API, hay xử lý yêu cầu từ người dùng, vì bạn không muốn chương trình bị "đóng băng" trong khi chờ đợi. JavaScript cung cấp một số cách tiếp cận để xử lý bất đồng bộ, bao gồm **Callback Functions**, **Promise**, và **Async/Await**.

## 1. Hiểu về Synchronous vs Asynchronous

### Synchronous (Đồng bộ) - Blocking:

```javascript
console.log("Bắt đầu");

// Code đồng bộ - chặn luồng chính
function synchronousTask() {
    console.log("Đang xử lý...");
    
    // Giả lập tác vụ mất thời gian (blocking)
    let start = Date.now();
    while (Date.now() - start < 3000) {
        // Chờ 3 giây (blocking main thread)
    }
    
    console.log("Hoàn thành sau 3 giây!");
}

synchronousTask();
console.log("Kết thúc");

// Output:
// Bắt đầu
// Đang xử lý...
// (chờ 3 giây - UI bị đóng băng)
// Hoàn thành sau 3 giây!
// Kết thúc
```

### Asynchronous (Bất đồng bộ) - Non-blocking:

```javascript
console.log("Bắt đầu");

// Code bất đồng bộ - không chặn luồng chính
function asynchronousTask() {
    console.log("Đang xử lý...");
    
    // setTimeout không chặn main thread
    setTimeout(() => {
        console.log("Hoàn thành sau 3 giây!");
    }, 3000);
}

asynchronousTask();
console.log("Kết thúc");

// Output:
// Bắt đầu
// Đang xử lý...
// Kết thúc
// (sau 3 giây)
// Hoàn thành sau 3 giây!
```

### Ví dụ thực tế - Tại sao cần Async:

```javascript
// ❌ Synchronous approach - UI bị đóng băng
function loadDataSync() {
    console.log("Bắt đầu tải dữ liệu...");
    
    // Giả lập việc tải dữ liệu từ server (blocking)
    let start = Date.now();
    while (Date.now() - start < 2000) {} // 2 giây blocking
    
    console.log("Dữ liệu đã tải xong");
    console.log("UI có thể tương tác trở lại");
}

// ✅ Asynchronous approach - UI không bị ảnh hưởng
function loadDataAsync() {
    console.log("Bắt đầu tải dữ liệu...");
    console.log("UI vẫn tương tác được trong khi tải");
    
    setTimeout(() => {
        console.log("Dữ liệu đã tải xong");
        console.log("Cập nhật UI với dữ liệu mới");
    }, 2000);
}

loadDataAsync();
console.log("Có thể làm việc khác trong khi chờ dữ liệu");
```

## 2. Callback Functions

**Callback Functions** là một trong những cách đơn giản để xử lý bất đồng bộ trong JavaScript. Một callback function là một hàm được truyền vào một hàm khác dưới dạng tham số, và được gọi khi công việc trong hàm trước đó hoàn thành.

### Cấu trúc Callback cơ bản:

```javascript
function greet(name, callback) {
    console.log(`Hello, ${name}!`);
    // Gọi callback sau khi hoàn thành
    callback();
}

function sayGoodbye() {
    console.log("Goodbye, Alice!");
}

// Sử dụng callback
greet("Alice", sayGoodbye);

// Output:
// Hello, Alice!
// Goodbye, Alice!
```

### Callback với setTimeout:

```javascript
function doSomething(message, callback) {
    console.log(`Bắt đầu: ${message}`);
    
    setTimeout(() => {
        console.log(`Hoàn thành: ${message}`);
        callback(`Kết quả từ ${message}`);
    }, 1000);
}

function handleResult(result) {
    console.log(`Xử lý: ${result}`);
}

doSomething("Tác vụ 1", handleResult);
console.log("Code này chạy ngay lập tức");

// Output:
// Bắt đầu: Tác vụ 1
// Code này chạy ngay lập tức
// (sau 1 giây)
// Hoàn thành: Tác vụ 1
// Xử lý: Kết quả từ Tác vụ 1
```

### Ví dụ thực tế - File Reading với Callback:

```javascript
// Giả lập việc đọc file
function readFile(filename, callback) {
    console.log(`Đang đọc file: ${filename}`);
    
    setTimeout(() => {
        // Giả lập có thể thành công hoặc thất bại
        const success = Math.random() > 0.3;
        
        if (success) {
            const content = `Nội dung của ${filename}`;
            callback(null, content); // null = không có lỗi
        } else {
            callback(new Error(`Không thể đọc file ${filename}`), null);
        }
    }, 1500);
}

// Sử dụng callback với error handling
readFile("data.txt", (error, content) => {
    if (error) {
        console.error("Lỗi:", error.message);
    } else {
        console.log("Đọc file thành công:", content);
    }
});

// Ví dụ xâu chuỗi callbacks
function processData() {
    readFile("config.json", (err, config) => {
        if (err) {
            console.error("Lỗi đọc config:", err.message);
            return;
        }
        
        console.log("Config loaded:", config);
        
        readFile("data.csv", (err, data) => {
            if (err) {
                console.error("Lỗi đọc data:", err.message);
                return;
            }
            
            console.log("Data loaded:", data);
            console.log("Xử lý hoàn tất!");
        });
    });
}

processData();
```

### Vấn đề Callback Hell:

```javascript
// ❌ Callback Hell - Khó đọc và maintain
function callbackHell() {
    getData1((err, data1) => {
        if (err) {
            console.error(err);
            return;
        }
        
        getData2(data1, (err, data2) => {
            if (err) {
                console.error(err);
                return;
            }
            
            getData3(data2, (err, data3) => {
                if (err) {
                    console.error(err);
                    return;
                }
                
                processData(data3, (err, result) => {
                    if (err) {
                        console.error(err);
                        return;
                    }
                    
                    console.log("Final result:", result);
                });
            });
        });
    });
}

// Giả lập các hàm getData
function getData1(callback) {
    setTimeout(() => callback(null, "Data 1"), 1000);
}

function getData2(data1, callback) {
    setTimeout(() => callback(null, data1 + " + Data 2"), 1000);
}

function getData3(data2, callback) {
    setTimeout(() => callback(null, data2 + " + Data 3"), 1000);
}

function processData(data3, callback) {
    setTimeout(() => callback(null, `Processed: ${data3}`), 1000);
}
```

**Lưu ý**: Mặc dù callback là cách đơn giản để xử lý bất đồng bộ, nhưng chúng có thể dẫn đến một vấn đề gọi là **callback hell** (địa ngục callback), khi bạn phải lồng nhiều callback vào nhau, gây khó khăn trong việc quản lý và đọc mã.

## 3. Promise

**Promise** là một cải tiến so với callback functions, giúp quản lý các tác vụ bất đồng bộ trở nên dễ dàng và rõ ràng hơn. Promise có thể có ba trạng thái:

- **Pending**: Trạng thái ban đầu, khi chưa có kết quả
- **Resolved (Fulfilled)**: Trạng thái khi tác vụ hoàn thành thành công
- **Rejected**: Trạng thái khi có lỗi xảy ra

### Cấu trúc Promise cơ bản:

```javascript
// Tạo Promise
function createPromise(success) {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            if (success) {
                resolve("Thành công!"); // Chuyển sang trạng thái resolved
            } else {
                reject(new Error("Có lỗi xảy ra!")); // Chuyển sang trạng thái rejected
            }
        }, 2000);
    });
}

// Sử dụng Promise
createPromise(true)
    .then(result => {
        console.log("Kết quả:", result); // "Kết quả: Thành công!"
    })
    .catch(error => {
        console.error("Lỗi:", error.message);
    })
    .finally(() => {
        console.log("Promise đã hoàn thành (thành công hay thất bại)");
    });
```

**Giải thích:**
- Khi `success` là `true`, `resolve` được gọi và trạng thái của Promise sẽ chuyển sang resolved
- Nếu `success` là `false`, `reject` được gọi và trạng thái của Promise sẽ chuyển sang rejected
- `then()` được sử dụng để xử lý kết quả khi Promise hoàn thành thành công
- `catch()` để xử lý lỗi nếu có
- `finally()` luôn được thực thi bất kể thành công hay thất bại

### Promise Chaining:

```javascript
// Ví dụ về chuỗi Promise
function fetchUserData(userId) {
    return new Promise((resolve, reject) => {
        console.log(`Đang lấy thông tin user ${userId}...`);
        setTimeout(() => {
            if (userId > 0) {
                resolve({ 
                    id: userId, 
                    name: `User ${userId}`, 
                    email: `user${userId}@example.com` 
                });
            } else {
                reject(new Error("Invalid user ID"));
            }
        }, 1000);
    });
}

function fetchUserPosts(user) {
    return new Promise((resolve, reject) => {
        console.log(`Đang lấy bài viết của ${user.name}...`);
        setTimeout(() => {
            const posts = [
                { id: 1, title: "Bài viết 1", content: "Nội dung 1" },
                { id: 2, title: "Bài viết 2", content: "Nội dung 2" }
            ];
            resolve({ user, posts });
        }, 1000);
    });
}

function processUserData(userData) {
    return new Promise((resolve) => {
        console.log("Đang xử lý dữ liệu...");
        setTimeout(() => {
            const processed = {
                ...userData,
                summary: `${userData.user.name} có ${userData.posts.length} bài viết`
            };
            resolve(processed);
        }, 500);
    });
}

// Sử dụng Promise chaining
fetchUserData(1)
    .then(user => {
        console.log("User data:", user);
        return fetchUserPosts(user);
    })
    .then(userData => {
        console.log("User posts:", userData.posts);
        return processUserData(userData);
    })
    .then(result => {
        console.log("Kết quả cuối cùng:", result.summary);
    })
    .catch(error => {
        console.error("Có lỗi trong quá trình xử lý:", error.message);
    });
```

### Promise.all và Promise.race:

```javascript
// Promise.all - Chờ tất cả promises hoàn thành
function task1() {
    return new Promise(resolve => {
        setTimeout(() => resolve("Task 1 completed"), 2000);
    });
}

function task2() {
    return new Promise(resolve => {
        setTimeout(() => resolve("Task 2 completed"), 1500);
    });
}

function task3() {
    return new Promise(resolve => {
        setTimeout(() => resolve("Task 3 completed"), 1000);
    });
}

// Chạy tất cả tasks song song
console.log("Bắt đầu chạy tất cả tasks...");
Promise.all([task1(), task2(), task3()])
    .then(results => {
        console.log("Tất cả tasks hoàn thành:", results);
        // ["Task 1 completed", "Task 2 completed", "Task 3 completed"]
    })
    .catch(error => {
        console.error("Có task thất bại:", error);
    });

// Promise.race - Lấy kết quả của promise hoàn thành đầu tiên
Promise.race([task1(), task2(), task3()])
    .then(result => {
        console.log("Task hoàn thành đầu tiên:", result);
        // "Task 3 completed" (vì nó nhanh nhất - 1 giây)
    })
    .catch(error => {
        console.error("Task đầu tiên thất bại:", error);
    });

// Promise.allSettled - Chờ tất cả promises (kể cả thất bại)
Promise.allSettled([
    Promise.resolve("Success 1"),
    Promise.reject("Error 1"),
    Promise.resolve("Success 2")
])
.then(results => {
    console.log("Tất cả promises đã settled:", results);
    results.forEach((result, index) => {
        if (result.status === 'fulfilled') {
            console.log(`Promise ${index}: Success -`, result.value);
        } else {
            console.log(`Promise ${index}: Failed -`, result.reason);
        }
    });
});
```

### Lợi ích của Promise:

```javascript
// ✅ Promise giải quyết callback hell
function betterDataProcessing() {
    return getData1()
        .then(data1 => {
            console.log("Got data1:", data1);
            return getData2(data1);
        })
        .then(data2 => {
            console.log("Got data2:", data2);
            return getData3(data2);
        })
        .then(data3 => {
            console.log("Got data3:", data3);
            return processData(data3);
        })
        .then(result => {
            console.log("Final result:", result);
            return result;
        })
        .catch(error => {
            console.error("Error in processing chain:", error.message);
            throw error; // Re-throw if needed
        });
}

// Chuyển đổi callbacks thành Promises
function promisifyReadFile(filename) {
    return new Promise((resolve, reject) => {
        readFile(filename, (error, content) => {
            if (error) {
                reject(error);
            } else {
                resolve(content);
            }
        });
    });
}

// Sử dụng
promisifyReadFile("data.txt")
    .then(content => {
        console.log("File content:", content);
    })
    .catch(error => {
        console.error("File read error:", error.message);
    });
```

**Promise giúp:**
- Viết mã dễ đọc và dễ bảo trì hơn
- Có thể xâu chuỗi nhiều `then()` để xử lý các kết quả liên tiếp
- Error handling tốt hơn với `catch()`
- Tránh được callback hell

## 4. Async/Await

**Async/Await** là một cú pháp được giới thiệu trong JavaScript ES2017 (ES8) để làm việc với Promise một cách dễ dàng hơn và tránh callback hell. Cú pháp này giúp bạn viết mã bất đồng bộ giống như mã đồng bộ, giúp cải thiện tính dễ đọc và dễ hiểu của chương trình.

### Cấu trúc Async/Await:

- **async**: Đảm bảo rằng hàm trả về một Promise
- **await**: Dừng chương trình cho đến khi Promise trả về kết quả

```javascript
// Hàm async cơ bản
async function fetchData() {
    try {
        console.log("Bắt đầu tải dữ liệu...");
        
        // await dừng thực thi cho đến khi Promise resolve
        const response = await fetch('https://jsonplaceholder.typicode.com/users/1');
        const data = await response.json();
        
        console.log("Dữ liệu đã tải:", data);
        return data;
    } catch (error) {
        console.error("Lỗi khi tải dữ liệu:", error.message);
        throw error;
    }
}

// Gọi hàm async
fetchData()
    .then(data => {
        console.log("Xử lý dữ liệu:", data.name);
    })
    .catch(error => {
        console.error("Xử lý lỗi:", error.message);
    });
```

**Giải thích:**
- Hàm `fetchData` được khai báo là `async`, điều này có nghĩa là hàm này sẽ trả về một Promise
- `await` dừng thực thi chương trình cho đến khi `fetch` trả về một kết quả, sau đó xử lý kết quả đó
- Kết quả sẽ được in ra sau khi dữ liệu được tải xong

### So sánh Promise vs Async/Await:

```javascript
// ❌ Promise chaining - có thể phức tạp
function fetchUserWithPromises(userId) {
    return fetch(`/api/users/${userId}`)
        .then(response => {
            if (!response.ok) {
                throw new Error(`HTTP ${response.status}`);
            }
            return response.json();
        })
        .then(user => {
            console.log("User:", user);
            return fetch(`/api/users/${userId}/posts`);
        })
        .then(response => {
            if (!response.ok) {
                throw new Error(`HTTP ${response.status}`);
            }
            return response.json();
        })
        .then(posts => {
            console.log("Posts:", posts);
            return { user, posts };
        })
        .catch(error => {
            console.error("Error:", error.message);
            throw error;
        });
}

// ✅ Async/Await - dễ đọc hơn
async function fetchUserWithAsync(userId) {
    try {
        console.log(`Fetching user ${userId}...`);
        
        const userResponse = await fetch(`/api/users/${userId}`);
        if (!userResponse.ok) {
            throw new Error(`HTTP ${userResponse.status}`);
        }
        const user = await userResponse.json();
        console.log("User:", user);
        
        console.log("Fetching user posts...");
        const postsResponse = await fetch(`/api/users/${userId}/posts`);
        if (!postsResponse.ok) {
            throw new Error(`HTTP ${postsResponse.status}`);
        }
        const posts = await postsResponse.json();
        console.log("Posts:", posts);
        
        return { user, posts };
    } catch (error) {
        console.error("Error:", error.message);
        throw error;
    }
}
```

### Xử lý lỗi với try-catch:

```javascript
async function handleMultipleOperations() {
    try {
        // Có thể xử lý nhiều operations với error handling rõ ràng
        console.log("Step 1: Validating user...");
        const isValid = await validateUser();
        
        if (!isValid) {
            throw new Error("User validation failed");
        }
        
        console.log("Step 2: Loading configuration...");
        const config = await loadConfig();
        
        console.log("Step 3: Processing data...");
        const processedData = await processUserData(config);
        
        console.log("Step 4: Saving results...");
        const saveResult = await saveToDatabase(processedData);
        
        console.log("All operations completed successfully!");
        return saveResult;
        
    } catch (error) {
        console.error("Operation failed:", error.message);
        
        // Có thể xử lý cụ thể từng loại lỗi
        if (error.message.includes("validation")) {
            console.log("Redirecting to login page...");
        } else if (error.message.includes("network")) {
            console.log("Checking network connection...");
        }
        
        throw error; // Re-throw nếu cần
    } finally {
        console.log("Cleanup operations...");
        // Code này luôn chạy bất kể thành công hay thất bại
    }
}

// Giả lập các async functions
async function validateUser() {
    await new Promise(resolve => setTimeout(resolve, 1000));
    return Math.random() > 0.2; // 80% thành công
}

async function loadConfig() {
    await new Promise(resolve => setTimeout(resolve, 800));
    return { theme: "dark", language: "vi" };
}

async function processUserData(config) {
    await new Promise(resolve => setTimeout(resolve, 1200));
    return { processed: true, config };
}

async function saveToDatabase(data) {
    await new Promise(resolve => setTimeout(resolve, 500));
    return { id: Date.now(), saved: true, data };
}
```

### Tại sao sử dụng Async/Await?

#### 1. **Dễ đọc và dễ duy trì**:

```javascript
// Async/Await giúp code trông giống synchronous
async function getUserProfile(userId) {
    try {
        const user = await fetchUser(userId);
        const avatar = await fetchUserAvatar(user.avatarId);
        const preferences = await fetchUserPreferences(userId);
        const friends = await fetchUserFriends(userId);
        
        return {
            ...user,
            avatar,
            preferences,
            friends
        };
    } catch (error) {
        console.error("Failed to load user profile:", error);
        return null;
    }
}
```

#### 2. **Xử lý lỗi dễ dàng**:

```javascript
async function robustDataFetching() {
    try {
        const primaryData = await fetchFromPrimarySource();
        return primaryData;
    } catch (primaryError) {
        console.warn("Primary source failed, trying backup...");
        
        try {
            const backupData = await fetchFromBackupSource();
            return backupData;
        } catch (backupError) {
            console.error("Both sources failed");
            throw new Error("All data sources unavailable");
        }
    }
}
```

#### 3. **Parallel execution với Promise.all**:

```javascript
async function loadDashboardData() {
    try {
        console.log("Loading dashboard data...");
        
        // Chạy song song để tăng hiệu suất
        const [users, posts, comments, analytics] = await Promise.all([
            fetchUsers(),
            fetchPosts(),
            fetchComments(),
            fetchAnalytics()
        ]);
        
        console.log("All data loaded successfully");
        
        return {
            users: users.length,
            posts: posts.length,
            comments: comments.length,
            pageViews: analytics.pageViews
        };
    } catch (error) {
        console.error("Failed to load dashboard:", error);
        throw error;
    }
}

// Giả lập fetch functions
async function fetchUsers() {
    await new Promise(resolve => setTimeout(resolve, 1000));
    return Array(10).fill().map((_, i) => ({ id: i, name: `User ${i}` }));
}

async function fetchPosts() {
    await new Promise(resolve => setTimeout(resolve, 1200));
    return Array(25).fill().map((_, i) => ({ id: i, title: `Post ${i}` }));
}

async function fetchComments() {
    await new Promise(resolve => setTimeout(resolve, 800));
    return Array(150).fill().map((_, i) => ({ id: i, text: `Comment ${i}` }));
}

async function fetchAnalytics() {
    await new Promise(resolve => setTimeout(resolve, 1500));
    return { pageViews: 50000, uniqueVisitors: 12000 };
}
```

## 5. Ví dụ Tổng Hợp - Ứng dụng Quản lý Dữ liệu

```javascript
// Ứng dụng thực tế sử dụng tất cả các kỹ thuật async
class DataManager {
    constructor(apiBaseUrl) {
        this.apiBaseUrl = apiBaseUrl;
        this.cache = new Map();
        this.retryCount = 3;
    }
    
    // Callback approach (legacy)
    fetchDataWithCallback(endpoint, callback) {
        console.log(`Fetching ${endpoint} with callback...`);
        
        setTimeout(() => {
            const success = Math.random() > 0.3;
            if (success) {
                const data = { endpoint, data: `Data from ${endpoint}`, timestamp: Date.now() };
                callback(null, data);
            } else {
                callback(new Error(`Failed to fetch ${endpoint}`), null);
            }
        }, 1000);
    }
    
    // Promise approach
    fetchDataWithPromise(endpoint) {
        console.log(`Fetching ${endpoint} with Promise...`);
        
        return new Promise((resolve, reject) => {
            // Kiểm tra cache trước
            if (this.cache.has(endpoint)) {
                console.log(`Cache hit for ${endpoint}`);
                resolve(this.cache.get(endpoint));
                return;
            }
            
            setTimeout(() => {
                const success = Math.random() > 0.2;
                if (success) {
                    const data = { 
                        endpoint, 
                        data: `Promise data from ${endpoint}`, 
                        timestamp: Date.now() 
                    };
                    this.cache.set(endpoint, data);
                    resolve(data);
                } else {
                    reject(new Error(`Promise: Failed to fetch ${endpoint}`));
                }
            }, 800);
        });
    }
    
    // Async/Await approach with retry logic
    async fetchDataWithAsync(endpoint, retries = this.retryCount) {
        console.log(`Fetching ${endpoint} with async/await (${this.retryCount - retries + 1}/${this.retryCount})...`);
        
        try {
            // Kiểm tra cache
            if (this.cache.has(endpoint)) {
                console.log(`Cache hit for ${endpoint}`);
                return this.cache.get(endpoint);
            }
            
            // Giả lập API call
            const data = await this.simulateApiCall(endpoint);
            this.cache.set(endpoint, data);
            
            console.log(`Successfully fetched ${endpoint}`);
            return data;
            
        } catch (error) {
            console.warn(`Attempt failed for ${endpoint}:`, error.message);
            
            if (retries > 0) {
                console.log(`Retrying ${endpoint}... (${retries} attempts left)`);
                await this.delay(1000); // Chờ 1 giây trước khi retry
                return this.fetchDataWithAsync(endpoint, retries - 1);
            }
            
            throw new Error(`Failed to fetch ${endpoint} after ${this.retryCount} attempts`);
        }
    }
    
    // Utility method
    simulateApiCall(endpoint) {
        return new Promise((resolve, reject) => {
            setTimeout(() => {
                const success = Math.random() > 0.4;
                if (success) {
                    resolve({
                        endpoint,
                        data: `Async data from ${endpoint}`,
                        timestamp: Date.now(),
                        source: 'api'
                    });
                } else {
                    reject(new Error(`API call failed for ${endpoint}`));
                }
            }, 600);
        });
    }
    
    delay(ms) {
        return new Promise(resolve => setTimeout(resolve, ms));
    }
    
    // Complex workflow combining all approaches
    async loadCompleteDataset() {
        console.log("=== Loading Complete Dataset ===");
        
        try {
            // Step 1: Load essential data with async/await
            console.log("Step 1: Loading essential data...");
            const essentialData = await this.fetchDataWithAsync('essential');
            
            // Step 2: Load multiple datasets in parallel
            console.log("Step 2: Loading multiple datasets in parallel...");
            const [users, posts, settings] = await Promise.all([
                this.fetchDataWithPromise('users'),
                this.fetchDataWithPromise('posts'),
                this.fetchDataWithAsync('settings')
            ]);
            
            // Step 3: Process data with callback (legacy system integration)
            console.log("Step 3: Processing with legacy system...");
            const processedData = await new Promise((resolve, reject) => {
                this.processWithLegacySystem(users, posts, (error, result) => {
                    if (error) reject(error);
                    else resolve(result);
                });
            });
            
            // Step 4: Final aggregation
            const finalResult = {
                essential: essentialData,
                users: users.data,
                posts: posts.data,
                settings: settings.data,
                processed: processedData,
                summary: {
                    totalItems: users.data.length + posts.data.length,
                    loadedAt: new Date().toISOString(),
                    cacheHits: Array.from(this.cache.keys()).length
                }
            };
            
            console.log("✅ Complete dataset loaded successfully!");
            return finalResult;
            
        } catch (error) {
            console.error("❌ Failed to load complete dataset:", error.message);
            throw error;
        }
    }
    
    // Legacy callback function simulation
    processWithLegacySystem(users, posts, callback) {
        console.log("Processing with legacy system...");
        setTimeout(() => {
            try {
                const result = {
                    processedUsers: users.data.length,
                    processedPosts: posts.data.length,
                    status: 'processed'
                };
                callback(null, result);
            } catch (error) {
                callback(error, null);
            }
        }, 500);
    }
}

// Sử dụng DataManager
async function demonstrateAsyncProgramming() {
    const dataManager = new DataManager('https://api.example.com');
    
    try {
        // Demo callback
        console.log("\n=== Callback Demo ===");
        dataManager.fetchDataWithCallback('callback-demo', (error, data) => {
            if (error) {
                console.error("Callback error:", error.message);
            } else {
                console.log("Callback success:", data);
            }
        });
        
        // Demo Promise
        console.log("\n=== Promise Demo ===");
        const promiseData = await dataManager.fetchDataWithPromise('promise-demo');
        console.log("Promise result:", promiseData);
        
        // Demo Async/Await
        console.log("\n=== Async/Await Demo ===");
        const asyncData = await dataManager.fetchDataWithAsync('async-demo');
        console.log("Async/Await result:", asyncData);
        
        // Demo complete workflow
        console.log("\n=== Complete Workflow Demo ===");
        const completeData = await dataManager.loadCompleteDataset();
        console.log("Complete dataset summary:", completeData.summary);
        
    } catch (error) {
        console.error("Demo failed:", error.message);
    }
}

// Chạy demonstration
demonstrateAsyncProgramming();
```

## 6. Best Practices và Common Patterns

### Error Handling Patterns:

```javascript
// Pattern 1: Global error handler
class AsyncErrorHandler {
    static async withRetry(asyncFn, retries = 3, delay = 1000) {
        for (let i = 0; i < retries; i++) {
            try {
                return await asyncFn();
            } catch (error) {
                console.warn(`Attempt ${i + 1} failed:`, error.message);
                if (i === retries - 1) throw error;
                await new Promise(resolve => setTimeout(resolve, delay));
            }
        }
    }
    
    static async withTimeout(asyncFn, timeoutMs = 5000) {
        return Promise.race([
            asyncFn(),
            new Promise((_, reject) => 
                setTimeout(() => reject(new Error('Operation timeout')), timeoutMs)
            )
        ]);
    }
}

// Sử dụng
async function robustOperation() {
    try {
        const result = await AsyncErrorHandler.withTimeout(
            () => AsyncErrorHandler.withRetry(
                () => fetch('/api/critical-data').then(r => r.json()),
                3,
                2000
            ),
            10000
        );
        return result;
    } catch (error) {
        console.error('Robust operation failed:', error.message);
        return { error: true, message: error.message };
    }
}
```

### Performance Patterns:

```javascript
// Pattern 2: Batching and caching
class PerformantAsyncManager {
    constructor() {
        this.cache = new Map();
        this.pendingRequests = new Map();
    }
    
    async batchFetch(urls) {
        const batchSize = 5;
        const results = [];
        
        for (let i = 0; i < urls.length; i += batchSize) {
            const batch = urls.slice(i, i + batchSize);
            const batchPromises = batch.map(url => this.fetchWithCache(url));
            const batchResults = await Promise.allSettled(batchPromises);
            results.push(...batchResults);
        }
        
        return results;
    }
    
    async fetchWithCache(url) {
        // Check cache first
        if (this.cache.has(url)) {
            return this.cache.get(url);
        }
        
        // Check if request is already pending
        if (this.pendingRequests.has(url)) {
            return this.pendingRequests.get(url);
        }
        
        // Create new request
        const promise = fetch(url)
            .then(response => response.json())
            .then(data => {
                this.cache.set(url, data);
                this.pendingRequests.delete(url);
                return data;
            })
            .catch(error => {
                this.pendingRequests.delete(url);
                throw error;
            });
        
        this.pendingRequests.set(url, promise);
        return promise;
    }
}
```

## Kết luận

**Lập trình bất đồng bộ** là một phần quan trọng trong việc phát triển ứng dụng JavaScript, đặc biệt là khi làm việc với các tác vụ dài hoặc yêu cầu thời gian như gọi API, đọc tệp, hoặc xử lý dữ liệu. 

Trong bài viết này, chúng ta đã tìm hiểu ba cách chính để xử lý bất đồng bộ trong JavaScript:

### **1. Callback Functions**: 
- ✅ Phương pháp đơn giản và cơ bản
- ❌ Có thể dẫn đến callback hell
- 🎯 Phù hợp cho: Legacy code, simple operations

### **2. Promise**: 
- ✅ Cung cấp một cách quản lý bất đồng bộ dễ dàng hơn
- ✅ Giúp tránh callback hell với chaining
- ✅ Error handling tốt hơn với `.catch()`
- 🎯 Phù hợp cho: Complex async workflows, API calls

### **3. Async/Await**: 
- ✅ Cú pháp mạnh mẽ giúp làm việc với bất đồng bộ giống như mã đồng bộ
- ✅ Dễ đọc và dễ duy trì nhất
- ✅ Error handling với try-catch
- ✅ Tốt nhất cho modern JavaScript
- 🎯 Phù hợp cho: Modern applications, complex logic

### **Key Takeaways:**

#### **Khi nào sử dụng từng approach:**
- **Callbacks**: Legacy systems, simple operations
- **Promises**: Chaining operations, working with multiple async tasks
- **Async/Await**: Modern applications, complex business logic

#### **Best Practices:**
- Sử dụng `Promise.all()` cho parallel execution
- Implement retry logic cho network requests  
- Cache kết quả để tăng performance
- Handle errors properly ở mọi level
- Use timeout để tránh hang indefinitely

#### **Common Patterns:**
- Error boundary pattern
- Retry with exponential backoff
- Request batching và deduplication
- Circuit breaker pattern for resilience

Hiểu rõ và áp dụng các kỹ thuật này sẽ giúp bạn phát triển các ứng dụng JavaScript **mạnh mẽ**, **responsive** và **dễ bảo trì**. Hãy tiếp tục thực hành và thử nghiệm với các công cụ và phương thức bất đồng bộ để cải thiện kỹ năng lập trình của mình!

Trong bài viết tiếp theo, chúng ta sẽ tìm hiểu về **DOM Manipulation** - cách JavaScript tương tác với HTML elements để tạo ra các trang web động và interactive!

---

**Từ khóa**: JavaScript Async, Asynchronous Programming, Promise, Async/Await, Callbacks, API calls, Error Handling, Performance Optimization, Modern JavaScript.
