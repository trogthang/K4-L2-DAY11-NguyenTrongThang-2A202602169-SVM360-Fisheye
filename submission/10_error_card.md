# Error analysis card

## Zone × block

| zone | block | what | count |
|---|---|---|---:|
| center | B3 | MISSING | 5 |
| center | B3 | SPURIOUS | 4 |
| center | B3 | WRONG_CLASS | 1 |
| edge | B3 | ATTRIBUTE | 1 |
| edge | B3 | IGNORE_SCOPE | 3 |
| edge | B3 | MISSING | 1 |
| edge | B3 | SPURIOUS | 3 |
| edge | B3 | WRONG_CLASS | 1 |
| mid | B3 | ATTRIBUTE | 1 |
| mid | B3 | MISSING | 5 |
| mid | B3 | SPURIOUS | 3 |
| mid | B3 | WRONG_CLASS | 2 |

## Top defects
- MISSING: 11 (ví dụ frame adasind_230910.jpg)
- SPURIOUS: 10 (ví dụ frame adasind_128310.jpg)
- WRONG_CLASS: 4 (ví dụ frame adasind_140160.jpg)

## Phân tích của bạn

- **Nguyên nhân khả dĩ (`why`) và lập luận:**
  - Lỗi chiếm đa số trong slice B3-mid là **MISSING** (11 ca) và **SPURIOUS** (10 ca), tập trung chủ yếu ở hai vùng `center` và `mid`.
  - Trên frame `adasind_230910.jpg`, các đối tượng đi bộ và phương tiện ở xa tâm đường có kích thước nhỏ, nằm sát ngưỡng chiều cao $H=40\text{ px}$ và bị cây cối/phương tiện khác che khuất một phần (occluded). Điều này khiến cả mô hình AI lẫn người gán nhãn dễ bỏ qua nếu chỉ lướt nhanh mà không zoom kỹ vùng hậu cảnh.
  - Lỗi **WRONG_CLASS** (4 ca, điển hình trên `adasind_140160.jpg`): Biến dạng quang học hình cầu của camera fisheye làm phương tiện ở vùng mid và edge bị bóp méo tỷ lệ (aspect ratio), dẫn đến nhầm lẫn giữa xe ba bánh (ThreeWheeler) với xe tải nhỏ (Truck) hoặc xe bán tải chở hàng.
  - Lỗi **SPURIOUS** ở vùng edge: Vành đen quang học (lens border) và các bóng đổ gắt ở góc mép ảnh khiến bộ nhận diện dễ bắt nhầm các mảng tối thành xe cộ nếu không bao phủ polygon `ignore_region` cẩn thận.
- **Cách sửa và phân công (`owner`):**
  - *Sửa nhãn và bổ sung box thiếu:* Annotator (`owner: self`) rà soát lại toàn bộ 3 frame theo phương pháp quét từ tâm ra rìa (center $\to$ mid $\to$ edge), đo chiều cao hộp kiểm tra ngưỡng $H \ge 40\text{ px}$ và áp dụng đúng luật ánh xạ phương tiện R04 để tách ThreeWheeler khỏi Truck.
  - *Chuẩn hóa ignore region:* Nhóm thảo luận thống nhất (`owner: team/guideline`) vẽ chính xác polygon `ego_body` ở mép dưới và kiểm tra viền `lens_border` không để lọt box phương tiện vào trong vùng loại trừ.
- **Bằng chứng:**
  - Quy tắc áp dụng: R01 (ngưỡng kích thước $\ge 40\text{ px}$), R03 (quy tắc rider gộp người và xe hai bánh), R04 (ánh xạ phương tiện đặc thù), R06/R07 (vùng ignore_region và ego_body).
  - Ảnh minh chứng đối chiếu trực quan lưu tại `submission/screenshots/error_edge_distortion.png` (hiện tượng méo rìa làm nhầm class) và `submission/screenshots/error_missing_small_object.png` (bỏ sót vật thể nhỏ ở hậu cảnh).
