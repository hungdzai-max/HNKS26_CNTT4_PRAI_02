# BÀI LÀM PHA 1 – HACKATHON 02

- **Mã đề:** 02
- **Họ tên:** vũ mạnh hùng 
- **Lớp:** CNTT4 
- **Link repository Pha1:**

> Pha 1 (70 phút đầu, KHÔNG dùng AI). Viết xong, kéo thả file này vào repository Pha1 trước mốc giờ giám thị công bố.

## 4.1. Bảo vệ dữ liệu và chống ảo giác

### a) Ghi chú đã ẩn danh hoá

**GHI CHU DA AN DANH**

```text
Khách hàng [TEN_KHACH_HANG], số điện thoại [SO_DIEN_THOAI], số CCCD [CCCD], email [EMAIL], đăng ký gói Yoga 1 tháng (mã YOG1) bắt đầu ngày 05/12/2026 cho 1 người lớn và 1 học sinh 15 tuổi. Khách đã chuyển khoản đặt cọc 500.000 đồng. Khách yêu cầu tập ca sáng.

```

### b) Hai câu lệnh chống ảo giác

**CAU LENH**

```text
câu 1:AI chỉ trả lời dựa trên file đính kèm, và nêu AI phải trả lời thế nào nếu file không có thông tin

câu 2: AI ghi rõ câu trả lời lấy từ mục hoặc điều khoản nào trong file

```

## 4.2. Trích xuất tin nhắn đăng ký gói tập ra JSON

**PROMPT**

```text
[CONTEXT]: bạn là một chuyên gia trong việc trích xuất dữ liệu
[Request] Bạn hãy chuyển TN1, TN2, TN3 thành một mảng JSON gồm 6 trường : 
ma_goi,ngay_bat_dau,
nguoi_lon,hoc_sinh, ca_tap,ghi_chu

[Explantion] : Phải theo đúng bộ quy tắc chuẩn hóa như sau :
QUY TẮC CHUẨN HOÁ (5 quy tắc)
1. ma_goi lấy theo bảng mã gói tập.
2. ngay_bat_dau dạng YYYY-MM-DD; tin nhắn không ghi năm thì lấy năm 2026; không có ngày cụ thể thì null.
3. Khách không nhắc học sinh thì hoc_sinh là 0 và mọi khách là người lớn.
4. ca_tap chỉ nhận "sang", "toi" hoặc null.
5. ghi_chu chỉ ghi yêu cầu đặc biệt về sức khoẻ, chấn thương, đi lại; không có thì null.


Câu Trả lời không chào hỏi, không giải thích

Ví dụ mẫu tương tự như sau :
Tin nhắn mẫu 1:
Đăng ký giúp mình gói Yoga 1 tháng bắt đầu 03/11/2026, 1 người lớn với 1 bạn học sinh, tập ca sáng. Mình đang đau lưng nhẹ.
Kết quả đúng:
{"ma_goi": "YOG1", "ngay_bat_dau": "2026-11-03", "nguoi_lon": 1, "hoc_sinh": 1, "ca_tap": "sang", "ghi_chu": "đau lưng nhẹ"}



Tin nhắn mẫu 2:
Gói gym 1 tháng còn nhận không ạ, em tập buổi tối, khi nào bắt đầu cũng được.
Kết quả đúng:
{"ma_goi": "GYM1", "ngay_bat_dau": null, "nguoi_lon": 1, "hoc_sinh": 0, "ca_tap": "toi", "ghi_chu": null}




[Action] : Lấy dữ liệu tin nhắn khách hàng từ <tin_nhan> => chuẩn hóa dữ liệu => Trả về đúng json

[Tone] : ngắn gọn , chuyên nghiệp

[Extra] : Trả về dữ liệu JSON

<tin_nhan>
TN1: Cho mình đăng ký 10 buổi tập với huấn luyện viên, bắt đầu 15/12 nhé, 2 người lớn và 1 bạn học sinh lớp 9, tập buổi tối.

TN2: Đăng ký Yoga cho 3 người, bắt đầu 04/01/2027. Một người vừa mổ dây chằng gối.

TN3: Gói gym tháng 12 còn ưu đãi không ạ? Nhóm em 4 người lớn, một bạn bị hen suyễn, muốn tập ca sáng.


</tin_nhan>
<BANG_MA_GOI_TAP>
BẢNG MÃ GÓI TẬP
GYM1 – Gym tự do 1 tháng
YOG1 – Yoga 1 tháng
PT10 – 10 buổi tập cùng huấn luyện viên

</BANG_MA_GOI_TAP>
```

## 4.3. Báo giá bằng Chain-of-Thought

### a) Prompt

**PROMPT**

```text
Bạn là một kế toán cho một câu lạc bộ fitness . bây giờ bạn đọc trong thẻ <data> các mục bảng giá , quy tắc , yêu cầu báo giá và hãy tính tổng tiền cho yêu cầu báo giá của khách hàng với các dữ liệu . Yêu cầu hãy  suy luận từng bước theo thứ như sau : tự tiền người lớn → tiền học sinh → tiền gói tập → giảm giá nhóm → phụ thu → tổng tiền . Mỗi bước ghi phép tính; dòng cuối có dạng như sau : [RESULT: <tổng tiền> đồng].

<data>
BẢNG GIÁ GÓI TẬP (đồng/người lớn)
GYM1 – Gym tự do 1 tháng: 600.000
YOG1 – Yoga 1 tháng: 900.000
PT10 – 10 buổi tập cùng huấn luyện viên: 3.500.000


QUY TẮC TÍNH GIÁ
1. Học sinh (từ 12 đến 17 tuổi) tính 70% giá người lớn. Trẻ dưới 12 tuổi đi cùng gia đình được dùng khu vui chơi miễn phí.
2. Nhóm từ 5 người lớn trở lên được giảm 5% trên tiền gói tập (tiền người lớn + tiền học sinh).
3. Phụ thu thuê tủ đồ riêng: 150.000 đồng/người. Phụ thu không được giảm giá.
4. Tổng tiền = tiền gói tập sau giảm + phụ thu.


YÊU CẦU BÁO GIÁ
Nhóm công ty đăng ký gói YOG1 gồm 6 người lớn, 2 học sinh (14 tuổi và 16 tuổi) và 1 bé 8 tuổi đi cùng. Có 2 người lớn thuê tủ đồ riêng.
<data>
```

## 4.4. Dây chuyền xử lý khiếu nại (Prompt Chaining)

### a) Prompt Trạm 1

**PROMPT**

```text
Bạn là một chuyên gia phân tích dữ liệu , bạn có nhiệm vụ phân tích Email phản hồi của khách hàng nằm trong mục "EMAIL KHIẾU NẠI CỦA KHÁCH" và chuyển thành một đối tượng JSON đúng 4 trường theo quy định "loai_su_co" , "huy_lop" , "thiet_bi" ,"huan_luyen_vien" . Câu Trả lời của bạn không chào hỏi, không giải thích , phần "tom_tat" không quá 20 từ và chỉ trả về đung đối tượng JSON như ví dụ sau :
{"loai_su_co": một trong "huy_lop" | "thiet_bi" | "huan_luyen_vien" | "khac", "so_khach": số nguyên, "so_buoi_bi_huy": số nguyên hoặc null, "tom_tat": "không quá 20 từ"}



Dữ liệu bạn phân tích nằm trong <data_phan_tich>

<data_phan_tich>
EMAIL KHIẾU NẠI CỦA KHÁCH

Tôi và chồng (2 người lớn) đăng ký gói Yoga YOG1 từ 01/11/2026, tập ca tối. Trong tuần qua có 3 buổi lớp Yoga bị huỷ mà phòng tập không báo trước, chúng tôi đến nơi mới biết. Huấn luyện viên Lan rất tận tâm, tôi không có gì phàn nàn về huấn luyện viên. Tôi đề nghị phòng tập giải quyết thỏa đáng.


CHÍNH SÁCH ĐỀN BÙ CỦA FITZONE GYM

- huy_lop: lớp tập bị huỷ không báo trước: hoàn 200.000 đồng/khách cho mỗi buổi bị huỷ.
- thiet_bi: máy tập hỏng, không sử dụng được: tặng voucher 100.000 đồng/khách.
- huan_luyen_vien: khiếu nại về thái độ huấn luyện viên: tặng voucher 300.000 đồng/khách.
- khac: chuyển bộ phận Chăm sóc hội viên xem xét, chưa đề xuất mức đền bù.
- Tổng mức đền bù trên 1.000.000 đồng phải được Quản lý chi nhánh duyệt trước khi gửi khách.



</data_phan_tich>
```

### b) Hai điều cần kiểm tra ở JSON đầu ra của Trạm 1

1. loai_su_co thuộc 4 nhãn; so_khach, so_buoi_bi_huy khớp email; loại sự cố đúng nội dung email; tom_tat không quá 20 từ.


2.

### c) Câu lệnh viết tiếp

**CAU LENH**

```text
(Viết câu lệnh vào đây – xoá dòng này)
```

## 4.5. Prompt chấm bài theo Rubric

**PROMPT**

```text
(Viết prompt vào đây – xoá dòng này)
```

## 4.6. Hoàn thiện System Prompt

> Phần Vai trò và Chuẩn đầu ra đã cho sẵn. Viết tiếp phần Quy tắc ràng buộc và Xử lý ngoại lệ.

```text
[Vai trò]
Bạn là "Trợ lý FitZone", nhân viên tư vấn trên website của phòng tập FitZone Gym, giúp khách chọn và đăng ký một trong 3 gói tập: GYM1 (Gym tự do 1 tháng), YOG1 (Yoga 1 tháng), PT10 (10 buổi tập cùng huấn luyện viên).

[Quy tắc ràng buộc]
1. chỉ tư vấn 3 gói tập của công ty
2.không hứa giảm giá ngoài bảng giá 
3.không hỏi xin số CCCD, số thẻ ngân hàng 

[Chuẩn đầu ra]
Trả lời bằng tiếng Việt, lịch sự, tối đa 120 từ. Giá gói tập trình bày dạng gạch đầu dòng. Kết thúc bằng một câu hỏi về nhu cầu tiếp theo của khách.

[Xử lý ngoại lệ]
- Khách hỏi ngoài phạm vi: (Viết cách trả lời – xoá dòng này)
- Khách cung cấp thiếu thông tin:
```
