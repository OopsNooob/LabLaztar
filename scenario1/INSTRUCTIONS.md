# Scenario 1: Merge Conflict - Accept Incoming or Current Changes

## Mục tiêu:
Tạo conflict khi merge 2 nhánh và giải quyết bằng cách chọn **Accept Incoming** hoặc **Accept Current**.

## Các bước thực hiện:

### Step 1: Khởi tạo repo và tạo commit đầu tiên
```bash
cd scenario1
git init
git config user.name "Your Name"
git config user.email "your@email.com"
git add .
git commit -m "Initial commit: Create website structure"
```

### Step 2: Tạo nhánh feature
```bash
git branch feature/update-header
```

### Step 3: Chỉnh sửa trên main branch
Sửa file `index.html` - đổi:
- `<p>Main Branch Version</p>` → `<p>Updated in Main Branch</p>`

Rồi commit:
```bash
git add index.html
git commit -m "Update header text in main branch"
```

### Step 4: Chuyển sang feature branch và sửa cùng dòng
```bash
git checkout feature/update-header
```

Sửa file `index.html` - đổi cùng dòng:
- `<p>Main Branch Version</p>` → `<p>Updated in Feature Branch</p>`

Rồi commit:
```bash
git add index.html
git commit -m "Update header text in feature branch"
```

### Step 5: Merge và gặp conflict
```bash
git checkout main
git merge feature/update-header
```

**Kết quả:** Git sẽ báo CONFLICT vì 2 nhánh sửa cùng 1 dòng!

### Step 6: Xem conflict trong file
File `index.html` sẽ có dạng:
```html
<<<<<<< HEAD (Current Change)
        <p>Updated in Main Branch</p>
=======
        <p>Updated in Feature Branch</p>
>>>>>>> feature/update-header (Incoming Change)
```

### Step 7: Giải quyết conflict

#### Cách 1: Dùng VS Code
- Mở `index.html`
- Chọn **"Accept Current Change"** (giữ main branch) HOẶC **"Accept Incoming Change"** (lấy feature branch)

#### Cách 2: Manual edit
Xóa các marker (`<<<<<<<`, `=======`, `>>>>>>>`) và giữ nội dung bạn muốn

#### Cách 3: Command line
```bash
# Chọn version từ main (current)
git checkout --ours index.html

# HOẶC chọn version từ feature (incoming)
git checkout --theirs index.html
```

### Step 8: Hoàn thành merge
```bash
git add index.html
git commit -m "Resolve merge conflict: Accept current/incoming changes"
```

### Step 9: Xác nhận merge thành công
```bash
git log --oneline --graph --all
```

---

## Key Concepts:
- **HEAD** = Current Branch (nhánh hiện tại)
- **Incoming** = Branch bị merge vào
- Khi conflict xảy ra ở cùng dòng → phải chọn 1 trong 2 hoặc sửa manual
