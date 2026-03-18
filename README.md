# Luca_bot_guide
# Hướng dẫn sử dụng Bot Telegram (Chat bot forward)

## 1. Giới thiệu

Bot dùng để **chuyển tin nhắn hai chiều** giữa nhóm khách hàng (Client) và nhóm nhân viên/leader (Staff/Leader), kèm quản lý vai trò và kết nối 1–1 theo từng nhóm.

**Chức năng chính:**
- Quản lý Leaders, Staffs, Clients (thêm/xóa/xem danh sách)
- Tạo kết nối giữa một group Client và một group Staff
- Forward tin nhắn (text, ảnh, file, video, audio, voice, sticker) giữa hai nhóm đã kết nối

---

## 2. Phân quyền

| Vai trò | Quyền |
|--------|--------|
| **Admin** | Toàn quyền: thêm/xóa Leader, Staff, Client; xem danh sách; tạo kết nối. |
| **Leader** | Thêm/xóa Staff; tạo kết nối (Connect); xem List Staff/Leader/Client; nhắn với Client đã kết nối. |
| **Staff** | Nhắn với Client đã kết nối; Check ID. |
| **Client** | Nhắn với Staff/Leader đã kết nối; Check ID. |

---

## 3. Sử dụng trong Telegram

### 3.1 Khởi động

- Gửi **`/start`** → Bot hiển thị menu theo quyền (Admin/Leader thấy menu đầy đủ, Staff/Client chỉ thấy Check ID).

### 3.2 Menu chính (Admin / Leader)

- **Check ID 🆔** — Xem ID Telegram của bạn (lệnh `/getmyid`).
- **Staffs 👨‍💼** — Vào menu quản lý Staff.
- **Leaders 👑** — Vào menu quản lý Leader (chỉ Admin).
- **Clients 👥** — Vào menu quản lý Client.
- **Connect 🔗** — Tạo link kết nối (chỉ Leader; xem mục 3.6).

### 3.3 Quản lý Leader (chỉ Admin)

1. Chọn **Leaders 👑**.
2. **ADD Leader ➕**: Nhập lần lượt **ID** → **tên** → **username** (có hoặc không có `@`).
3. **Delete Leader ❌**: Nhập **ID** Leader cần xóa.
4. **List Leader 📋**: Xem danh sách Leader.

### 3.4 Quản lý Staff (Admin và Leader)

1. Chọn **Staffs 👨‍💼**.
2. **ADD Staff ➕**: Nhập **ID** → **tên**.
3. **Delete Staff ❌**: Nhập **ID** Staff cần xóa.
4. **List Staff 📋**: Xem danh sách Staff (nếu rỗng, bot báo "Chưa có Staff nào được thêm vào.").

### 3.5 Quản lý Client (Admin và Leader)

1. Chọn **Clients 👥**.
2. **ADD Client ➕**: Nhập **ID** → **tên**.
3. **Delete Client ❌**: Nhập **ID** Client cần xóa.
4. **List Client 📋**: Xem danh sách Client.

### 3.6 Tạo kết nối (Connect) — chỉ Leader

1. Leader chọn **Connect 🔗**.
2. Bot gửi một dòng dạng: `/connect <số_id>`.
3. Leader **copy** nguyên dòng đó và **gửi vào group cần kết nối** (group khách hàng).
4. Khi lệnh được gửi trong group đó, bot xử lý và kết nối: **group đó** ↔ **chat/group của Leader** (nơi Leader vừa bấm Connect).

**Lưu ý:**  
- Bot phải là thành viên (tốt nhất là admin) của cả hai phía (group client và group/nơi staff nhận tin).  
- Một group Client tại một thời điểm chỉ kết nối với một phía Staff; kết nối mới sẽ thay thế kết nối cũ.

### 3.7 Gửi tin nhắn sau khi đã kết nối

- Trong **group Client**: thành viên (Client) hoặc Leader gửi tin → bot forward sang group/nhóm Staff.
- Trong **group Staff**: Staff hoặc Leader gửi tin → bot forward sang group Client đã kết nối.
- Hỗ trợ: text, ảnh, file, video, audio, voice, sticker. Caption có thể có nhưng **không được chứa tag (@)**; nếu có tag (trừ username Leader đã cấu hình), bot có thể từ chối hoặc xử lý đặc biệt.

---

## 4. Lưu ý quan trọng

1. **Tag (@):** Không dùng tag trong nội dung tin nhắn (trừ username Leader đã được cấu hình).
2. **Quyền bot:** Nên đặt bot làm admin trong các group để đọc/gửi tin ổn định.
3. **Kết nối 1–1:** Mỗi group Client chỉ kết nối với một phía Staff; tạo Connect mới sẽ ghi đè kết nối cũ.

---

## 5. Xử lý sự cố

| Vấn đề | Gợi ý |
|--------|--------|
| Tin không được chuyển | Kiểm tra bot đã vào đủ 2 group chưa, có quyền gửi tin không; kiểm tra lại đã Connect đúng group chưa; tin không có tag. |
| Không thêm/xóa được Leader/Staff/Client | Kiểm tra bạn là Admin hoặc Leader (với Staff/Client); nhập đúng ID; ID chưa tồn tại khi thêm, đã tồn tại khi xóa. |
| List Staff/Leader/Client trống | Bình thường nếu chưa thêm ai; bot sẽ báo "Chưa có … được thêm vào." thay vì lỗi. |
| Connect không hoạt động | Thử tạo Connect lại; copy đúng nguyên dòng `/connect <id>`; gửi đúng vào group cần kết nối; bot đã vào group đó. |

---

## 6. Lấy ID Telegram

Bấm **Check ID 🆔** hoặc gửi **`/getmyid`** cho bot → bot trả về ID của bạn (dùng khi thêm Leader/Staff/Client).
