# Báo cáo Day 14 — Bùi Văn Thịnh — 2A202604040

> Sao chép file này thành `report/individual/<MSSV>_<HoTen>.md` (không dấu), ví dụ `2A20260000_NguyenVanAn.md`.

- Mã học viên dùng với `--student`: `2A202604040`
- `seed_tag` trong `frames_A.txt`: `82ac3100fd`

## 1. Dự đoán trước sweep (bước 5b)

Ghi **trước** khi chạy `scripts/pp_sweep.py`, rồi commit và push ngay (lịch sử commit là bằng chứng thời điểm viết). Không sửa phần này sau khi có kết quả.

- Tham số tôi nghĩ giảm công sửa nhiều nhất: `score_thr` (tăng nhẹ lên khoảng `0.3`–`0.4`, thay vì tăng quá cao hoặc chỉ tăng `min_points`).
- Vì sao (nhìn ảnh BEV tập A: box thừa nhiều hay box sót nhiều?): Quan sát 3 ảnh trong `d14_2A202604040/png_A/`, box thừa (false positive) xuất hiện rất nhiều (101 box dự đoán nhưng nhiều box giả trên bụi cây, hàng rào và box trùng sát thân xe, nhất là ở `s02f00` và `s01f58`). Tăng `score_thr` vừa phải sẽ lọc bớt box rác điểm thấp (`0.3`/box) mà không làm sót quá nhiều xe/người thật (`1.0`/box). Trong khi đó `min_points` khó lọc được bụi cây/hàng rào vì các cụm này vốn có nhiều điểm LiDAR.

## 2. Tập A: sửa tay và tune

| Cấu hình | Xóa | Thêm | Sửa | Chi phí |
|---|---:|---:|---:|---:|
| Gốc | 57 | 16 | 15 | 40.6 |
| `best_config.json` | | | | |

- Tham số đã đổi trong `best_config.json`: ...
- Kết quả leave-one-out (dán các dòng `scripts/pp_sweep.py` in ra): ...
- Cấu hình có ổn định trên từng frame không? Vì sao tôi vẫn chọn (hoặc không chọn) nó: ...

## 3. Trước/sau (bước 8)

![so sánh](../../d14_2A202604040/compare/<frame>.jpg)

- `scripts/pp_compare.py` báo giảm (hoặc tăng) ...% công sửa trên tập A.
- Dự đoán ở mục 1 đúng hay sai? Giải thích bằng số box xóa/thêm/sửa: ...

## 4. Tập B

Số đo từ `scripts/pp_prelabel.py --frames d14_2A202604040/frames_B.txt --config d14_2A202604040/best_config.json --gt d14_2A202604040/ref_B.json`:

| Xóa | Thêm | Sửa | Chi phí |
|---:|---:|---:|---:|
| | | | |

- Loại box tốn công sửa nhất ở tập B: ...

## 5. Giới hạn

- Nêu ít nhất 2 giới hạn (ví dụ: chỉ 3 frame tune; model KITTI không có Truck/Bus; chi phí là công thức, chưa phải thời gian sửa thật): ...

