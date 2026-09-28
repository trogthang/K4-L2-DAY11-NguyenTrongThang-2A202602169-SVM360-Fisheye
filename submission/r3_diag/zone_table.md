# Zone table (slice của bạn)

Lệnh `python3 lab11.py model` tự ghi bảng số (cùng cách đếm với `r1_craft/compare.md` và `model_compare.md`); chạy lại lệnh sẽ cập nhật bảng và giữ nguyên phần nhận xét. Bạn chỉ viết mục Nhận xét.

| Zone | n_ref | L missing | L spurious | M missing (`LR_noM` + `R_only`) | M thừa (`LM_noR` + `M_only`) | Lỗi L chính (`what`) |
|---|---:|---:|---:|---:|---:|---|
| center | 8 | 3 | 2 | 3 | 3 | MISSING (2) |
| mid | 9 | 3 | 2 | 4 | 3 | WRONG_CLASS (2) |
| edge | 3 | 1 | 2 | 1 | 2 | WRONG_CLASS (1) |

## Nhận xét

- **Zone người (L) và model (M) gãy nhiều nhất:**
  - Về số lượng tuyệt đối, vùng **mid** là nơi cả người gán nhãn (L) và mô hình (M) gặp nhiều lỗi nhất (L missing 3, M missing 4, lỗi L chính là WRONG_CLASS 2 ca). Tiếp đến là vùng **center** với L missing 3 và lỗi chính là MISSING.
  - Vùng **edge** tuy có ít đối tượng hơn (n_ref=3) nhưng tỷ lệ lỗi tương đối cao (L missing 1, spurious 2; M missing 1, thừa 2).
- **Giả thuyết nguyên nhân và giới hạn:**
  - *Méo thấu kính fisheye:* Ở vùng mid và edge, độ cong quang học lớn khiến các vật thể bị biến dạng cong hình vòm, làm thay đổi tỷ lệ khung hình (aspect ratio) thông thường, dẫn tới model nhận diện nhầm lẫn giữa ThreeWheeler và Truck hoặc Bike.
  - *Ngưỡng kích thước ở vùng center:* Tại vùng center, các phương tiện di chuyển ở xa có kích thước gần ngưỡng H=40px, độ phân giải chi tiết thấp nên người gán nhãn dễ bỏ sót (MISSING).
  - *Giới hạn slice 3 frame:* Tập dữ liệu slice chỉ gồm 3 khung hình tĩnh cắt đoạn, không có thông tin liên tục theo thời gian (temporal context/tracking) nên không thể kiểm chứng sự dịch chuyển của các đối tượng đang di chuyển nhanh ở rìa khung hình.
