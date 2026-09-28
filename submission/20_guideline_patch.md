# Guideline patch — Đề xuất bổ sung quy tắc gán nhãn

- **Rule mới đề xuất (R11):** 
  - *Quy tắc phân định ThreeWheeler chở hàng với Truck nhỏ:* Đối với các phương tiện giao thông đặc thù có cơ cấu 3 bánh (kể cả xe tự chế, xe kéo ba bánh có gắn thùng hàng lớn phía sau hoặc tay lái dạng ghi-đông/xe máy), bắt buộc phải phân loại là `ThreeWheeler`. Chỉ phân loại là `Truck` khi phương tiện có cabin lái kín hoàn toàn, vô lăng ô tô hoặc có từ 4 bánh xe trở lên.
- **Áp dụng cho:** Class `ThreeWheeler` và `Truck`, đặc biệt ở vùng `mid` và `edge` khi xe bị biến dạng góc nhìn nghiêng.
- **Vì sao luật hiện tại (`docs/02-rules-vi.md`) không đủ:**
  - Quy tắc R04 trong guideline v1.0.0 chỉ nêu nguyên tắc chung: *"xe ba bánh chở người/hàng → ThreeWheeler; xe bán tải nhỏ hoặc máy kéo → Truck"*.
  - Tuy nhiên, trong tập dữ liệu thực tế ADASIND, xuất hiện nhiều xe ba bánh chở hàng có thùng hàng rất to phía sau che khuất phần đầu xe, khiến cả người gán nhãn lẫn mô hình AI thường nhầm thành xe tải chở hàng (Truck). Việc bổ sung tiêu chí nhận diện dựa trên cấu trúc tay lái và cabin giúp giải quyết triệt để sự nhập nhằng này.
- **`rules_version` mới:** v1.1.0 (nâng cấp từ v1.0.0)
- **Hiệu lực từ:** Áp dụng ngay từ vòng `rework` và áp dụng cho toàn bộ các lô dữ liệu tiếp theo.
