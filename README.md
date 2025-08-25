# 🧑‍🤝‍🧑 Phân tích và phân loại tính cách (Personality Analysis)

## 📌 Giới thiệu
Dự án này tập trung vào việc **phân tích dữ liệu tính cách** của con người dựa trên bộ dữ liệu khảo sát tâm lý.  
Mục tiêu chính:
- Khám phá và trực quan hóa dữ liệu
- Tìm hiểu mối quan hệ giữa các đặc điểm tính cách
- Áp dụng các thuật toán học máy để phân loại nhóm tính cách
- Đánh giá hiệu quả các mô hình dự đoán

---

## 📂 Bộ dữ liệu
Bộ dữ liệu gồm nhiều biến liên quan đến đặc điểm cá nhân và hành vi, ví dụ:
- **Gender**: Giới tính  
- **Age**: Tuổi  
- **Openness**: Tính cởi mở  
- **Neuroticism**: Tính dễ bị căng thẳng  
- **Conscientiousness**: Tính tận tâm  
- **Agreeableness**: Tính dễ chịu  
- **Extraversion**: Tính hướng ngoại  
- **Personality Type**: Nhãn phân loại (`Extravert`, `Introvert`, …)

---

## 🛠️ Các bước xử lý
1. **Tiền xử lý dữ liệu**
   - Kiểm tra dữ liệu thiếu  
   - Chuẩn hóa giá trị số  
   - Mã hóa biến phân loại  

2. **Phân tích mô tả**
   - Thống kê cơ bản theo giới tính, tuổi  
   - Biểu đồ phân phối các đặc điểm tính cách  
   - Heatmap ma trận tương quan  

3. **Phân tích nâng cao**
   - PCA (Principal Component Analysis) để giảm chiều dữ liệu  
   - Trực quan hóa phân cụm tính cách  

4. **Xây dựng mô hình Machine Learning**
   - Decision Tree  
   - Random Forest  
   - Logistic Regression  
   - KNN (k-Nearest Neighbors)  
   - SVM (Support Vector Machine)  

5. **Đánh giá mô hình**
   - Accuracy, Precision, Recall, F1-score  
   - So sánh hiệu quả các thuật toán  

---

## 📈 Một số kết quả nổi bật
- Tương quan mạnh giữa **Extraversion** và **Agreeableness**.  
- Nhóm **Introvert** có điểm trung bình thấp hơn ở các đặc điểm hướng ngoại và cởi mở.  
- Mô hình **Random Forest** đạt độ chính xác cao nhất (≈ 85%).  
- PCA cho thấy dữ liệu có thể rút gọn thành **2–3 thành phần chính**.  

---

## 🚀 Công nghệ sử dụng
- **Ngôn ngữ**: Python  
- **Thư viện chính**:  
  - `pandas`, `numpy` (xử lý dữ liệu)  
  - `matplotlib`, `seaborn` (trực quan hóa)  
  - `scikit-learn` (thuật toán ML, PCA, đánh giá mô hình)

---

## 📊 Minh họa
- Biểu đồ phân phối Extraversion, Agreeableness  
- Heatmap tương quan giữa các đặc điểm tính cách  
- PCA Biplot  
- Confusion Matrix các mô hình  

---

## 📜 Kết luận
- Các đặc điểm tính cách có sự liên quan chặt chẽ và ảnh hưởng trực tiếp đến phân loại nhóm tính cách.  
- **Random Forest** cho kết quả tốt nhất trong phân loại.  
- PCA và trực quan hóa hỗ trợ rất nhiều trong việc hiểu cấu trúc dữ liệu.  

---

## 📁 Tài liệu
- `personality_synthetic_dataset.csv`: Dữ liệu gốc  
- `Personality-analysis.pdf`: Báo cáo phân tích chi tiết  
- `Personality-analysis.Rmd`: Notebook xử lý và huấn luyện mô hình

---

## 👨‍💻 Tác giả
Dự án được thực hiện bởi [Trần Đăng Khôi].  
Mục đích: Học tập và nghiên cứu về **Phân tích dữ liệu & Học máy trong tâm lý học**.
