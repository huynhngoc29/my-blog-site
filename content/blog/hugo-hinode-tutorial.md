---
title: "Hướng dẫn tạo blog với Hugo và theme Hinode"
date: 2025-10-17
draft: false
tags: ["hugo", "static-site", "hinode", "web-development"]
categories: ["Tutorial"]
description: "Hướng dẫn chi tiết cách tạo một blog static với Hugo sử dụng theme Hinode"
---

# Tạo blog với Hugo và theme Hinode

Hugo là một static site generator rất mạnh mẽ và nhanh chóng. Trong bài viết này, tôi sẽ hướng dẫn bạn cách tạo một blog đẹp mắt sử dụng theme Hinode.

## Tại sao chọn Hugo?

- ⚡ **Tốc độ**: Build site cực nhanh
- 🎨 **Themes**: Có nhiều theme đẹp và chuyên nghiệp
- 📝 **Markdown**: Viết content bằng Markdown đơn giản
- 🔧 **Flexible**: Có thể customize theo ý muốn

## Tại sao chọn theme Hinode?

Theme Hinode có những ưu điểm:

- 🌟 Modern và responsive design
- 🎯 SEO-friendly
- 🌙 Dark/Light mode
- 📱 Mobile-first approach
- 🔍 Built-in search functionality

## Cài đặt

### 1. Cài đặt Hugo

```bash
# macOS
brew install hugo

# Ubuntu/Debian
sudo apt install hugo

# Windows
choco install hugo
```

### 2. Tạo site mới

```bash
hugo new site my-blog
cd my-blog
```

### 3. Thêm theme Hinode

```bash
git clone https://github.com/gethinode/hinode.git themes/hinode
```

### 4. Cấu hình hugo.toml

Cập nhật file `hugo.toml` với cấu hình cho theme Hinode:

```toml
baseURL = 'https://yourdomain.com'
languageCode = 'en-us'
title = 'My Blog'
theme = 'hinode'

[params]
  [params.main]
    description = "My personal blog"
```

## Tạo nội dung

### Tạo bài viết mới

```bash
hugo new blog/my-first-post.md
```

### Chạy development server

```bash
hugo server -D
```

Site sẽ chạy tại `http://localhost:1313`

## Kết luận

Hugo với theme Hinode là một combination tuyệt vời để tạo blog cá nhân. Theme này có đầy đủ tính năng và thiết kế hiện đại, phù hợp cho blogger và developer.

---

*Happy blogging! 🚀*
