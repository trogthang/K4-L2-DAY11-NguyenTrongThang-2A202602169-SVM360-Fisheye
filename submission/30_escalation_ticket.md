# Escalation ticket — Phiếu yêu cầu phân xử kỹ thuật

## Ticket 1: Phân xử vật thể méo nặng ở vùng rìa bị cắt bởi vành kính

- **Frame:** `adasind_140160.jpg`
- **Ảnh chụp:** `submission/screenshots/escalation_edge_occlusion.png`
- **Mô tả vấn đề:** Tại vùng rìa bên phải ảnh (tọa độ khoảng x: 940–1080, y: 920–1060), xuất hiện một phương tiện hai bánh di chuyển sát biên. Do góc nhìn fisheye méo cực đại và bị vành đen quang học che một phần, có sự bất đồng ý kiến giữa các thành viên: một ý kiến cho rằng cần gán nhãn `Bike` với `truncated=true`, trong khi ý kiến khác cho rằng nên khoanh polygon `ignore_region` với lý do `unreadable` vì khó nhìn rõ tư thế người lái.
- **Expected impact:** Nếu chính sách dán nhãn không thống nhất giữa các annotator, tập dữ liệu huấn luyện sẽ bị nhiễu nhãn ở vùng seam/edge, làm giảm độ tin cậy của thuật toán phát hiện chướng ngại vật ở góc mù phía trước xe.
- **Owner:** `guideline` / `qa`
- **Recommendation:** Trưởng nhóm guideline đưa ra quy định thống nhất: Khi vẫn còn nhận diện được ít nhất một bánh xe hoặc ghi-đông xe hai bánh, ưu tiên gán bounding box `Bike` với cả hai thuộc tính `truncated=true` và `occluded=true`. Chỉ chuyển sang `ignore_region` khi vật thể bị nhòe mờ hoặc che khuất trên 70% bề mặt.
