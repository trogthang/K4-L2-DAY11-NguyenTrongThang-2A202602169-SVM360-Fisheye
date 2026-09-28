# QA review · B3-mid

Mã khóa: F056-82C1

| frame | object_ref | rule_id | nhận xét |
|---|---|---|---|
| adasind_140160.jpg | L2 | R01 | Box Car ở vị trí (50,50,150,150) nằm ở vành đen ngoài vòng kính quang học, là box thừa sai vùng cần loại bỏ khi rework. |
| adasind_128310.jpg | L1 | R05 | Phương tiện Truck ở mép phải (703,877,878,1073) bị cắt một phần thân bởi biên ảnh, cần gán thuộc tính truncated=true. |
| adasind_230910.jpg | L1 | R03 | Đối tượng người lái kèm xe hai bánh ở (950,939,1079,1117) được gom chung thành một nhãn Bike duy nhất đúng quy định rider R03. |

Ghi finding r2_qa: cell=L_only, rule_id có giá trị, why để trống.
