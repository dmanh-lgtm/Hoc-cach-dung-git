# 📚 Ghi Chép Lộ Trình Học Git Toàn Tập

### 🧠 Khái niệm nền tảng
* **Commit:** Một "snapshot" (ảnh chụp) trạng thái của file/thư mục/repo tại một thời điểm.
* **Branch (Nhánh):** Một con trỏ chứa các commit của chính nó và lịch sử trước đó.
* **HEAD:** Con trỏ đặc biệt luôn xác định vị trí bạn đang đứng (tại commit hoặc nhánh nào).

---

## I. Thao tác Cơ bản (Main)

### 1. Lưu phiên bản (Commit)
* **Lệnh:** `git commit -m "Lưu ghi chú cho thay đổi"`
* **Ý nghĩa:** Lưu lại phiên bản mới nhất.
* > **💡 Mẹo:** Hãy coi `git commit` là hành động "chụp ảnh" trạng thái code và dán nhãn để dễ dàng tìm lại.

### 2. Tạo nhánh (Branch)
* **Lệnh:** `git branch <Tên nhánh>`
* **Ý nghĩa:** Tạo một nhánh mới trỏ ngay vào commit hiện tại.

### 3. Di chuyển (Checkout)
* **Lệnh:** `git checkout <Tên nhánh>` (Di chuyển con trỏ sang nhánh khác).
* **Lệnh tắt:** `git checkout -b <Tên nhánh>` (Vừa tạo vừa nhảy sang nhánh mới).

### 4. Gộp nhánh (Merge)
* **Lệnh:** `git merge <Tên nhánh>`
* **Cơ chế:** Tạo ra một **Merge Commit** nối hai nhánh lại. Commit này có **2 cha**.

#### 💡 Ví dụ minh họa:
Giả sử bạn đang ở `main` và muốn gộp `bugFix`:
1.  Gõ `git merge bugFix` -> `main` trỏ vào commit mới có 2 cha.
2.  Để `bugFix` cũng lên vị trí đó: `git checkout bugFix` -> `git merge main`. 
3.  **Kết quả:** Git thực hiện **Fast-forward** (kéo thẳng con trỏ lên) vì không có sự phân nhánh mới.

### 5. Di dời nhánh (Rebase)
* **Lệnh:** `git rebase <Tên nhánh mục tiêu>`
* **Cơ chế:** "Nhấc" các commit nhánh hiện tại đặt nối tiếp vào cuối nhánh mục tiêu.
* **Lưu ý:** Thường dùng cho nhánh phụ để cập nhật từ nhánh chính mà không làm rối lịch sử.

---

---

## II. Điều hướng và Quản lý Commit (Relative Refs)

### 6. Di chuyển con trỏ HEAD
* **Lùi bước với `~`**: `git checkout HEAD~<number>`
  * Ý nghĩa: Lùi lại `n` bước trên đường thẳng.
* **Lùi bước với `^`**: `git checkout HEAD^`
  * Ý nghĩa: Lùi lại 1 bước. 
  * **Mẹo:** Sử dụng `HEAD^1` hoặc `HEAD^2` để chọn cha cụ thể khi bạn đang đứng ở một **Merge Commit** (commit có 2 cha).

### 7. Di chuyển nhánh tự do (Force Move)
* **Lệnh:** `git branch -f <tên nhánh> <vị trí/mã hash>`
* **Ý nghĩa:** Ép một nhánh phải trỏ vào một commit bất kỳ. 
* **Ứng dụng:** Giúp tìm lại các commit bị ẩn hoặc sửa nhanh lỗi vị trí của nhánh.

### 8. Hoàn tác thay đổi (Reset & Revert)
* **Git Reset:** `git reset HEAD~1` (Di chuyển nhánh về vị trí cũ).
  * `--soft`: Giữ code đã sửa ở vùng Staging (sẵn sàng để commit lại).
  * `--mixed`: (Mặc định) Giữ code ở vùng làm việc (Working directory) nhưng chưa add vào Staging.
  * `--hard`: Xóa sạch mọi thay đổi, đưa code về trạng thái cũ hoàn toàn.
* **Git Revert:** `git revert HEAD`
  * **Cơ chế:** Tạo một commit mới đảo ngược lại toàn bộ thay đổi của commit cũ. 
  * **Ưu điểm:** Cực kỳ an toàn cho làm việc nhóm vì không làm mất lịch sử commit.

### 9. Nhặt Commit (Cherry-pick)
* **Lệnh:** `git cherry-pick C2 C4`
* **Ý nghĩa:** Sao chép các commit cụ thể (ở đây là C2 và C4) và dán chúng vào ngay sau vị trí `HEAD` hiện tại.

### 10. Chỉnh sửa lịch sử (Interactive Rebase)
* **Lệnh:** `git rebase -i HEAD~<number>`
* **Các tùy chọn trong giao diện:**
  * `Drop`: Xóa bỏ commit đó.
  * `Squash`: Gộp commit đó vào commit phía trước.
  * `Reword`: Chỉ sửa lại nội dung tin nhắn (message) commit.
  * `Edit`: Dừng lại để sửa nội dung code bên trong commit.

---

## III. Nhãn và Thông tin (Tags)

### 11. Đánh dấu phiên bản (Tag)
* **Lệnh:** `git tag <Tên tag> <commit>` 
  * Ý nghĩa: Gắn nhãn cố định vào một commit (không di chuyển như Branch).
* **Annotated Tag:** `git tag -a v1 -m "Message" <commit>`
  * Ý nghĩa: Tạo tag chứa thêm thông tin người tạo, ngày tháng và tin nhắn.

### 12. Mô tả vị trí (Describe)
* **Lệnh:** `git describe <commit>`
* **Kết quả:** Trả về chuỗi `<tag>-<số commit từ tag>-g<mã hash>`. Giúp bạn biết mình đang cách tag gần nhất bao xa.

---

## IV. Làm việc với Remote (GitHub)

### 13. Tải dự án (Clone)
* **Lệnh:** `git clone <link>`
* **Remote Branch:** Các nhánh có tiền tố `origin/`. Bạn không thể tự di chuyển các nhánh này trừ khi thực hiện lệnh đồng bộ.

### 14. Đồng bộ dữ liệu (Fetch, Pull, Push)
* **Fetch:** `git fetch` 
  * Ý nghĩa: Tải dữ liệu mới từ server về nhưng **chưa gộp** vào code local của bạn.
* **Pull:** `git pull`
  * Ý nghĩa: Kết hợp giữa `fetch` và `merge`. Cập nhật và gộp luôn vào code đang làm.
* **Push:** `git push`
  * Ý nghĩa: Đẩy các thay đổi từ local lên server.
  * **Xóa nhánh remote:** `git push origin :<tên nhánh>`

### 15. Theo dõi nhánh (Remote Tracking)
* **Cách 1:** `git checkout -b <nhánh_local> origin/<nhánh_remote>`
* **Cách 2:** `git branch -u origin/<nhánh_remote> <nhánh_local>`
* **Cách 3:** `git push -u origin <nhánh_remote>`

---

## V. Xử lý xung đột (Diverged Work)
* **Tình huống:** Xảy ra khi lịch sử máy local và server khác nhau (ví dụ: bạn sửa C3, đồng nghiệp đã đẩy C4 lên trước).
* **Cách giải quyết tối ưu:**
  1. `git fetch`: Để lấy commit C4 của đồng nghiệp về.
  2. `git rebase origin/main`: Để nhấc commit C3 của bạn đặt lên trên đầu C4.
  3. **Xử lý conflict:** (Nếu có) sau đó dùng `git add` và `git rebase --continue`.
  4. `git push`: Đẩy kết quả đã được nối thẳng hàng lên server.
