# Báo cáo cá nhân — Ngày 11
Họ tên: Nguyễn Huy Vượng               Mã học viên: 2A202303133  
Phiên bản CVAT (Help → About): CVAT 2.82.0 (Docker Local)  
Guideline: Road v1.0    Lần nộp (`revision` trong manifest): 2  
Thời điểm export (ngày giờ trên CVAT): 2026-11-21    Số lần nộp lại sau Rework: 1  

## 1. Kiểm project
| Mục | Đúng như guideline Road v1.0? | Ghi chú |
| --- | --- | --- |
| 6 label, đúng kiểu | Có | Đủ 6 label: lane, road_curb, crosswalk, drivable, traffic_light, traffic_sign |
| Thuộc tính và giá trị | Có | Khớp hoàn toàn với configs/road_v1_labels.json |
| 4 tag ảnh | Có | camera, timeofday, weather, source đều có attribute select 'value' |
Cách kết thúc polyline trên bản CVAT này: Bấm phím N  
Cách đặt tag ảnh trên bản CVAT này: Chọn công cụ Tag ở thanh bên trái, chọn label rồi chỉnh giá trị trong Details  

## 2. Số lượng đã gán
| Task | Ảnh | lane | road_curb | crosswalk | drivable | traffic_light | traffic_sign |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| front | 12 | 36 | 7 | 4 | 33 | 24 | 15 |
| front-extra (đã làm 4 / 4) | 4 | 12 | 0 | 2 | 11 | 8 | 14 |
| fisheye | 8 | 5 | 3 | 7 | 9 | 0 | 1 |
| fisheye-extra (đã làm 4 / 4) | 4 | 2 | 0 | 4 | 1 | 0 | 0 |

## 3. Bảng ca khó
| Ảnh | Nhãn | Phân vân giữa | Đã chọn | Lý do |
| --- | --- | --- | --- | --- |
| A01 | traffic_sign | information và other | information | Biển báo bảo trì đường bộ chỉ dẫn thông tin tuyến đường |
| A03 | lane | L1 và road_curb | lane (L1) | Sát con lươn có vạch sơn vàng liền rõ nét, gán L1 solid yellow |
| A05 | lane | vẽ vạch hay không | không vẽ L1/R1 | Ảnh đường không có vạch sơn phân làn rõ ràng, được miễn QC1-02 theo CHECKPOINTS |
| B05 | lane | L1/R1 và other | other | Theo guideline, camera bên hông (MVL/MVR) luôn gán position = other |

## 4. Phiếu QC 1 nhận được
Bạn kiểm lô của tôi: Phan Lê Hoàng Phúc                Quyết định nhận được: Release (sau Rework/Buffer)  
| Mã lỗi | Số lỗi | Đồng ý? | Đã sửa? |
| --- | ---: | --- | --- |
| QC1-03 | 2 | Đồng ý | Đã chuẩn hóa position L1/R1, không trùng lặp position trên cùng một ảnh |
| QC1-04 | 1 | Đồng ý | Đã đảo lại chiều vẽ polyline từ dưới lên trên (gần ra xa) theo quy tắc 2 |
| QC1-11 | 2 | Đồng ý | Đã gán position = other cho camera bên hông (MVL, MVR) và gắn edge_zone = true cho vật thể mép ảnh |
| Bổ sung | 8 | Đồng ý | Đã gán hoàn chỉnh 100% hai task mở rộng front-extra (4 ảnh) và fisheye-extra (4 ảnh) |

## 5. Kiểm file export
| File | Mở lại được? | Số shape ảnh 1 (job / file) | Số shape ảnh 2 (job / file) | Tag camera có trong XML? |
| --- | --- | --- | --- | --- |
| nguyenhuyvuong-front.zip | Có | Khớp (16 ảnh) | Khớp (166 shapes) | Có (value="front") |
| nguyenhuyvuong-fisheye.zip | Có | Khớp (12 ảnh) | Khớp (32 shapes) | Có (value="fisheye_*") |

## 6. Ảnh chụp màn hình
1. Tab Labels của project: [Đã kiểm tra cấu hình khớp road_v1_labels.json]
2. Một ảnh camera trước đã gán đủ (A01): vạch L1, R1, drivable, traffic_sign.
3. Một ảnh fisheye đã gán: polyline cong theo cung tròn (B01, B09).
4. Một đoạn XML có <polyline label="lane">.

## 7. Tự đánh giá
Lỗi bạn mắc nhiều nhất hôm nay (theo mã QC1-xx), và cách tránh ở Ngày 20: Dễ quên đổi thuộc tính mặc định (như area_type từ direct sang alternative hoặc position từ L1 sang R1/L2, hoặc fisheye position thành other). Cách tránh: Luôn mở Details kiểm tra sau khi vẽ từng đối tượng và dùng script road_check lint trước khi xuất xưởng.  
Nhãn của bạn đi vào model ở đâu? Chọn một lỗi đã sửa và nói nó làm model học sai thế nào: Nhãn lane đi vào mô hình phát hiện làn đường (Lane Detection / Row-anchor). Nếu gán sai position (nhầm L1 thành R1) hoặc vẽ ngược chiều từ xa về gần, mô hình sẽ học sai hệ quy chiếu xe, dẫn đến hệ thống giữ làn (LKA) điều khiển vô lăng lệch hướng, gây mất an toàn nghiêm trọng.

## 8. (Tùy chọn, buffer) Từ polyline đến đích row-anchor
| y | 720 | 680 | 640 | 600 | 560 |
| --- | ---: | ---: | ---: | ---: | ---: |
| x của chúng tôi | 580 | 610 | 635 | 655 | 670 |
| x của bạn kia | 582 | 612 | 638 | 658 | 672 |

1. Năm số x đó chính là đích mà một model row-anchor học cho vạch này. Nếu bạn dừng polyline sớm 40 px, hàng nào đổi thành "không có làn"?  
Trả lời: Hàng y = 560 sẽ đổi thành "không có làn" (nằm ngoài phạm vi của polyline).
2. So với bạn được kiểm (cùng ảnh): ở hàng 720 và hàng 560, hai bạn lệch nhau bao nhiêu pixel? Lệch ở hàng nào ảnh hưởng LKA nhiều hơn (slide 25)?  
Trả lời: Hàng 720 lệch 2 px, hàng 560 lệch 2 px. Lệch ở hàng 720 (gần mũi xe) ảnh hưởng đến góc đánh lái tức thời của LKA nhiều hơn vì đây là điểm tựa điều khiển bám làn trực tiếp.
3. Nếu polyline vẽ từ xa về gần (ngược quy tắc 2), cách tính trên có đổi không? Script nào sẽ gặp khó?  
Trả lời: Cách tính tọa độ x tại từng hàng y vẫn có thể tìm được bằng phép cắt ngang hình học, tuy nhiên các script nội suy giả định mảng điểm tăng dần theo y từ dưới lên trên hoặc script gán vector hướng di chuyển (heading angle) sẽ bị đảo chiều hoàn toàn, dẫn đến lỗi thuật toán trích xuất làn.
