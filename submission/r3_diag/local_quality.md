# Đối chiếu chất lượng cục bộ — rectangle

Teaching reference, không phải gold set đã phê duyệt; không có điểm đạt tự động.
Nguồn: export r1_craft đã khóa SHA256 `f05682c1b107130d78d883d63402c5e77a72ab52d40399b3eac9605686ea927f`; slice `B3-mid`.
Ghép hình học greedy một-một theo IoU ≥ 0.50, rồi so class; H ≥ 40 px.
Box trái nằm chủ yếu trong ignore_region reference không tính. Polygon, polyline, track không được chấm.
Đây là phép tính offline của lab, không phải báo cáo hay kết quả tương đương CVAT Premium.

Frame được tính: adasind_128310.jpg, adasind_140160.jpg, adasind_230910.jpg. Frame thiếu trong export: không.
TP=13; FP=6; FN=7; số lần đối chiếu=22; mean IoU của TP=0.893.

| Chỉ số | Micro | Macro | Nhãn thấp nhất |
|---|---:|---:|---:|
| accuracy | 0.591 | 0.882 | 0.818 |
| precision | 0.684 | 0.531 | 0.000 |
| recall | 0.650 | 0.575 | 0.000 |
| jaccard | 0.500 | 0.412 | 0.000 |
| dice | 0.667 | 0.538 | 0.000 |

| Nhãn | TP | FP | FN | Accuracy | Precision | Recall | Jaccard | Dice |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| Bike | 1 | 1 | 1 | 0.909 | 0.500 | 0.500 | 0.333 | 0.500 |
| Car | 3 | 1 | 1 | 0.909 | 0.750 | 0.750 | 0.600 | 0.750 |
| Pedestrian | 5 | 1 | 3 | 0.818 | 0.833 | 0.625 | 0.556 | 0.714 |
| ThreeWheeler | 0 | 0 | 2 | 0.909 | 0.000 | 0.000 | 0.000 | 0.000 |
| Truck | 4 | 3 | 0 | 0.864 | 0.571 | 1.000 | 0.571 | 0.727 |

| Frame | TP | FP | FN | Accuracy | Precision | Recall |
|---|---:|---:|---:|---:|---:|---:|
| adasind_128310.jpg | 5 | 1 | 0 | 0.833 | 0.833 | 1.000 |
| adasind_140160.jpg | 1 | 3 | 2 | 0.250 | 0.250 | 0.333 |
| adasind_230910.jpg | 7 | 2 | 5 | 0.583 | 0.778 | 0.583 |

Confusion matrix: hàng = teaching reference; cột = export đã khóa.
`<missing>` là thiếu box; `<extra>` là box thừa. Xem `local_quality_confusion.csv`.

| Reference \ Export | Bike | Car | Pedestrian | ThreeWheeler | Truck | <missing> |
|---|---:|---:|---:|---:|---:|---:|
| Bike | 1 | 0 | 1 | 0 | 0 | 0 |
| Car | 0 | 3 | 0 | 0 | 1 | 0 |
| Pedestrian | 0 | 0 | 5 | 0 | 0 | 3 |
| ThreeWheeler | 0 | 1 | 0 | 0 | 1 | 0 |
| Truck | 0 | 0 | 0 | 0 | 4 | 0 |
| <extra> | 1 | 0 | 0 | 0 | 1 | 0 |

Chi tiết xung đột trong `local_quality_conflicts.csv`; dữ liệu máy đọc trong `local_quality.json`.
Mismatching label đóng góp một FP cho class vẽ và một FN cho class reference; attribute khác được báo riêng.
Micro accuracy đếm mỗi cặp ghép sai class là một lần đối chiếu; Jaccard đếm cả FP và FN.
Macro/worst bỏ nhãn không xuất hiện ở cả hai phía; chỉ số không có mẫu là N/A.
