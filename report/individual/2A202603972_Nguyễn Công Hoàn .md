# Báo cáo cá nhân — Day 01: Lọc tin nhắn rác bằng ML, DL, Embedding và LLM

> Đổi tên file này thành `MSSV_HoTen.md` của bạn, ví dụ `2A20260000_NguyenVanAn.md`, rồi điền từng mục. Xoá các dòng hướng dẫn in nghiêng khi xong.

- **MSSV:** 2A202603972
- **Họ và tên:** Nguyễn Công Hoàn 
- **SEED** (in ở ô đầu notebook): 8977

## 1. Bằng chứng

| Tệp | Có? |
| --- | --- |
| [`day01_lab.ipynb`](day01_lab.ipynb) — notebook đã chạy, còn output | Có |
| [`lab1_report.json`](lab1_report.json) — do ô "Báo cáo cuối" sinh ra | Có |
| [`hand_calc.jpg`](hand_calc.jpg) — ảnh tính tay có các bước | Có |

## 2. Kết quả chính

                                 precision  recall  F1 (test)  F1 (SUB 40)  \
1. BoW + LogReg (tự code)            0.988   0.782      0.873        0.889   
2. BoW + MLP (deep learning)         0.947   0.891      0.918        1.000   
3a. Encoder (MiniLM) + kNN           0.838   0.970      0.899        0.952   
3b. Encoder (MiniLM) + LogReg        0.989   0.931      0.959        0.974   
3c. Encoder (MiniLM) + MLP head      0.969   0.921      0.944        0.974   
4a. LLM nhỏ zero-shot                0.800   1.000      0.889        0.889   
4b. LLM lớn zero-shot                0.952   1.000      0.976        0.976   
4c. LLM nhỏ few-shot                 0.909   1.000      0.952        0.952   

                                 train (s)  tin/s (cả lô)  p50 ms/tin  \
1. BoW + LogReg (tự code)            8.412       8204.701       0.059   
2. BoW + MLP (deep learning)        10.185      24225.123       0.301   
3a. Encoder (MiniLM) + kNN          98.352         37.045      66.262   
3b. Encoder (MiniLM) + LogReg       99.898         46.322      28.386   
3c. Encoder (MiniLM) + MLP head     99.321         46.194      28.389   
4a. LLM nhỏ zero-shot                0.000          1.207     345.141   
4b. LLM lớn zero-shot                0.000          1.254     288.850   
4c. LLM nhỏ few-shot                 0.000          0.633    2305.290   

                                 p95 ms/tin  USD / 1k tin  
1. BoW + LogReg (tự code)             0.117           0.0  
2. BoW + MLP (deep learning)          0.649           0.0  
3a. Encoder (MiniLM) + kNN          127.524           0.0  
3b. Encoder (MiniLM) + LogReg        40.256           0.0  
3c. Encoder (MiniLM) + MLP head      36.091           0.0  
4a. LLM nhỏ zero-shot              2435.319           0.0  
4b. LLM lớn zero-shot              2426.385           0.0  
4c. LLM nhỏ few-shot               2589.649           0.0  
• Hàng LLM chỉ đo trên SUB (40 tin) → so sánh chất lượng công bằng bằng cột 'F1 (SUB 40)'.
• SUB chỉ 40 tin: 1 tin sai đổi F1 vài điểm. Chênh < ~0.05 F1 coi như HOÀ — đừng xếp hạng theo số lẻ.
• Inference đo TỪ VĂN BẢN THÔ → NHÃN (gồm cả vectorize / encode). p50/p95 = gọi từng tin một, như một request thật.
• train (s) của 3a/3b/3c = thời gian encoder MiniLM encode tập train (+ train đầu LogReg / MLP); LLM = 0 vì không train. Số đo phụ thuộc CPU/GPU của Colab.


## 3. Dự đoán và thực tế

BoW + Logistic Regression và Embedding + Logistic Regression có thể nằm trên đường Pareto. Kết quả BoW + Logistic Regression và BoW + 
Encoder + Logistic Regression sẽ dự đoán đúng nhiều hơn BoW. kết quả bằng nhau , đều đúng 5/6 câu 
F1 của MLP có thể tương đương hoặc thấp hơn Logistic Regression. F1 của MLP cao hơn bên 

## 4. Phân tích 50 case khó

Model tụt nhiều nhất là BoW + MLP . model làm kém nhất ở case né từ khóa 0/6.
Case #29: “C0ngr4tulat10ns! Y0u h4ve w0n a £1000 g1ft c4rd. Cl4im n0w…” . chữ thay bằng số 
Case #31: “U have been s.e.l.e.c.t.e.d for a c.a.s.h r.e.w.a.r.d, c.a.l.l…” có dấu chấm giữa các chữ 

## 5. Thử thách cá nhân



## 6. Phương án cho sản phẩm thật



## 7. AI log và điều đã học

Hôm nay, tôi đã hỏi AI về cách xây dựng và đánh giá mô hình phân loại Spam/Ham bằng Logistic Regression, MLP và Embedding. Tôi đã tự kiểm tra, sửa lỗi trong code, điều chỉnh Learning Rate, phân tích Overfitting, so sánh hiệu quả các mô hình và xử lý lỗi kết nối API.
