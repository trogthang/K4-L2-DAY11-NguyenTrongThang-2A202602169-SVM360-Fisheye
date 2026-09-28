# Kế hoạch review từ lỗi quan sát được

Từ `findings.csv` và `zone_table.md`, tôi chọn **hai lát cắt của bài ADASIND một camera** cần được ưu tiên review trước:

| Lát cắt / frame | Số ca và loại lỗi | Vì sao review trước | Bằng chứng cần giữ |
|---|---|---|---|
| `adasind_140160.jpg` (Vùng edge/mid) | 6 ca (MISSING 1, SPURIOUS 2, WRONG_CLASS 2, IGNORE_SCOPE 1) | Vùng có mật độ giao thông hỗn hợp cao, méo quang học fisheye lớn nhất và xuất hiện ca tranh chấp phân loại ThreeWheeler vs Truck sát vành kính. | Ảnh chụp màn hình vùng rìa, file so sánh overlay đối chiếu với reference R, bảng thuộc tính `truncated` và `reason` của polygon. |
| `adasind_230910.jpg` (Vùng center/mid) | 10 ca (MISSING 5 ca vật thể xa, SPURIOUS 3, ATTRIBUTE 2) | Chứa số lượng phương tiện và người đi bộ ở xa tâm đường nhiều nhất, dễ dẫn tới lỗi bỏ sót do vật thể nhỏ sát ngưỡng chiều cao $H=40\text{ px}$. | Bảng đo kích thước pixel (xtl, ytl, xbr, ybr), ảnh zoom chi tiết hậu cảnh và đối chiếu với quy tắc R01 (ngưỡng 40 px). |

- **Giới hạn của kết luận từ ba frame ADASIND:**
  - Kết luận chỉ được rút ra trên 3 khung hình cắt đoạn từ một camera fisheye gắn phía trước trong điều kiện ban ngày khô ráo tại Ấn Độ.
  - Kích thước mẫu quá nhỏ nên chưa phản ánh được các điều kiện biến đổi môi trường khác (ban đêm, mưa ướt, chói sáng ngược chiều), không có thông tin tracking động học và hoàn toàn thiếu vắng góc nhìn từ 3 camera còn lại quanh xe (rear, left, right).

## Chuyển sang kế hoạch bốn camera giả lập

- **Phương pháp soát độ phủ 200 frame:**
  - Nhóm thiết lập bảng phân bổ phân tầng (stratified sampling) chia đều cho 4 vị trí camera quanh thân xe (Front, Rear, Left, Right) với hai nhóm kịch bản: `normal` (50%) và `hard` (50%).
  - Để tránh thiên lệch (bias) do tự tương quan thời gian giữa các khung hình liên tiếp trong cùng một chuỗi video, thuật toán lấy mẫu bắt buộc giãn cách tối thiểu 30–50 frames giữa hai mẫu được chọn trong cùng một hành trình (temporal subsampling), đồng thời phân tán mẫu qua nhiều bối cảnh khác nhau (đô thị đông đúc, đường cao tốc, bãi đỗ chật hẹp, ngã tư).
- **Ý nghĩa của kế hoạch lấy mẫu:**
  - Kế hoạch 200 frame này được thiết kế có chủ đích hướng tới việc **săn tìm và khai phá các ca lỗi góc khuất (edge cases / hard cases)** thay vì lấy mẫu ngẫu nhiên đồng đều. Do đó, tập mẫu này phục vụ hoàn hảo cho việc xây dựng benchmark và gold set để phát hiện lỗi của mô hình/người gán nhãn, nhưng **chưa thể suy rộng thành tỷ lệ lỗi thống kê tổng thể** của toàn bộ hệ thống 50.000 frame trong sản xuất.
