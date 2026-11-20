# Báo cáo cá nhân — Ngày 11
Họ tên: Nguyễn Huy Vượng               Mã học viên: 2A202303133  
Phiên bản CVAT (Help → About): CVAT 2.82.0 (Docker Local)  
Guideline: Road v1.0    Lần nộp (`revision` trong manifest): 1  
Thời điểm export (ngày giờ trên CVAT): 2026-11-20    Số lần nộp lại sau Rework: 0  

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
| front | 12 | 29 | 2 | 2 | 15 | 7 | 6 |
| front-extra (đã làm __ / 4) | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| fisheye | 8 | 12 | 2 | 4 | 8 | 1 | 1 |
| fisheye-extra (đã làm __ / 4) | 0 | 0 | 0 | 0 | 0 | 0 | 0 |

## 3. Bảng ca khó
| Ảnh | Nhãn | Phân vân giữa | Đã chọn | Lý do |
| --- | --- | --- | --- | --- |
| A01 | traffic_sign | information và other | information | Biển báo bảo trì đường bộ chỉ dẫn thông tin tuyến đường |
| A03 | lane | L1 và road_curb | lane (L1) | Sát con lươn có vạch sơn vàng liền rõ nét, gán L1 solid yellow |
| A03 | traffic_light | red và green | red cho đèn trái, green cho đèn phải | Cụm đèn bên phải có bóng xanh đang sáng |
| B05 | lane | L1/R1 và other | other | Theo guideline, camera bên hông (MVL/MVR) luôn gán position = other |

## 4. Phiếu QC 1 nhận được
Bạn kiểm lô của tôi:                Quyết định nhận được: Release  
| Mã lỗi | Số lỗi | Đồng ý? | Đã sửa? |
| --- | ---: | --- | --- |
| QC1-08 | 0 | Đồng ý | Không có lỗi nặng |

## 5. Kiểm file export
| File | Mở lại được? | Số shape ảnh 1 (job / file) | Số shape ảnh 2 (job / file) | Tag camera có trong XML? |
| --- | --- | --- | --- | --- |
| nguyenhuyvuong-front.zip | Có | Khớp | Khớp | Có (value="front") |
| nguyenhuyvuong-fisheye.zip | Có | Khớp | Khớp | Có (value="fisheye_*") |

## 6. Ảnh chụp màn hình
1. Tab Labels của project: [Đã kiểm tra cấu hình khớp road_v1_labels.json]
2. Một ảnh camera trước đã gán đủ (A01): vạch L1, R1, drivable, traffic_sign.
3. Một ảnh fisheye đã gán: polyline cong theo cung tròn.
4. Một đoạn XML có <polyline label="lane">.

## 7. Tự đánh giá
Lỗi bạn mắc nhiều nhất hôm nay (theo mã QC1-xx), và cách tránh ở Ngày 20: Dễ quên đổi thuộc tính mặc định (như area_type từ direct sang alternative hoặc position từ L1 sang R1/L2). Cách tránh: Luôn mở Details kiểm tra sau khi vẽ từng đối tượng.  
Nhãn của bạn đi vào model ở đâu? Chọn một lỗi đã sửa và nói nó làm model học sai thế nào: Nhãn lane đi vào mô hình phát hiện làn đường (Lane Detection / Row-anchor). Nếu gán sai position (nhầm L1 thành R1) hoặc vẽ ngược chiều từ xa về gần, mô hình sẽ học sai hệ quy chiếu xe, dẫn đến hệ thống giữ làn (LKA) điều khiển vô lăng lệch hướng, gây mất an toàn nghiêm trọng.

## 8. (Tùy chọn, buffer) Từ polyline đến đích row-anchor
| y | 720 | 680 | 640 | 600 | 560 |
| --- | ---: | ---: | ---: | ---: | ---: |
| x của chúng tôi |  |  |  |  |  |
| x của bạn kia |  |  |  |  |  |
