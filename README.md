# D09_WineQuality_Red_MachineLearning

## Giới thiệu

Project thực hiện **phân tích dữ liệu và áp dụng các thuật toán Machine Learning**
trên bộ dữ liệu **Wine Quality Red**.

Project bao gồm:
- Khảo sát và thống kê dữ liệu.
- Giảm số chiều và trực quan hóa dữ liệu bằng PCA.
- Huấn luyện và so sánh các mô hình phân lớp.
- Gom cụm dữ liệu bằng K-Means và DBSCAN.

---

# Tính Năng Cốt Lõi

- **Data Analysis:** Phân tích kích thước, kiểu dữ liệu, nhãn và thống kê dữ liệu.
- **PCA Visualization:** Giảm số chiều dữ liệu xuống 2D và trực quan hóa.
- **Classification:** Đánh giá KNN, Random Forest và SVM.
- **Hyperparameter Tuning:** Tìm tham số tốt nhất bằng `GridSearchCV`.
- **Model Evaluation:** Sử dụng 10-Fold Cross Validation và Macro F1-Score.
- **Clustering:** Gom cụm bằng K-Means và DBSCAN.
- **Result Visualization:** Trình bày kết quả bằng bảng và biểu đồ.

---

# Dataset

Sử dụng bộ dữ liệu **Wine Quality Red**, gồm:

| Thông tin | Giá trị |
|---|---:|
| Số mẫu | 1599 |
| Số thuộc tính | 11 |
| Cột nhãn | `quality` |
| Số cột tổng cộng | 12 |
| Giá trị nhãn | 3 – 8 |

### Các thuộc tính

```text
fixed acidity
volatile acidity
citric acid
residual sugar
chlorides
free sulfur dioxide
total sulfur dioxide
density
pH
sulphates
alcohol
```

Dữ liệu được xuất từ **Excel sang CSV** trước khi sử dụng trong project.

File dữ liệu:

```text
data/winequality-red.csv
```

---

# Công Nghệ Sử Dụng

- **Python 3.x**
- **Jupyter Notebook**
- **Pandas** – xử lý dữ liệu
- **NumPy** – tính toán
- **Matplotlib** – trực quan hóa
- **Scikit-learn** – Machine Learning
- **OpenPyXL** – xử lý Excel

### Machine Learning

```text
PCA
KNN
Random Forest
SVM
K-Means
DBSCAN
```

---

# Cấu Trúc Project

```text
D09_WineQuality/
│
├── data/
│   └── winequality-red.csv
│
├── notebooks/
│   └── D09_WineQuality.ipynb

├── README.md
└── .gitignore
```

---

# Yêu Cầu

Cần cài đặt:

- Python 3.x
- Git
- Jupyter Notebook hoặc VS Code

### 🔗 Link cài đặt

- Python: https://www.python.org/downloads/
- Git: https://git-scm.com/downloads
- VS Code: https://code.visualstudio.com/download
- Jupyter: https://jupyter.org/install

---

# Cài Đặt

## 1. Clone project

```bash
git clone https://github.com/GH2909/D09_WineQuality_Red_MachineLearning.git
cd D09_WineQuality
```

## 2. Tạo môi trường ảo

```bash
python -m venv .venv
```

## 3. Kích hoạt môi trường

### Windows

```powershell
.venv\Scripts\Activate.ps1
```

### macOS / Linux

```bash
source .venv/bin/activate
```

## 4. Cài đặt thư viện

```bash
python -m pip install -r requirements.txt
```

---

# ▶️ Cách Chạy

Khởi động Jupyter:

```bash
jupyter notebook
```

Mở:

```text
notebooks/D09_WineQuality.ipynb
```

Chọn Python Kernel của `.venv`, sau đó chạy Notebook theo thứ tự:

```text
STEP 1
   ↓
STEP 2
   ↓
STEP 3
   ↓
STEP 4
```

Hoặc chọn:

```text
Run → Run All Cells
```

---

# Nội Dung Các Step

## STEP 1 – Data Analysis

- Đọc dữ liệu từ CSV.
- Kiểm tra kích thước và số chiều.
- Kiểm tra kiểu dữ liệu.
- Thống kê số lượng các giá trị nhãn.
- Tính Min, Max và Mean của các thuộc tính số.

---

## STEP 2 – PCA & Visualization

- Lấy các thuộc tính liên tục.
- Chuẩn hóa dữ liệu bằng `StandardScaler`.
- Giảm số chiều bằng `PCA`.
- Đưa dữ liệu về không gian 2D.
- Biểu diễn các nhãn `quality` bằng màu sắc khác nhau.

```text
Features
   ↓
StandardScaler
   ↓
PCA
   ↓
2D Visualization
```

---

## STEP 3 – Classification

Sử dụng 3 mô hình:

```text
KNN
Random Forest
SVM
```

Tinh chỉnh tham số bằng:

```text
GridSearchCV
```

Đánh giá bằng:

```text
10-Fold Cross Validation
Macro F1-Score
```

Kết quả được trình bày bằng bảng và biểu đồ so sánh.

---

## STEP 4 – Clustering

Loại bỏ cột `quality` trước khi gom cụm.

Sử dụng:

```text
K-Means
DBSCAN
```

Sau khi gom cụm, sử dụng `quality` để đánh giá kết quả của hai thuật toán.

---

# Kết Quả

Project tạo ra:

```text
results/
│
├── figures/
│   ├── PCA visualization
│   ├── Model comparison
│   └── Clustering visualization
│
└── tables/
    ├── Data statistics
    ├── Classification results
    └── Clustering results
```

Notebook hoàn chỉnh:

```text
notebooks/D09_WineQuality.ipynb
```

Có thể xuất Notebook thành PDF để nộp:

```text
D09_WineQuality.pdf
```
