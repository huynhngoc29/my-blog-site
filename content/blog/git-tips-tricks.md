---
title: "Git Tips & Tricks cho Developer"
date: 2025-10-16
draft: false
tags: ["git", "version-control", "developer-tips"]
categories: ["Development"]
description: "Những tips và tricks hữu ích khi làm việc với Git"
---

# Git Tips & Tricks cho Developer

Git là công cụ không thể thiếu đối với mọi developer. Dưới đây là một số tips và tricks hữu ích để làm việc hiệu quả hơn với Git.

## 1. Git Aliases - Tạo shortcuts

Tạo các alias để rút ngắn các lệnh Git thường dùng:

```bash
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.st status
git config --global alias.lg "log --oneline --graph --all"
```

## 2. Commit Messages Best Practices

### Cấu trúc commit message

```
<type>(<scope>): <subject>

<body>

<footer>
```

### Ví dụ:

```
feat(auth): add login functionality

Implement user login with email and password validation.
Include error handling for invalid credentials.

Closes #123
```

### Các loại commit phổ biến:

- `feat`: Tính năng mới
- `fix`: Sửa bug
- `docs`: Cập nhật documentation
- `style`: Thay đổi formatting, spacing
- `refactor`: Refactor code
- `test`: Thêm hoặc sửa tests
- `chore`: Maintenance tasks

## 3. Useful Git Commands

### Xem history đẹp mắt

```bash
git log --oneline --graph --all --decorate
```

### Stash với message

```bash
git stash push -m "Work in progress on feature X"
```

### Cherry-pick multiple commits

```bash
git cherry-pick commit1^..commit2
```

### Reset soft để sửa commit message

```bash
git reset --soft HEAD~1
git commit -m "New commit message"
```

## 4. Gitflow Workflow

### Khởi tạo gitflow

```bash
git flow init
```

### Tạo feature branch

```bash
git flow feature start new-feature
git flow feature finish new-feature
```

### Tạo release branch

```bash
git flow release start 1.0.0
git flow release finish 1.0.0
```

## 5. Git Hooks

### Pre-commit hook để check coding standards

Tạo file `.git/hooks/pre-commit`:

```bash
#!/bin/sh
# Run tests before commit
npm test
if [ $? -ne 0 ]; then
    echo "Tests must pass before commit!"
    exit 1
fi
```

## 6. Resolving Merge Conflicts

### Sử dụng merge tool

```bash
git config --global merge.tool vimdiff
git mergetool
```

### Abort merge khi cần thiết

```bash
git merge --abort
```

## 7. Rebase vs Merge

### Khi nào dùng rebase:

- Feature branches nhỏ
- Muốn giữ history tuyến tính
- Trước khi merge vào main branch

### Khi nào dùng merge:

- Feature branches lớn với nhiều commits
- Collaborative features
- Muốn preserve context của feature

## Kết luận

Git là công cụ mạnh mẽ với rất nhiều tính năng. Việc nắm vững các commands và workflows sẽ giúp bạn làm việc hiệu quả hơn và tránh được những rắc rối không đáng có.

---

*Keep coding and keep learning! 💪*
