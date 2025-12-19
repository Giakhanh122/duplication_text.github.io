---
layout: minimal
title: Duplication Text Report
---

# Duplication Text Detection System

Hệ thống phát hiện văn bản trùng lặp và tương tự, kết hợp các phương pháp hashing truyền thống và embedding ngữ nghĩa hiện đại, nhằm xử lý hiệu quả tập dữ liệu văn bản quy mô lớn.

---

## 1. Introduction
Dự án được thực hiện trong khuôn khổ học phần mở rộng **Cấu trúc dữ liệu và Giải thuật**, với mục tiêu nghiên cứu và đánh giá các phương pháp phát hiện văn bản trùng lặp dựa trên:

- Đặc trưng cú pháp (syntax-based)
- Đặc trưng ngữ nghĩa (semantic-based)

Bài toán hướng tới các ứng dụng thực tế như lọc bình luận trùng lặp, phát hiện đạo văn và tối ưu lưu trữ văn bản.

---

## 2. System Overview
Hệ thống bao gồm các thành phần chính sau:

- Biểu diễn văn bản ngữ nghĩa bằng mô hình `all-MiniLM-L6-v2`
- Các phương pháp hashing:
  - SimHash
  - MinHash
  - Bloom Filter
- Cấu trúc tìm kiếm và truy vấn tương đồng:
  - Locality Sensitive Hashing (LSH)
  - Faiss
- Giao diện minh họa và thử nghiệm được triển khai bằng Gradio

---

## 3. Source Code
Repository chứa toàn bộ mã nguồn triển khai hệ thống:

👉 https://github.com/BTL-DSA-HK251/BTL-Extended-DSA

---

## 4. Experimental Setup and Evaluation
Các thí nghiệm được thực hiện nhằm đánh giá hiệu quả của từng phương pháp theo các tiêu chí:

- Precision, Recall, F1-score
- Mức độ sử dụng bộ nhớ
- Thời gian thực thi

Toàn bộ quá trình đánh giá được triển khai và tái hiện thông qua Google Colab:

- Đánh giá trên đặc trưng cú pháp (syntax-based):  
  https://colab.research.google.com/drive/1o1-CAwPNq9E4pYC2eHI5YzXxxwapfhQt

- Đánh giá trên đặc trưng ngữ nghĩa (semantic-based):  
  https://colab.research.google.com/drive/1eVFntUjP9f837L_oexBRiJNE2wyIAZc4

- Đánh giá mức độ sử dụng bộ nhớ:  
  https://colab.research.google.com/drive/1B_XhvkkWgPJnxAY2CHhRAEjYRb2wiIku

- So sánh thời gian thực thi giữa các phương pháp:  
  https://colab.research.google.com/drive/1J-iLNpH-PLPtxKQLlAXqLvJbCexVNV32

---

## 5. Report
Chi tiết kiến trúc hệ thống, cơ chế thuật toán và phân tích kết quả được trình bày trong báo cáo:

👉 https://drive.google.com/file/d/1zQ7Wyf5HfboOBgLL1bE9udIcNqWbwo4w/view

---

## 6. Demonstration
Hệ thống được triển khai thử nghiệm tại:

👉 https://huggingface.co/spaces/DatNguyen-BK/demo_deploy

Demo cho phép tải lên các tập tin văn bản (`.docx`, `.txt`, `.csv`) và lựa chọn phương pháp phát hiện trùng lặp để quan sát kết quả nhóm và lọc văn bản.

---

## 7. Notes on Reproducibility
- Các notebook Colab có thể được chạy lại bằng cách sử dụng chức năng **Run all**.
- Khuyến nghị sử dụng GPU để cải thiện tốc độ thực thi.
- Các cell có thể được mở và kiểm tra chi tiết từng bước xử lý.




<!-- ---
layout: minimal
title: Duplication Text Report
---

# 📄 Duplication Text
Hệ thống phát hiện văn bản trùng lặp sử dụng Hashing và Embedding hiện đại.  

---

<a name="gioi-thieu"></a>
## 📖 Giới thiệu
Dự án được xây dựng cho học phần mở rộng **Cấu trúc dữ liệu và Giải thuật**, nhằm phát hiện và loại bỏ các văn bản trùng lặp hoặc tương tự trong tập dữ liệu lớn (bài viết, bình luận,...).

---

<a name="mo-ta"></a>
## 🚀 Mô tả
- Trích xuất đặc trưng văn bản bằng mô hình `all-MiniLM-L6-v2`
- Áp dụng các kỹ thuật băm: **SimHash**, **MinHash**, **BloomFilter**
- Tìm kiếm tương đồng gần giống: **LSH**, **Faiss**
- Giao diện trực quan bằng **Gradio**

---
## Github : [Github](https://github.com/BTL-DSA-HK251/BTL-Extended-DSA)
---

## 📄 Report : 
* Chi tiết cách triển khai + cơ chế được trình bày trong [Report](https://drive.google.com/file/d/1zQ7Wyf5HfboOBgLL1bE9udIcNqWbwo4w/view?usp=sharing)

---

## 📝 Colab
1. Đánh giá precise/recall/F1 score về 3 phương pháp được sử dụng :
   - Trong phát hiện văn bản Cú pháp : [Colab](https://colab.research.google.com/drive/1o1-CAwPNq9E4pYC2eHI5YzXxxwapfhQt?usp=sharing)
   - Trong phát hiện văn bản Ngữ nghĩa : [Colab](https://colab.research.google.com/drive/1eVFntUjP9f837L_oexBRiJNE2wyIAZc4?usp=sharing)
4. Đánh giá mức độ sử dụng bộ nhớ  của 3 phương pháp : [Colab](https://colab.research.google.com/drive/1B_XhvkkWgPJnxAY2CHhRAEjYRb2wiIku?usp=sharing)
5. Đánh giá, so sánh tốc độ thực thi của 3 phương pháp được sử dụng : [Colab](https://colab.research.google.com/drive/1J-iLNpH-PLPtxKQLlAXqLvJbCexVNV32?usp=sharing)

---

## ⚙️ Demo 
1. Truy cập [demo](https://huggingface.co/spaces/DatNguyen-BK/demo_deploy)
2. Upload file `.docx`, `.txt`, hoặc `.csv`.
3. Chọn phương pháp: **SimHash (Semantic)**, **Bloom + Faiss (Semantic)** hoặc **MinHash (Syntax)**.
4. Submit và quan sát kết quả gộp nhóm văn bản và kết quả lọc văn bản.
5. Tải file kết quả đã lọc văn bản `result.docx`.

---

## 📌 Ghi chú
* Truy cập colab/demo trực tiếp để chạy code.
* Run all trên colab (Nên chạy bằng GPU để có tốc độ thực thi nhanh hơn)
* Thầy có thể mở lại các cell bất kỳ để kiểm tra chi tiết
 -->
