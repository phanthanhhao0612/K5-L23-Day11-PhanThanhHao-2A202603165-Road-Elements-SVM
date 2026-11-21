# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): NguyenDai        Người kiểm (học viên): Phan Thanh Hào  
Ngày: 2026-11-21                          Phiên bản guideline: Road v1.0  
File được kiểm (tên + `revision` trong manifest): `NguyenDai-front (1).zip`, `NguyenDai-fisheye (1).zip` (`revision: 1`)  
Số ảnh kiểm: 6 ảnh mẫu bắt buộc (`A01, A02, A03, A12, B01, B08`) (+ 0 ảnh thêm)   Số nhãn đã kiểm (shape + tag): 83 (59 shape + 24 tag)  

## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 6 | 0 | nặng |
| QC1-02 đủ L1, R1 | bỏ sót | 6 | 0 | nặng |
| QC1-03 position | sai thuộc tính / thừa | 14 | 0 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 14 | 0 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 14 | 1 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 14 | 0 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 26 | 0 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 12 | 0 | nặng / chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 19 | 0 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 7 | 0 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 10 | 1 | chính |
| QC1-12 file | lỗi file | 2 | 4 | nhẹ / nặng |

*(Ghi chú: 2 cảnh báo box đèn < 8 px ở `A03` là không bắt buộc nên không tính lỗi. Ảnh mẫu ghi **"không lỗi"**: `A01_bc5fadac-fa6dd225.jpg`, `B01_02688_FV.png`.)*

## Danh sách lỗi (mỗi lỗi một dòng)
| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| ---: | --- | --- | --- | --- | --- |
| 1 | QC1-05 | A12 | `lane` (`position=L1`) | chính | Có 2 polyline cùng `position = L1` |
| 2 | QC1-11 | B08 | `lane#4@(217,619)` | chính | Polyline trên fisheye chỉ có 3 điểm, nên thêm điểm bám theo cung |
| 3 | QC1-12 | A02 | `lane#1@(1153,720)` | nhẹ | Có 1 điểm lặp liền nhau (click đúp), cần xoá điểm thừa |
| 4 | QC1-12 | A03 | `drivable#2@(231,705)` | nhẹ | Có 1 điểm lặp liền nhau |
| 5 | QC1-12 | A03 | `lane#4@(160,708)` | nhẹ | Có 1 điểm lặp liền nhau |
| 6 | QC1-12 | A12 | `drivable#6@(478,399)` | nhẹ | Có 1 điểm lặp liền nhau |

## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| — | Không có ca chờ lead trong mẫu 6 ảnh kiểm | — |

## Quyết định
Lỗi nặng: 0   Lỗi chính: 2 / 83 nhãn = 2,41 %   Lỗi nhẹ: 4   Ca chờ lead: 0  
Quyết định (Release / Hold / Rework): **Release**  
Lý do (theo luật của phiếu): Mẫu 6 ảnh kiểm có **0 lỗi nặng**, tỉ lệ lỗi chính là **2,41 %** (≤ 5 %) và không có ca chờ lead, nên đạt điều kiện **Release** theo quy tắc Phiếu QC 1. *(Góp ý nhẹ: bạn có thể gộp/chỉnh lại `L1` ở `A12`, thêm điểm cong ở `B08`, và xóa các điểm click đúp để file sạch hơn).*

Loại lỗi: bỏ sót = thiếu nhãn phải có; thừa = gán cái không phải đối tượng; sai phạm vi = hình lệch, sai chiều, dừng sai chỗ, tràn vùng. Ba loại này theo cách chia lỗi gán nhãn của ISO/IEC 5259-4 (mục 8.4.2); "sai thuộc tính" và "lỗi file" là khóa học thêm. Cách xếp mức: [thang mức lỗi](../docs/qc_severity_road_v1.0.md).
