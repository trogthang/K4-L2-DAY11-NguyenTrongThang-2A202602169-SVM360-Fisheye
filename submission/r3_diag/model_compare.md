# L / R / M

L/R/M là thứ tự box in-scope theo XML của từng frame.

## adasind_128310.jpg
- L5+R2+M1: LRM (edge)
- L6+R5: LR_noM (mid)
- L7+R1+M2: LRM (center)
- L4+R4+M6: LRM (center)
- L1+R3+M3: LRM (mid)
- L2+M4: LM_noR (center)
## adasind_140160.jpg
- L5+R2+M4: LRM (mid)
- L1+M1: LM_noR (edge)
- L3+M2: LM_noR (edge)
- L4+M3: LM_noR (center)
- R1: R_only (edge)
- R3: R_only (center)
- M5: M_only (center)
- M6: M_only (mid)
## adasind_230910.jpg
- L7+R6+M6: LRM (edge)
- L5+R2+M4: LRM (mid)
- L1+R12+M10: LRM (mid)
- L6+R9+M5: LRM (center)
- L2+R1+M1: LRM (mid)
- L4+R3+M3: LRM (center)
- L8+R4+M7: LRM (center)
- L9+M8: LM_noR (mid)
- L10+M9: LM_noR (mid)
- R5: R_only (mid)
- R7: R_only (mid)
- R8: R_only (mid)
- R10: R_only (center)
- R11: R_only (center)

## Zone × cell
| zone | LRM | LR_noM | LM_noR | L_only | RM_noL | R_only | M_only |
|---|---|---|---|---|---|---|---|
| center | 5 | 0 | 2 | 0 | 0 | 3 | 1 |
| mid | 5 | 1 | 2 | 0 | 0 | 3 | 1 |
| edge | 2 | 0 | 2 | 0 | 0 | 1 | 0 |
