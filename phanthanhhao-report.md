# Báo cáo cá nhân — Ngày 11
Họ tên: Phan Thanh Hào              Mã học viên: 2A202603165  
Phiên bản CVAT (Help → About): v2.81.0 (local)  
Guideline: Road v1.0    Lần nộp (`revision` trong manifest): 2  
Thời điểm export (ngày giờ trên CVAT): 2026-11-21T02:07:43+00:00 (UTC)    Số lần nộp lại sau Rework: 1  

## 1. Kiểm project
| Mục | Đúng như guideline Road v1.0? | Ghi chú |
| --- | --- | --- |
| 6 label, đúng kiểu | Đúng | Nạp từ `configs/road_v1_labels.json` (`lane`, `road_curb`, `crosswalk`, `drivable`, `traffic_light`, `traffic_sign`) |
| Thuộc tính và giá trị | Đúng | Khớp hoàn toàn với `src/road_lab/taxonomy.py` |
| 4 tag ảnh | Đúng | `camera`, `timeofday`, `weather`, `source` (mỗi tag có select `value`) |
Cách kết thúc polyline trên bản CVAT này: Nhấn phím `N` (hoặc nút Done).  
Cách đặt tag ảnh trên bản CVAT này: Dùng công cụ Setup tag ở thanh trái rồi mở Details trong bảng Objects để chọn `value`.  

## 2. Số lượng đã gán
| Task | Ảnh | lane | road_curb | crosswalk | drivable | traffic_light | traffic_sign |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| front | 12 | 41 | 26 | 3 | 24 | 39 | 39 |
| front-extra (đã làm 4 / 4) | 4 | 13 | 6 | 3 | 9 | 9 | 15 |
| fisheye | 8 | 11 | 16 | 9 | 11 | 4 | 9 |
| fisheye-extra (đã làm 4 / 4) | 4 | 1 | 6 | 5 | 4 | 0 | 0 |

## 3. Bảng ca khó
| Ảnh | Nhãn | Phân vân giữa | Đã chọn | Lý do |
| --- | --- | --- | --- | --- |
| A05_b2576c8c-2de20b8a.jpg | `lane` | Có vẽ `L1`/`R1` hay không | Không vẽ | Ảnh không có vạch sơn rõ ràng hai bên làn, chỉ có bó vỉa (`road_curb`), không vẽ bịa theo guideline |
| B11_07282_RV.png | `lane` | Có gán vạch ô đỗ người khuyết tật là `lane` không | Không gán `lane` | Guideline mục 4 quy định rõ: vạch ô đỗ không gán `lane`, chỉ gán `drivable` phần đường lưu thông và `road_curb` |
| A08_c0deebc1-16cfa791.jpg | `traffic_sign` | Nhóm biển phụ "PASSENGER CARS ONLY" phía trên biển chỉ dẫn | `group = supplementary` | Tấm biển phụ đi kèm biển chính, vẽ box riêng và đặt `supplementary` theo guideline |

## 4. Phiếu QC 1 nhận được
Bạn kiểm lô của tôi: Nguyễn Đại (`NguyenDai`)  Quyết định nhận được: Rework (3 lỗi nặng, 4 lỗi chính = 5,33 %)  
| Mã lỗi | Số lỗi | Đồng ý? | Đã sửa? |
| --- | ---: | --- | --- |
| QC1-03 (`nặng`: `A01 lane#6` trùng L2; `A06 lane#1, #16` trên crosswalk) | 3 | Đồng ý | Đã xoá 3 shape `lane` thừa trên CVAT và export lại `revision 2` |
| QC1-06 (`chính`: `A01 lane#2` đặt nhầm `kind=double`) | 1 | Đồng ý | Đã đổi `kind = single` |
| QC1-08 (`chính`: `B02 traffic_light#7` box rộng bao đầu người) | 1 | Đồng ý | Đã thu gọn box sát vỏ đèn `[1082, 42, 1158, 162]` |
| QC1-11 (`chính`: `B06 crosswalk#2`, `B07 drivable#5` tràn thân xe) | 2 | Đồng ý | Đã chỉnh lại đỉnh polygon tránh thân xe mình |

## 5. Kiểm file export
| File | Mở lại được? | Số shape ảnh 1 (job / file) | Số shape ảnh 2 (job / file) | Tag camera có trong XML? |
| --- | --- | --- | --- | --- |
| `phanthanhhao-front.zip` | Có (`road_check lint` đọc hợp lệ) | A01: 11 / 11 | A02: 8 / 8 | Có (`camera=front`) |
| `phanthanhhao-fisheye.zip` | Có (`road_check lint` đọc hợp lệ) | B01: 5 / 5 | B02: 8 / 8 | Có (`camera=fisheye_front`) |

## 6. Ảnh chụp màn hình
1. Tab Labels của project `d11-road-phanthanhhao`:

   ![Tab Labels của project](screenshots/01-labels.jpg)

2. Một ảnh camera trước đã gán đủ (làn, vùng lái, đèn/biển — `A12_c0f978fa-9b4e623f.jpg`):

   ![Ảnh camera trước đã gán đủ](screenshots/02-front.jpg)

3. Một ảnh fisheye đã gán (`B04_05535_RV.png`):

   ![Ảnh fisheye đã gán](screenshots/03-fisheye.jpg)

4. Một đoạn XML có `<polyline label="lane">`:

   ![Đoạn XML polyline lane](screenshots/04-xml.png)

## 7. Tự đánh giá
Lỗi bạn mắc nhiều nhất hôm nay (theo mã QC1-xx), và cách tránh ở Ngày 20:  
Lỗi hay gặp nhất qua tự kiểm `road_check lint` là quên đổi giá trị mặc định của CVAT (như `position = L1` cho các vạch khác dẫn tới `QC1-05` trùng `position` hoặc `QC1-03` trên camera fisheye hai bên) và vẽ vạch bị ngược chiều từ xa về gần (`QC1-04`). Ở Ngày 20, luôn mở **Details** ngay sau khi vẽ xong từng shape và chạy `road_check lint` trước khi chốt job.

Nhãn của bạn đi vào model ở đâu? Chọn một lỗi đã sửa và nói nó làm model học sai thế nào:  
Nhãn `lane` và `drivable` là ground truth để huấn luyện model nhận diện làn đường (như row-anchor / lane detection) và vùng chạy được cho hệ thống giữ làn (LKA). Nếu mắc lỗi `QC1-03` (gán nhầm `position = L1` cho vạch bên phải `R1` hoặc trên camera hai bên), model sẽ học sai ranh giới trái/phải của làn xe đang đi, dẫn tới dự đoán lệch làn hoặc cảnh báo sai cho bộ điều khiển LKA.
