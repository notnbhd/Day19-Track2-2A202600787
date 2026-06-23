# Reflection — Lab 19

**Tên:** Nguyễn Bạch Hải Đăng
**Cohort:** A20-K2
**Path đã chạy:** lite

---

## Câu hỏi (≤ 200 chữ)

> Trên golden set 50 queries, mode nào thắng ở loại query nào (`exact` /
> `paraphrase` / `mixed`), và tại sao? Khi nào bạn **không** dùng hybrid
> (i.e. khi nào pure BM25 hoặc pure vector là lựa chọn đúng)?

- **exact**: BM25 & Hybrid thắng (96.7%). Do query chứa từ khoá verbatim khớp chính xác tài liệu; semantic bị lệch do phân bố vector.
- **paraphrase**: BM25 thắng (33.3%) do model `bge-small-en-v1.5` tối ưu cho tiếng Anh nên semantic biểu diễn tiếng Việt kém. Dùng `bge-m3` sẽ giúp semantic thắng.
- **mixed**: Hybrid thắng (100.0%) nhờ RRF kết hợp thế mạnh từ khoá của BM25 và ngữ nghĩa của Vector.

**Khi nào không dùng Hybrid:**
- **Pure BM25:** Khi cần khớp chính xác mã lỗi, ID, SKU, tên hàm/thư viện; hoặc khi bị giới hạn tài nguyên/độ trễ cực thấp (BM25 chạy sub-ms, không cần GPU/embedding).
- **Pure Vector:** Khi câu hỏi viết lại hoàn toàn, tìm kiếm đa ngôn ngữ, không có trùng lặp từ vựng, hoặc tìm kiếm đa phương thức (hình ảnh/âm thanh).

---

## Điều ngạc nhiên nhất khi làm lab này

Ngạc nhiên nhất là SQLite Feast online lookup có độ trễ cực thấp (< 1ms trên Linux), đồng thời thấy rõ sự hạn chế của model nhúng thuần Anh (`bge-small-en-v1.5`) khi xử lý truy vấn paraphrase tiếng Việt.

---

## Bonus challenge

- [ ] Đã làm bonus (xem `bonus/`)
- [ ] Pair work với: _không có_
