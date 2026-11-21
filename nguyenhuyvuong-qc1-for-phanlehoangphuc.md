# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): Phan Lê Hoàng Phúc            Người kiểm (học viên): Nguyễn Huy Vượng  
Ngày: 2026-11-21                                       Phiên bản guideline: Road v1.0  
File được kiểm (tên + `revision` trong manifest): phanlehoangphuc-front.zip, phanlehoangphuc-fisheye.zip (rev 1)  
Số ảnh kiểm: 6 (+ 0 ảnh thêm, ghi riêng)              Số nhãn đã kiểm (shape + tag): 76  

## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 6 | 0 | nặng |
| QC1-02 đủ L1, R1 | bỏ sót | 4 | 1 | nặng |
| QC1-03 position | sai thuộc tính / thừa | 14 | 0 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 14 | 0 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 14 | 1 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 14 | 1 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 10 | 0 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 8 | 0 | nặng / chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 4 | 0 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 4 | 0 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 10 | 0 | chính |
| QC1-12 file | lỗi file | 2 | 0 | nhẹ / nặng |

## Danh sách lỗi (mỗi lỗi một dòng)
| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-02 | A06 | lane | nặng | Thiếu vạch phân làn R1 bên phải xe trong khi vệt sơn trên đường nhìn thấy rõ |
| 2 | QC1-06 | A04 | lane (L1) | chính | Vạch vàng đôi ở tim đường bị vẽ thành 2 polyline riêng rẽ thay vì 1 polyline đi giữa mang kind=double |
| 3 | QC1-05 | A01 | lane (L2) | chính | Vạch L2 bị vẽ 2 polyline đè nhau/tách đoạn gây trùng lặp thuộc tính position |

## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| A05 | Ảnh đường đất không có vạch sơn phân làn L1/R1. Được miễn QC1-02 không? | Coach xác nhận được miễn QC1-02 theo CHECKPOINTS |

## Quyết định
Lỗi nặng: 1   Lỗi chính: 2 / 76 nhãn = 2.6 %   Lỗi nhẹ: 0   Ca chờ lead: 0  
Quyết định (Release / Hold / Rework): Rework  
Lý do (theo luật của phiếu): Có 1 lỗi nặng (ảnh A06 bỏ sót vạch R1 quan trọng có thể quan sát rõ), theo luật quyết định phải Rework.
