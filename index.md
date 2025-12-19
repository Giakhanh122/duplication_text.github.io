---
title: Duplication Text Detection System
---

# Duplication Text Detection System

Hệ thống phát hiện văn bản trùng lặp và tương tự được xây dựng nhằm giải quyết bài toán so sánh và lọc văn bản trong tập dữ liệu lớn.  
Dự án kết hợp các phương pháp hashing truyền thống với các mô hình embedding ngữ nghĩa hiện đại, cho phép đánh đổi linh hoạt giữa độ chính xác, tốc độ xử lý và chi phí bộ nhớ.

---

## 1. Introduction

Trong bối cảnh dữ liệu văn bản ngày càng gia tăng nhanh chóng, bài toán phát hiện văn bản trùng lặp và tương tự đóng vai trò quan trọng trong nhiều ứng dụng thực tế như:
- Phát hiện đạo văn trong giáo dục
- Lọc nội dung trùng lặp trên mạng xã hội
- Tối ưu hóa lưu trữ và tìm kiếm văn bản
- Tiền xử lý dữ liệu cho các hệ thống phân tích ngôn ngữ tự nhiên

Dự án này được thực hiện trong khuôn khổ học phần mở rộng **Cấu trúc dữ liệu và Giải thuật**, với mục tiêu nghiên cứu, triển khai và đánh giá các phương pháp phát hiện trùng lặp văn bản dựa trên hai hướng tiếp cận chính:
- Phân tích đặc trưng cú pháp (*syntax-based*)
- Phân tích đặc trưng ngữ nghĩa (*semantic-based*)

Thông qua việc kết hợp nhiều kỹ thuật khác nhau, hệ thống cho phép so sánh toàn diện hiệu quả của từng phương pháp trong các điều kiện dữ liệu và tiêu chí đánh giá khác nhau.



## 2. Problem Definition

Bài toán đặt ra là:  
Cho một tập hợp các văn bản đầu vào, hệ thống cần xác định các cặp văn bản trùng lặp hoặc có mức độ tương đồng cao vượt quá một ngưỡng xác định trước.

Các thách thức chính của bài toán bao gồm:
- Quy mô dữ liệu lớn dẫn đến chi phí so sánh tăng cao
- Văn bản có thể khác nhau về mặt hình thức nhưng tương đồng về mặt ngữ nghĩa
- Cần cân bằng giữa độ chính xác, tốc độ và mức sử dụng bộ nhớ



## 3. System Overview

Hệ thống được thiết kế theo mô hình pipeline gồm các bước chính:

1. Tiền xử lý văn bản
2. Biểu diễn văn bản
3. Lập chỉ mục và tìm kiếm tương đồng
4. Đánh giá và trực quan hóa kết quả

### 3.1 Text Representation

Hai nhóm phương pháp biểu diễn văn bản được sử dụng:

- **Syntax-based**:
  - SimHash
  - MinHash
  - Bloom Filter

- **Semantic-based**:
  - Sentence Embedding sử dụng mô hình `all-MiniLM-L6-v2`

### 3.2 Similarity Search

Để tăng tốc quá trình truy vấn tương đồng, hệ thống sử dụng:
- **Locality Sensitive Hashing (LSH)** cho các phương pháp hashing
- **Faiss** cho tìm kiếm vector embedding trong không gian chiều cao

### 3.3 User Interface

Một giao diện thử nghiệm được triển khai bằng **Gradio**, cho phép:
- Tải lên các tập tin văn bản
- Lựa chọn phương pháp phát hiện trùng lặp
- Quan sát kết quả nhóm và lọc văn bản trực quan



## 4. Source Code

Toàn bộ mã nguồn của hệ thống được tổ chức và quản lý tại repository GitHub sau:

👉 [Github](https://github.com/BTL-DSA-HK251/BTL-Extended-DSA)

Repository bao gồm:
- Mã nguồn triển khai các thuật toán
- Notebook phục vụ thí nghiệm
- Tài liệu hướng dẫn chạy và tái hiện kết quả



## 5. Experimental Setup and Evaluation

Các thí nghiệm được thiết kế nhằm đánh giá và so sánh hiệu quả của từng phương pháp theo các tiêu chí sau:

- **Precision, Recall, F1-score**
- **Mức độ sử dụng bộ nhớ**
- **Thời gian thực thi**

Toàn bộ thí nghiệm được triển khai dưới dạng Google Colab notebook, đảm bảo khả năng tái hiện kết quả.

### 5.1 Syntax-based Evaluation
[Colab](https://colab.research.google.com/drive/1o1-CAwPNq9E4pYC2eHI5YzXxxwapfhQt)

### 5.2 Semantic-based Evaluation
[Colab](https://colab.research.google.com/drive/1eVFntUjP9f837L_oexBRiJNE2wyIAZc4)

### 5.3 Memory Usage Analysis
[Colab](https://colab.research.google.com/drive/1B_XhvkkWgPJnxAY2CHhRAEjYRb2wiIku)

### 5.4 Execution Time Comparison
[Colab](https://colab.research.google.com/drive/1J-iLNpH-PLPtxKQLlAXqLvJbCexVNV32)



## 6. Report

Báo cáo chi tiết trình bày:
- Kiến trúc tổng thể của hệ thống
- Phân tích cơ chế hoạt động của từng thuật toán
- Đánh giá và so sánh kết quả thực nghiệm

👉 [Report](https://drive.google.com/file/d/1zQ7Wyf5HfboOBgLL1bE9udIcNqWbwo4w/view)



## 7. Demonstration

Hệ thống được triển khai thử nghiệm tại:

👉 [Demo](https://huggingface.co/spaces/DatNguyen-BK/demo_deploy)

Trang demo cho phép người dùng tải lên các tập tin văn bản (`.docx`, `.txt`, `.csv`) và lựa chọn phương pháp phát hiện trùng lặp để quan sát kết quả xử lý.



## 8. Notes on Reproducibility

- Các notebook Colab có thể được chạy lại bằng chức năng **Run all**
- Khuyến nghị sử dụng GPU để cải thiện tốc độ thực thi
- Các cell có thể được mở và kiểm tra chi tiết từng bước xử lý



## 9. Conclusion

Trang GitHub Pages này cung cấp cái nhìn tổng quan về hệ thống phát hiện văn bản trùng lặp được xây dựng trong khuôn khổ học phần.  
Thông qua việc kết hợp các phương pháp hashing và embedding, dự án cho thấy sự đánh đổi rõ ràng giữa độ chính xác, hiệu năng và chi phí tài nguyên, đồng thời mở ra hướng mở rộng cho các nghiên cứu và ứng dụng thực tế trong tương lai.
