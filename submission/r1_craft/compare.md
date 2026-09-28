# So sánh L với R

Chỉ số L/R là thứ tự box cao ≥ H=40 trong từng frame, theo thứ tự XML; bắt đầu từ 1.
Box L trong ignore_region được báo IGNORE_SCOPE, không tính SPURIOUS.

## adasind_128310.jpg
- L3 edge IGNORE_SCOPE
- L2 center SPURIOUS
## adasind_140160.jpg
- L2 edge IGNORE_SCOPE
- L1+R1 edge WRONG_CLASS
- L3 edge SPURIOUS
- L4+R3 center WRONG_CLASS
## adasind_230910.jpg
- L3 edge IGNORE_SCOPE
- L7+R6 edge ATTRIBUTE
- L2+R1 mid ATTRIBUTE
- L9+R5 mid WRONG_CLASS
- L10+R7 mid WRONG_CLASS
- R8 mid MISSING
- R10 center MISSING
- R11 center MISSING

## Theo zone
| zone | n_ref | matched | missing | spurious |
|---|---|---|---|---|
| center | 8 | 5 | 3 | 2 |
| mid | 9 | 6 | 3 | 2 |
| edge | 3 | 2 | 1 | 2 |
