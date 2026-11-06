# Báo cáo cá nhân — Day 01: Lọc tin nhắn rác bằng ML, DL, Embedding và LLM

> Đổi tên file này thành `MSSV_HoTen.md` của bạn, ví dụ `2A20260000_NguyenVanAn.md`, rồi điền từng mục. Xoá các dòng hướng dẫn in nghiêng khi xong.

- **MSSV:** 2A202603972
- **Họ và tên:** Nguyen Cong Hoan
- **SEED** (in ở ô đầu notebook): 8977

## 1. Bằng chứng

| Tệp | Có? |
| 3  | 3   |
| [`day01_lab.ipynb`](day01_lab.ipynb) — notebook đã chạy, còn output | ☐ |
| [`lab1_report.json`](lab1_report.json) — do ô "Báo cáo cuối" sinh ra | ☐ |
| [`hand_calc.jpg`](hand_calc.jpg) — ảnh tính tay có các bước | ☐ |

## 2. Kết quả chính

                                 precision  recall  F1 (test)  F1 (SUB 40)  \
1. BoW + LogReg (tự code)            0.988   0.782      0.873        0.889   
2. BoW + MLP (deep learning)         0.947   0.891      0.918        1.000   
3a. Encoder (MiniLM) + kNN           0.838   0.970      0.899        0.952   
3b. Encoder (MiniLM) + LogReg        0.989   0.931      0.959        0.974   
3c. Encoder (MiniLM) + MLP head      0.969   0.921      0.944        0.974   

                                 train (s)  tin/s (cả lô)  p50 ms/tin  \
1. BoW + LogReg (tự code)           10.851       4762.736       0.057   
2. BoW + MLP (deep learning)        18.342       9038.612       0.340   
3a. Encoder (MiniLM) + kNN         104.288         31.563      75.821   
3b. Encoder (MiniLM) + LogReg      105.453         52.360      24.522   
3c. Encoder (MiniLM) + MLP head    105.241         52.338      25.373   

                                 p95 ms/tin  USD / 1k tin  
1. BoW + LogReg (tự code)             0.580           0.0  
2. BoW + MLP (deep learning)          5.290           0.0  
3a. Encoder (MiniLM) + kNN          115.175           0.0  
3b. Encoder (MiniLM) + LogReg        33.446           0.0  
3c. Encoder (MiniLM) + MLP head      33.884           0.0  
• Hàng LLM chỉ đo trên SUB (40 tin) → so sánh chất lượng công bằng bằng cột 'F1 (SUB 40)'.
• SUB chỉ 40 tin: 1 tin sai đổi F1 vài điểm. Chênh < ~0.05 F1 coi như HOÀ — đừng xếp hạng theo số lẻ.
• Inference đo TỪ VĂN BẢN THÔ → NHÃN (gồm cả vectorize / encode). p50/p95 = gọi từng tin một, như một request thật.
• train (s) của 3a/3b/3c = thời gian encoder MiniLM encode tập train (+ train đầu LogReg / MLP); LLM = 0 vì không train. Số đo phụ thuộc CPU/GPU của Colab.


## 3. Dự đoán và thực tế

*Chọn 3 dự đoán `predict(...)` lệch nhiều nhất so với kết quả. Mỗi cái: bạn đoán gì, ra gì, vì sao lệch.*

## 4. Phân tích 50 case khó

*Model nào tụt nhiều nhất, ở nhóm case nào? Nêu 2 case cụ thể và cơ chế khiến model sai.*

## 5. Thử thách cá nhân

*Đề theo SEED của bạn, cách làm, kết quả, giải thích.*

## 6. Phương án cho sản phẩm thật

*Với yêu cầu p95 < 50 ms/tin cho 10 triệu SMS/ngày: chọn phương án nào, dẫn số liệu nào, chấp nhận đánh đổi gì.*

## 7. AI log và điều đã học

Hôm nay, tôi đã hỏi AI về cách xây dựng và đánh giá mô hình phân loại Spam/Ham bằng Logistic Regression, MLP và Embedding. Tôi đã tự kiểm tra, sửa lỗi trong code, điều chỉnh Learning Rate, phân tích Overfitting, so sánh hiệu quả các mô hình và xử lý lỗi kết nối API. 
