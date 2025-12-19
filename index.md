---
title: Duplication Text Detection System
---

# Duplication Text Detection System

Hệ thống phát hiện văn bản trùng lặp và tương tự, kết hợp các phương pháp hashing truyền thống với các mô hình embedding ngữ nghĩa hiện đại, nhằm xử lý hiệu quả các tập dữ liệu văn bản quy mô lớn.  
Mục tiêu của hệ thống là đạt được sự cân bằng giữa độ chính xác, chi phí bộ nhớ và thời gian thực thi trong các bài toán phát hiện trùng lặp thực tế.

## 1. Introduction

Dự án được thực hiện trong khuôn khổ học phần mở rộng **Cấu trúc dữ liệu và Giải thuật**, với mục tiêu nghiên cứu, triển khai và đánh giá các phương pháp phát hiện văn bản trùng lặp dựa trên hai hướng tiếp cận chính:

- Đặc trưng cú pháp (*syntax-based*)
- Đặc trưng ngữ nghĩa (*semantic-based*)

Trong thực tế, nhiều văn bản có thể không hoàn toàn giống nhau về mặt cú pháp nhưng lại tương đồng về mặt ý nghĩa. Do đó, việc chỉ sử dụng các phương pháp so khớp bề mặt thường không đủ để phát hiện đầy đủ các trường hợp trùng lặp.  
Dự án này tập trung so sánh ưu và nhược điểm của từng hướng tiếp cận, cũng như khả năng áp dụng của chúng trong các bài toán như lọc bình luận trùng lặp, phát hiện đạo văn và tối ưu hóa lưu trữ văn bản.

## 2. System Overview

Hệ thống được thiết kế theo mô hình pipeline, bao gồm các thành phần chính sau:

- **Biểu diễn văn bản ngữ nghĩa** bằng mô hình embedding `all-MiniLM-L6-v2`, cho phép ánh xạ văn bản sang không gian vector để phục vụ so sánh ngữ nghĩa.
- **Các phương pháp hashing** nhằm giảm chi phí lưu trữ và tăng tốc độ truy vấn:
  - *SimHash* cho phát hiện near-duplicate
  - *MinHash* cho so khớp cú pháp dựa trên độ tương đồng Jaccard
  - *Bloom Filter* cho kiểm tra trùng lặp nhanh với chi phí bộ nhớ thấp
- **Cấu trúc tìm kiếm và truy vấn tương đồng**:
  - *Locality Sensitive Hashing (LSH)* cho tìm kiếm xấp xỉ
  - *Faiss* cho tìm kiếm vector hiệu năng cao
- **Giao diện minh họa và thử nghiệm**, được triển khai bằng *Gradio*, giúp người dùng dễ dàng kiểm tra hệ thống mà không cần cấu hình môi trường cục bộ

## 3. Source Code

Toàn bộ mã nguồn triển khai hệ thống, bao gồm các module xử lý dữ liệu, hashing, embedding và đánh giá, được quản lý tại:

👉 [GitHub Repository](https://github.com/BTL-DSA-HK251/BTL-Extended-DSA)

Repository được tổ chức nhằm đảm bảo tính dễ đọc, dễ kiểm tra và khả năng tái hiện kết quả thực nghiệm.

## 4. Experimental Setup and Evaluation

Các thí nghiệm được thực hiện nhằm đánh giá hiệu quả của từng phương pháp theo các tiêu chí sau:

- **Precision, Recall và F1-score**, phản ánh độ chính xác của việc phát hiện trùng lặp
- **Mức độ sử dụng bộ nhớ**, đặc biệt quan trọng với các phương pháp hashing
- **Thời gian thực thi**, ảnh hưởng trực tiếp đến khả năng mở rộng hệ thống

Toàn bộ quá trình đánh giá được triển khai và có thể tái hiện thông qua các notebook Google Colab:

- **Đánh giá dựa trên đặc trưng cú pháp (*syntax-based*)**  
  [Google Colab – Syntax-based Evaluation](https://colab.research.google.com/drive/1o1-CAwPNq9E4pYC2eHI5YzXxxwapfhQt)

- **Đánh giá dựa trên đặc trưng ngữ nghĩa (*semantic-based*)**  
  [Google Colab – Semantic-based Evaluation](https://colab.research.google.com/drive/1eVFntUjP9f837L_oexBRiJNE2wyIAZc4)

- **Đánh giá mức độ sử dụng bộ nhớ**  
  [Google Colab – Memory Usage Analysis](https://colab.research.google.com/drive/1B_XhvkkWgPJnxAY2CHhRAEjYRb2wiIku)

- **So sánh thời gian thực thi giữa các phương pháp**  
  [Google Colab – Execution Time Comparison](https://colab.research.google.com/drive/1J-iLNpH-PLPtxKQLlAXqLvJbCexVNV32)

## 5. Report

Chi tiết kiến trúc hệ thống, cơ chế thuật toán, thiết kế thí nghiệm và phân tích kết quả thực nghiệm được trình bày trong báo cáo cuối kỳ:

👉 [Final Project Report (PDF)](https://drive.google.com/file/d/1zQ7Wyf5HfboOBgLL1bE9udIcNqWbwo4w/view)

## 6. Demonstration

Hệ thống được triển khai thử nghiệm thông qua một demo trực tuyến tại:

👉 [Live Demonstration](https://huggingface.co/spaces/DatNguyen-BK/demo_deploy)

Trang demo cho phép người dùng tải lên các tập tin văn bản (`.docx`, `.txt`, `.csv`), lựa chọn phương pháp phát hiện trùng lặp và quan sát kết quả nhóm cũng như kết quả lọc văn bản.

## 7. Notes on Reproducibility

- Các notebook Google Colab có thể được chạy lại bằng chức năng **Run all** để tái hiện toàn bộ quá trình thực nghiệm.
- Khuyến nghị sử dụng **GPU runtime** nhằm cải thiện đáng kể tốc độ thực thi, đặc biệt với các phương pháp embedding.
- Các cell trong notebook có thể được mở và kiểm tra chi tiết để hiểu rõ từng bước xử lý và đánh giá.

## 8. Challenges and Limitations

Trong quá trình thiết kế, triển khai và đánh giá hệ thống, nhóm đã gặp phải một số khó khăn và hạn chế đáng chú ý như sau.

### 8.1 Trade-off giữa độ chính xác và hiệu năng

Các phương pháp hashing như SimHash và MinHash có ưu điểm về tốc độ xử lý và chi phí bộ nhớ thấp. Tuy nhiên, khi ngưỡng tương đồng không được lựa chọn phù hợp, các phương pháp này có thể làm giảm độ chính xác, đặc biệt trong các trường hợp văn bản chỉ tương đồng về mặt ngữ nghĩa.

Ngược lại, các phương pháp dựa trên embedding cho kết quả chính xác hơn trong việc phát hiện văn bản tương đồng về ý nghĩa, nhưng đi kèm với chi phí tính toán cao hơn và yêu cầu nhiều tài nguyên hơn.

### 8.2 Lựa chọn và điều chỉnh tham số

Việc lựa chọn các tham số như:
- mức threshole để so sánh hiệu quả
- số lượng hash function trong MinHash,
- độ dài fingerprint trong SimHash,
- kích thước Bloom Filter và tỷ lệ false positive,
- số lượng bucket và hash function trong LSH,

có ảnh hưởng lớn đến kết quả cuối cùng. Quá trình điều chỉnh tham số đòi hỏi nhiều lần thử nghiệm và đánh đổi giữa độ chính xác, tốc độ và bộ nhớ.

### 8.3 Chi phí tính toán của embedding

Việc sinh embedding cho tập dữ liệu lớn tiêu tốn đáng kể thời gian và tài nguyên, đặc biệt khi không sử dụng GPU.  
Trong một số thí nghiệm, thời gian tạo embedding chiếm phần lớn tổng thời gian thực thi của hệ thống.

### 8.4 Hạn chế của dữ liệu và đánh giá

Do giới hạn về thời gian và tài nguyên, tập dữ liệu sử dụng trong các thí nghiệm chưa thể bao phủ đầy đủ mọi loại văn bản trong thực tế.  
Điều này có thể ảnh hưởng đến khả năng tổng quát hóa kết quả khi áp dụng hệ thống cho các tập dữ liệu có đặc điểm khác biệt.

### 8.5 Khả năng mở rộng hệ thống

Mặc dù hệ thống hoạt động hiệu quả với tập dữ liệu ở quy mô vừa, việc mở rộng lên quy mô rất lớn (hàng triệu văn bản) đặt ra các thách thức về quản lý bộ nhớ, thời gian xử lý và kiến trúc lưu trữ, đặc biệt với các phương pháp embedding và tìm kiếm vector.
