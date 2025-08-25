# 🧑‍🤝‍🧑 Phân tích tính cách (Personality Analysis)

## 📌 Giới thiệu
Dự án này tập trung vào việc **phân tích đặc điểm tính cách con người** dựa trên dữ liệu khảo sát tâm lý, và áp dụng các **phương pháp thống kê** cùng **mô hình học máy** để phân loại nhóm tính cách.  
Quy trình bao gồm: **tiền xử lý dữ liệu, phân tích khám phá (EDA), phân tích thành phần chính (PCA)** và xây dựng các mô hình trong **R**.

---

## 📂 Dữ liệu
Bộ dữ liệu gồm thông tin nhân khẩu học và các đặc điểm tâm lý:
- **Gender** – giới tính  
- **Age** – tuổi  
- **Openness, Neuroticism, Conscientiousness, Agreeableness, Extraversion** – 5 yếu tố tính cách (Big Five)  
- **Personality Type** – nhãn phân loại (ví dụ: Introvert, Extravert)

---

## 🛠️ Quy trình
1. **Tiền xử lý dữ liệu**
   - Kiểm tra và xử lý giá trị thiếu  
   - Mã hóa biến phân loại  
   - Chuẩn hóa dữ liệu số  

2. **Phân tích khám phá (EDA)**
   - Phân phối điểm số các đặc điểm tính cách  
   - Heatmap ma trận tương quan  
   - So sánh theo nhóm tính cách  

3. **Giảm chiều dữ liệu**
   - **PCA (Principal Component Analysis)** để rút gọn và trực quan hóa  

4. **Xây dựng mô hình**
   - Decision Tree  
   - Random Forest  
   - Logistic Regression  
   - k-Nearest Neighbors (KNN)  
   - Support Vector Machine (SVM)  

5. **Đánh giá mô hình**
   - Accuracy, Precision, Recall, F1-score  
   - Ma trận nhầm lẫn (Confusion Matrix)  

---

## 📈 Kết quả chính
- **Extraversion** và **Agreeableness** có tương quan mạnh nhất  
- Nhóm **Introvert** có điểm trung bình thấp hơn ở **Extraversion** và **Openness**  
- **Random Forest** cho kết quả tốt nhất (~85% accuracy)  
- PCA cho thấy dữ liệu có thể rút gọn còn **2–3 thành phần chính**  

---

## 🚀 Công nghệ sử dụng
- **Ngôn ngữ:** R  
- **Thư viện chính:**  
  - `dplyr`, `tidyr` – xử lý dữ liệu  
  - `ggplot2`, `corrplot` – trực quan hóa  
  - `psych`, `factoextra` – PCA, phân tích nhân tố  
  - `caret`, `randomForest`, `e1071`, `class` – mô hình học máy  

---

## 📊 Trực quan hóa
- Biểu đồ phân phối các đặc điểm tính cách  
- Heatmap tương quan  
- Biểu đồ PCA (biplot)  
- Ma trận nhầm lẫn của các mô hình  

---

## 📁 Cấu trúc repo
- `personality_synthetic_dataset.csv` – dữ liệu gốc  
- `Personality-analysis.Rmd` – code xử lý và mô hình  
- `Personality-analysis.pdf` – báo cáo chi tiết  

---

## 👨‍💻 Tác giả
Thực hiện bởi Trần Dăng Khôi  
Mục đích: Học tập và nghiên cứu trong lĩnh vực **Khoa học dữ liệu & Tâm lý học với R**.
