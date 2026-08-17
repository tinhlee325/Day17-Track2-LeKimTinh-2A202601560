# Báo cáo LAB 17 — Data Pipeline Engineering

**Họ tên:** Lê Kim Tính  **MSSV:** 2A202601560  **Lớp:** E403  **Ngày:** 17/08/2026

---

## 0 · Kết quả `make verify`

<details>
<summary>Output ba lần chạy</summary>

```text
* Lần 1:
kimtinh@LAPTOPPC:~/labs/lab17$ make verify

  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  LAB 17 · make verify
  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  run 1/3 … 35.1s
  run 2/3 … 33.5s
  run 3/3 … 37.3s

  BẢNG                  ỔN ĐỊNH          SỐ HÀNG     KỲ VỌNG   GHI CHÚ
  ──────────────────────────────────────────────────────────────────────────
  gold_training_set     ✓ ok              12,480      12,480   ✓
  gold_feature_daily    ✓ ok               8,645       9,100   ✗ thiếu 455 hàng
  gold_doc_chunks       ✓ ok              31,200      31,200   ✓
  quarantine_tickets    ✓ ok                   0         312   ✗ thiếu 312 hàng

  CHECKSUM từng lượt
  ──────────────────────────────────────────────────────────────────────────
  gold_training_set     8622572a97    8622572a97    8622572a97   ✓
  gold_feature_daily    4eee63cd82    4eee63cd82    4eee63cd82   ✓
  gold_doc_chunks       92d8e50131    92d8e50131    92d8e50131   ✓
  quarantine_tickets    empty         empty         empty        ✓

  KIỂM TRA KHÁC
  ──────────────────────────────────────────────────────────────────────────
  dbt test                                    ✓ 9/9 pass
  silver_tickets.priority ∈ 1..4, không NULL  ✗ 6,606 hàng sai
  quarantine_tickets đúng số bản ghi lỗi      ✗ 0 / 312
  gold_training_set: 1 hàng / 1 ticket        ✓ không lặp
Traceback (most recent call last):
  File "/home/kimtinh/labs/lab17/tools/verify.py", line 287, in <module>
    sys.exit(main())
  File "/home/kimtinh/labs/lab17/tools/verify.py", line 231, in main
    d = dashboard_check() if BASELINE_FILE.exists() else None
  File "/home/kimtinh/labs/lab17/tools/verify.py", line 131, in dashboard_check
    m = measure(read_query())
  File "/home/kimtinh/labs/lab17/tools/explain.py", line 93, in measure
    rows = con.execute(sql).fetchall()
_duckdb.IOException: IO Error: No files found that match the pattern "data/gold_events/*.parquet"

LINE 18: from read_parquet('data/gold_events/*.parquet')
              ^
make: *** [Makefile:41: verify] Error 1

* LẦN 2:
kimtinh@LAPTOPPC:~/labs/lab17$ make verify

  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  LAB 17 · make verify
  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  run 1/3 … 36.6s
  run 2/3 … 33.1s
  run 3/3 … 34.8s

  BẢNG                  ỔN ĐỊNH          SỐ HÀNG     KỲ VỌNG   GHI CHÚ
  ──────────────────────────────────────────────────────────────────────────
  gold_training_set     ✓ ok              12,480      12,480   ✓
  gold_feature_daily    ✓ ok               9,100       9,100   ✓
  gold_doc_chunks       ✓ ok              31,200      31,200   ✓
  quarantine_tickets    ✓ ok                   0         312   ✗ thiếu 312 hàng

  CHECKSUM từng lượt
  ──────────────────────────────────────────────────────────────────────────
  gold_training_set     8622572a97    8622572a97    8622572a97   ✓
  gold_feature_daily    3db448685c    3db448685c    3db448685c   ✓
  gold_doc_chunks       92d8e50131    92d8e50131    92d8e50131   ✓
  quarantine_tickets    empty         empty         empty        ✓

  KIỂM TRA KHÁC
  ──────────────────────────────────────────────────────────────────────────
  dbt test                                    ✓ 9/9 pass
  silver_tickets.priority ∈ 1..4, không NULL  ✗ 6,606 hàng sai
  quarantine_tickets đúng số bản ghi lỗi      ✗ 0 / 312
  gold_training_set: 1 hàng / 1 ticket        ✓ không lặp
Traceback (most recent call last):
  File "/home/kimtinh/labs/lab17/tools/verify.py", line 287, in <module>
    sys.exit(main())
  File "/home/kimtinh/labs/lab17/tools/verify.py", line 231, in main
    d = dashboard_check() if BASELINE_FILE.exists() else None
  File "/home/kimtinh/labs/lab17/tools/verify.py", line 131, in dashboard_check
    m = measure(read_query())
  File "/home/kimtinh/labs/lab17/tools/explain.py", line 93, in measure
    rows = con.execute(sql).fetchall()
_duckdb.IOException: IO Error: No files found that match the pattern "data/gold_events/*.parquet"

LINE 18: from read_parquet('data/gold_events/*.parquet')
              ^
make: *** [Makefile:41: verify] Error 1

*LẦN 3:
kimtinh@LAPTOPPC:~/labs/lab17$ make verify

  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  LAB 17 · make verify
  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  run 1/3 … -48.2s
  run 2/3 … 39.9s
  run 3/3 … 33.4s

  BẢNG                  ỔN ĐỊNH          SỐ HÀNG     KỲ VỌNG   GHI CHÚ
  ──────────────────────────────────────────────────────────────────────────
  gold_training_set     ✓ ok              12,480      12,480   ✓
  gold_feature_daily    ✓ ok               9,100       9,100   ✓
  gold_doc_chunks       ✓ ok              31,200      31,200   ✓
  quarantine_tickets    ✓ ok                 312         312   ✓

  CHECKSUM từng lượt
  ──────────────────────────────────────────────────────────────────────────
  gold_training_set     8dd7c98653    8dd7c98653    8dd7c98653   ✓
  gold_feature_daily    3db448685c    3db448685c    3db448685c   ✓
  gold_doc_chunks       92d8e50131    92d8e50131    92d8e50131   ✓
  quarantine_tickets    ebb89036fb    ebb89036fb    ebb89036fb   ✓

  KIỂM TRA KHÁC
  ──────────────────────────────────────────────────────────────────────────
  dbt test                                    ✓ 11/11 pass
  silver_tickets.priority ∈ 1..4, không NULL  ✓ sạch
  quarantine_tickets đúng số bản ghi lỗi      ✓ 312 / 312
  gold_training_set: 1 hàng / 1 ticket        ✓ không lặp
  dashboard rows scanned                      ✗ 5,000,000 → 5,000,000 (1.0×, cần ≥ 10×)
    số file parquet                           ✗ 5,000 → 5,000
    kết quả truy vấn không đổi                ✓
  DAG: catchup / max_active_runs              ✓ False / 1

  TỔNG KẾT
  ──────────────────────────────────────────────────────────────────────────
  ✓  1 · gold_training_set idempotent & đúng số hàng
  ✓  2 · gold_feature_daily đủ hàng (dữ liệu về muộn)
  ✓  3 · contract + quarantine + dbt test
  ✓  4 · gold_doc_chunks vẫn ổn định (đối chứng)
  ──────────────────────────────────────────────────────────────────────────
  4/4 tiêu chí đạt
```

</details>

Tổng kết: **4 / 4 tiêu chí đạt**.

---

## 1 · Kích thước bảng training tăng sau mỗi lần chạy

|                             |                                                                                                                                                                                                                                                                                                                                                        |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Triệu chứng**     | Khi chạy lại pipeline hoặc Clear Task trong Airflow, số hàng của`gold_training_set` tiếp tục tăng và một `ticket_id` xuất hiện nhiều lần, dù `silver_tickets` chỉ giữ một hàng cho mỗi ticket.                                                                                                                              |
| **Nguyên nhân**     | Model incremental không khai báo`unique_key` và strategy nên dbt dùng append. Vì bảng có grain entity và nguồn CDC chứa cả `c` lẫn `u`, cùng một ticket có thể được ghi thêm ở nhiều ngày. `catchup=True` và không giới hạn concurrent run làm tăng khả năng kích hoạt lỗi, nhưng không phải root cause. |
| **Cách khắc phục** | Trong`gold_training_set.sql`, đặt `unique_key='ticket_id'` và `incremental_strategy='merge'`. Trong DAG, đặt `catchup=False` và `max_active_runs=1`. Giữ bộ lọc `run_date` để backfill không phải quét toàn bộ lịch sử.                                                                                                  |
| **Bằng chứng**      | Sau sửa:**12.480 hàng**, không ticket trùng; checksum ba lượt cùng bằng `8dd7c98653`. DAG được kiểm tra là `False / 1`.                                                                                                                                                                                                         |

---

## 2 · Bảng đặc trưng theo ngày thiếu hàng ở các ngày quá khứ

|                                     |                                                                                                                                                                                                                              |
| ----------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Triệu chứng**             | `gold_feature_daily` chỉ có 8.645 thay vì 9.100 hàng, thiếu 455 cặp `(event_date, customer_id)` ở các ngày cũ. Có 6.539/129.462 event, tương đương **5,05%**, đến muộn hơn một ngày.         |
| **P99 độ trễ đo được** | **2,725833 ngày**; độ trễ lớn nhất đo được là `2,9446875` ngày.                                                                                                                                          |
| **Lookback đã chọn**       | **3 ngày** — làm tròn P99 lên ngày nguyên để bao phủ gần như toàn bộ dữ liệu về muộn trong khi giới hạn lượng dữ liệu phải tính lại.                                                        |
| **Nguyên nhân**             | Điều kiện cũ chỉ lấy`event_date > max(event_date)` của bảng đích. Event xảy ra ở ngày cũ nhưng đến kho sau vài ngày không còn thỏa điều kiện và bị bỏ qua vĩnh viễn.                         |
| **Cách khắc phục**         | Mở cửa sổ lookback ba ngày và dùng`delete+insert` với composite key `['event_date', 'customer_id']`, đúng grain của bảng. Các aggregate trong cửa sổ được tính lại và thay thế thay vì cộng dồn. |
| **Bằng chứng**              | Trước:**8.645 hàng**; sau: **9.100 hàng**. Checksum ba lượt cùng bằng `3db448685c`.                                                                                                                    |

P99 đại diện tốt hơn cho hành vi thông thường và tránh để một ngoại lệ cực đoan làm cửa sổ xử lý tăng vĩnh viễn. Dùng `max` bao phủ mọi bản ghi đã quan sát nhưng dễ làm chi phí compute tăng mạnh; mỗi ngày lookback bổ sung đều khiến pipeline phải quét, aggregate và ghi lại thêm dữ liệu ở mọi lần chạy. Với dữ liệu đo được, ba ngày vừa bao phủ P99 vừa đủ chứa giá trị lớn nhất hiện tại.

---

## 3 · Kiểu dữ liệu cột priority thay đổi giữa chu kỳ

|                                                                         |                                                                                                                                                                                                                                                                                                    |
| ----------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Triệu chứng**                                                 | Từ 10/08, backend đổi`priority` từ số sang nhãn chữ. Pipeline không dừng nhưng `try_cast` tạo nhiều `NULL`; đồng thời các số ngoài miền như `0`, `5`, `-1` vẫn được chấp nhận. Ban đầu Silver có 6.606 hàng priority sai và quarantine rỗng.           |
| **Nguyên nhân**                                                 | Macro chỉ dùng`try_cast`, contract đang tắt và chưa có test miền giá trị. Logic này nhầm schema drift hợp lệ với dữ liệu hỏng, đồng thời chỉ kiểm tra kiểu mà không kiểm tra miền `1..4`.                                                                          |
| **Ba nhóm giá trị `priority` và cách xử lý từng nhóm** | (1)`'1'..'4'`: giữ và cast sang integer; (2) `urgent/high/medium/low`: ánh xạ lần lượt thành `1/2/3/4`; (3) `P1`, `P2`, `unknown`, `0`, `5`, `-1`, rỗng và `NULL`: trả `NULL` để định tuyến sang quarantine.                                                 |
| **Cách khắc phục**                                             | Chuẩn hóa bằng macro`CASE`; lọc bản ghi lỗi **trước** `row_number()` để ticket giữ trạng thái hợp lệ gần nhất; đưa đúng các bản ghi không chuẩn hóa được vào `quarantine_tickets`; bật contract và thêm `not_null`, `accepted_values: [1,2,3,4]`. |
| **Bằng chứng**                                                  | `quarantine_tickets` = **312 hàng**; `dbt test` **11/11 pass**; `silver_tickets.priority` sạch, không NULL và luôn thuộc `1..4`.                                                                                                                                         |

Bronze nên giữ nguyên payload để bảo toàn khả năng audit và replay; chuẩn hóa và định tuyến lỗi thuộc Silver, nơi data contract được áp dụng. Không nên để 312 bản ghi lỗi chặn hơn 129 nghìn event và 31.200 document chunk hợp lệ. Pipeline tiếp tục phục vụ downstream, còn quarantine trở thành hàng đợi có quan sát để đội vận hành xử lý riêng.

---

## 4 · *(mở rộng, không bắt buộc)* Bài trong EXTRA.md

|                             |                                                                                                                            |
| --------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| **Bài đã làm**    | Không làm.                                                                                                               |
| **Nguyên nhân**     | Phần dashboard chỉ được chạy để xác nhận baseline; chưa thực hiện compact/partition hoặc sửa consumer.      |
| **Cách khắc phục** | Không áp dụng.                                                                                                          |
| **Bằng chứng**      | Dashboard giữ nguyên result nhưng vẫn scan 5.000.000 hàng qua 5.000 file (1,0×), đúng trạng thái chưa tối ưu. |

---

## 5 · Tổng kết

| Nhiệm vụ | Khi tiếp nhận một hệ thống chưa quen, tôi sẽ kiểm tra điều này trước tiên                                                           |
| ---------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1          | Xác định grain, natural key và materialization strategy; chạy lặp để kiểm tra idempotency trước khi tin vào kết quả.                 |
| 2          | So sánh event time với ingestion time, đo percentile độ trễ và kiểm tra incremental watermark có bỏ sót dữ liệu về muộn hay không. |
| 3          | Đối chiếu raw value với contract, tách schema drift hợp lệ khỏi dữ liệu hỏng và kiểm tra thứ tự normalize–filter–deduplicate.     |
