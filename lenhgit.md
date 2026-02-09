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
* **Cơ chế:** Tạo ra một commit mới (Merge Commit) nối hai nhánh lại với nhau. Nhánh hiện tại sẽ trỏ vào commit mới này. Commit này có **2 cha**.



#### 💡 Ví dụ minh họa:
Giả sử bạn có 2 nhánh là **bugFix** và **main**, bạn đang đứng ở **main**.

1.  **Gộp bugFix vào main:** Gõ `git merge bugFix`. Git tạo một commit mới. Nhánh `main` sẽ trỏ vào commit mới này.
2.  **Đưa bugFix lên cùng vị trí với main:** * Bước 1: `git checkout bugFix`.
    * Bước 2: `git merge main`.
    * **Kết quả:** Vì `bugFix` là tổ tiên của `main`, Git thực hiện **Fast-forward** (chỉ đơn giản là kéo con trỏ `bugFix` lên đứng cùng `main`).

---

### 5. Di dời nhánh (Rebase)
* **Lệnh:** `git rebase <Tên nhánh mục tiêu>`
* **Cơ chế:** Thay vì tạo commit gộp, Rebase sẽ "nhấc" toàn bộ các commit mới của nhánh hiện tại và "đặt nối tiếp" vào điểm cuối của nhánh mục tiêu. Điều này tạo ra một lịch sử code **thẳng hàng**, sạch sẽ.



#### 💡 Ví dụ minh họa:
Giả sử bạn đang ở nhánh phụ `docs` và muốn cập nhật những thay đổi mới nhất từ nhánh `main`.

1. **Thực hiện Rebase:**
   * Di chuyển sang nhánh phụ: `git checkout docs`.
   * Chạy lệnh: `git rebase main`.
   * **Kết quả:** Các commit của `docs` giờ đây sẽ nằm trên đỉnh của các commit mới nhất từ `main`.

2. **Cập nhật lại nhánh main:**
   * Quay lại main: `git checkout main`.
   * Gộp nhánh: `git merge docs`.
   * **Kết quả:** Do các commit đã nối thẳng hàng, nhánh `main` chỉ cần "Fast-forward" đến vị trí cuối của `docs`. Lịch sử dự án sẽ cực kỳ đẹp và không có nhánh rẽ.

---