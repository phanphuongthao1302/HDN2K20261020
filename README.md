# Bản Đồ Ăn Chung

Trang web một file (`index.html`) để cả nhóm cùng lưu quán ăn, đánh giá, ảnh kỷ niệm và lọc theo người vắng mặt.

Trên GitHub Pages chỉ chạy được file tĩnh, nên dữ liệu dùng chung được lưu ở Firebase Firestore (gói miễn phí Spark là đủ). Chưa cấu hình Firebase thì trang vẫn chạy, nhưng mỗi người chỉ thấy dữ liệu trong trình duyệt của mình.

## Bước 1. Tạo cơ sở dữ liệu Firebase
1. Vào https://console.firebase.google.com, tạo dự án mới (tắt Google Analytics cũng được).
2. Menu **Build > Firestore Database > Create database**. Chọn vị trí `asia-southeast1` (Singapore), chế độ production.
3. Tab **Rules**: xóa nội dung cũ, dán toàn bộ file `firestore.rules`, bấm **Publish**.

## Bước 2. Lấy cấu hình và dán vào index.html
1. **Project settings (biểu tượng bánh răng) > Your apps > biểu tượng Web `</>`**, đặt tên rồi bấm Register app.
2. Chép 4 giá trị `apiKey`, `authDomain`, `projectId`, `appId`.
3. Mở `index.html`, tìm khối `window.FIREBASE_CONFIG` gần cuối file và thay các chữ `DIEN_VAO_DAY`.

## Bước 3. Đăng lên GitHub Pages
1. Tạo repo mới trên GitHub, tải `index.html` lên (nhánh `main`).
2. **Settings > Pages > Build and deployment**: chọn *Deploy from a branch*, nhánh `main`, thư mục `/ (root)`, bấm Save.
3. Sau 1 đến 2 phút, link có dạng `https://<tên-github>.github.io/<tên-repo>/`. Gửi link này cho cả nhóm.

## Lưu ý
- **Ai có link đều thêm, sửa, xóa được.** Đó là ý bạn muốn, nhưng người lạ nhặt được link cũng làm được. Đừng đăng link công khai. Nếu bị phá, vào Firestore xóa hoặc sửa dữ liệu, hoặc đổi rule thành `allow delete: if false;`.
- `apiKey` của Firebase nằm trong file là bình thường, không phải bí mật. Việc ai được đọc, ghi do file `firestore.rules` quyết định.
- Ảnh được nén nhỏ và lưu trong chính dữ liệu của quán (tối đa 2 ảnh quán và 2 ảnh kỷ niệm), để khỏi phải dùng Firebase Storage có tính phí.
- Muốn đổi danh sách người vắng mặt, sửa dòng `const MEMBERS=[...]` trong `index.html`.
