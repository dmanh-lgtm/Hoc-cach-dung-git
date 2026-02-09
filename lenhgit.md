# 📚 Ghi chép lộ trình học Git

### 🧠 Khái niệm cốt lõi
* **Commit:** Là một trạng thái, một **snapshot** (ảnh chụp) của toàn bộ file, thư mục hoặc repository tại một thời điểm nhất định.
* **Branch (Nhánh):** Là một nhánh chứa các commit của chính nó và toàn bộ các commit trước đó.
* **Pointer (Con trỏ):** Trong Git luôn có một con trỏ (thường gọi là `HEAD`) đang đứng tại một commit hoặc một nhánh cụ thể.

---

### 1. Lưu phiên bản (Commit)
* **Lệnh:** `git commit -m "Lưu ghi chú cho thay đổi"`
* **Ý nghĩa:** Lưu lại phiên bản mới nhất của code so với phiên bản trước đó.
* > **Gemini:** Hãy coi `git commit` là hành động "chụp ảnh" trạng thái code hiện tại và dán cho nó một cái nhãn để dễ dàng tìm lại sau này.

### 2. Tạo nhánh (Branch)
* **Lệnh:** `git branch <Tên nhánh>`
* **Ý nghĩa:** Tạo một nhánh mới trỏ ngay vào commit hiện tại bạn đang đứng.

### 3. Di chuyển con trỏ (Checkout)
* **Lệnh:** `git checkout <Tên nhánh>`
* **Ý nghĩa:** Di chuyển con trỏ đến một nhánh khác để làm việc.
* **Mẹo:** Để tạo nhanh nhánh mới và nhảy sang nhánh đó ngay lập tức, dùng:  
    `git checkout -b <Tên nhánh>`

---

### 4. Gộp nhánh (Merge)
* **Lệnh:** `git merge <Tên nhánh>`
* **Cơ chế:** Lệnh này tạo ra một commit mới (Merge Commit) và chuyển nhánh hiện tại đến commit này. Commit mới sẽ có **2 commit cha** (cha từ nhánh hiện tại và cha từ nhánh vừa gộp).

#### 💡 Ví dụ minh họa:
Giả sử bạn có 2 nhánh là **bugFix** và **main**, bạn đang đứng ở **main**.

1.  **Gộp bugFix vào main:** Gõ `git merge bugFix`. Git tạo một commit mới. Nhánh `main` sẽ trỏ vào commit mới này. Commit này chứa nội dung của cả `main` cũ và `bugFix`.
    
2.  **Đưa bugFix lên cùng vị trí với main:** * Bước 1: `git checkout bugFix` (Nhảy sang nhánh bugFix).
    * Bước 2: `git merge main`.
    * **Kết quả:** Vì `bugFix` là tổ tiên của commit mới mà `main` đang đứng, Git sẽ chỉ đơn giản là di chuyển con trỏ `bugFix` lên thẳng vị trí của `main` (gọi là Fast-forward).

---