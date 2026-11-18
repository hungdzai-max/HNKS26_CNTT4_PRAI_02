# BÀI LÀM PHA 2 – HACKATHON 02

- **Mã đề:** 02
- **Họ tên:** vũ mạnh hùng 
- **Lớp:** CNTT4   
- **Link repository Pha2:**
- **Công cụ AI đã dùng (ChatGPT/Claude/Gemini):**

> Pha 2 (20 phút cuối). Mỗi mục: mở cuộc trò chuyện mới, gửi nguyên văn prompt đã viết trong bai_lam_pha1.md, dán câu trả lời và link chia sẻ vào đây. Xong, kéo thả file này vào repository Pha2.

## 4.2. Trích xuất tin nhắn đăng ký gói tập ra JSON

**KET QUA AI**

```text
[
  {
    "ma_goi": "PT10",
    "ngay_bat_dau": "2026-12-15",
    "nguoi_lon": 2,
    "hoc_sinh": 1,
    "ca_tap": "toi",
    "ghi_chu": null
  },
  {
    "ma_goi": "YOG1",
    "ngay_bat_dau": "2027-01-04",
    "nguoi_lon": 3,
    "hoc_sinh": 0,
    "ca_tap": null,
    "ghi_chu": "vừa mổ dây chằng gối"
  },
  {
    "ma_goi": "GYM1",
    "ngay_bat_dau": null,
    "nguoi_lon": 4,
    "hoc_sinh": 0,
    "ca_tap": "sang",
    "ghi_chu": "bị hen suyễn"
  }
]
```

**Link trò chuyện:** https://chatgpt.com/share/6afd0340-a014-83ec-9f05-7d1f0a9e06a3

## 4.3. Báo giá bằng Chain-of-Thought

**KET QUA AI**

```text
Bước 1: Tính tiền người lớn
- 6 người lớn
- Giá gói YOG1: 900.000 đồng/người
\[
6 \times 900.000 = 5.400.000
\]

Tiền người lớn: 5.400.000 đồng
Bước 2: Tính tiền học sinh
- 2 học sinh (14 tuổi và 16 tuổi)
- Học sinh tính 70% giá người lớn
\[
900.000 \times 70\% = 630.000
\]

\[
2 \times 630.000 = 1.260.000
\]

Tiền học sinh: 1.260.000 đồng
Bước 3: Tính tiền gói tập
\[
5.400.000 + 1.260.000 = 6.660.000
\]

Bé 8 tuổi được miễn phí khu vui chơi nên không tính tiền.

Tiền gói tập: 6.660.000 đồng
Bước 4: Giảm giá nhóm
Nhóm có 6 người lớn, đủ điều kiện giảm 5%.
\[
6.660.000 \times 5\% = 333.000
\]

\[
6.660.000 - 333.000 = 6.327.000
\]

Tiền gói tập sau giảm: 6.327.000 đồng
Bước 5: Phụ thu thuê tủ đồ riêng
Có 2 người thuê tủ đồ riêng, mỗi người 150.000 đồng.
\[
2 \times 150.000 = 300.000
\]

Phụ thu: 300.000 đồng
Bước 6: Tổng tiền
\[
6.327.000 + 300.000 = 6.627.000
\]

[RESULT: 6.627.000 đồng]
```

**Link trò chuyện:** https://chatgpt.com/share/6afd0396-2de4-83ec-a057-3b7b7c11036d

### b) Kiểm tra kết quả AI

kết quả đúng 

## 4.4. Dây chuyền xử lý khiếu nại – kết quả Trạm 1

**KET QUA AI**

```text
{
  "loai_su_co": "huy_lop",
  "so_khach": 2,
  "so_buoi_bi_huy": 3,
  "tom_tat": "2 khách bị huỷ 3 buổi Yoga ca tối không báo trước."
}
```

**Link trò chuyện:** https://chatgpt.com/share/6afd0458-97bc-83ec-824c-16c2b580c2f9

## 4.5. Prompt chấm bài theo Rubric

**KET QUA AI**

```text
(Dán câu trả lời của AI vào đây (bấm nút Copy dưới câu trả lời) – xoá dòng này)
```

**Link trò chuyện:**
