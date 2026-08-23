# D09 - Wine Quality Red: Gom cụm bằng Machine Learning

Dự án thực hiện gom cụm bộ dữ liệu **Wine Quality Red** bằng hai thuật toán:

- **K-Means**: chia dữ liệu thành `k = 6` cụm, tương ứng với 6 mức nhãn `quality` trong dữ liệu.
- **DBSCAN**: gom cụm theo mật độ, tự động phát hiện cụm và đánh dấu các điểm lẻ là nhiễu (`-1`).

Notebook không đưa cột `quality` vào quá trình gom cụm. Cột này chỉ được dùng để đối chiếu kết quả và tính các chỉ số đánh giá.

## Mục tiêu

- Đọc dữ liệu rượu vang đỏ từ file Excel.
- Tách 11 đặc trưng hóa lý làm dữ liệu đầu vào.
- Chuẩn hóa dữ liệu bằng Z-score.
- Cài đặt và chạy K-Means, DBSCAN.
- Đánh giá kết quả bằng **ARI**, **NMI** và **Purity**.
- Chiếu dữ liệu về 2 chiều bằng PCA để trực quan hóa.
- Tạo báo cáo HTML gồm biểu đồ, bảng chỉ số, bảng chéo và nhận xét.

## Cấu trúc dự án

```text
D09_WineQuality_Red_MachineLearning/
├── README.md
├── main.ipynb
└── clustering_report.html
```

Trong đó:

- `main.ipynb`: notebook chính, gồm toàn bộ pipeline xử lý dữ liệu, gom cụm, đánh giá và tạo báo cáo.
- `clustering_report.html`: báo cáo trực quan được sinh sau khi chạy notebook.
- `README.md`: tài liệu mô tả dự án.

File dữ liệu Excel được sử dụng trong notebook có tên:

```text
D09 - winequality-red.xlsx
```

Notebook tìm file dữ liệu theo đường dẫn tương đối: trước tiên ở thư mục đang chạy, sau đó ở thư mục cha. Vì vậy notebook không còn phụ thuộc vào path cố định của một máy cụ thể.

## Dữ liệu

Bộ dữ liệu gồm các đặc trưng hóa lý của rượu vang đỏ. Các cột đặc trưng được dùng để gom cụm, còn cột cuối `quality` là nhãn thật để đánh giá.

Quy trình đọc dữ liệu:

1. Đọc file `.xlsx` bằng các thư viện chuẩn của Python.
2. Tự động chọn sheet có nhiều dòng dữ liệu nhất.
3. Lấy các cột trừ cột cuối làm `X`.
4. Lấy cột cuối làm nhãn `y`.
5. Loại bỏ các dòng thiếu giá trị.

## Thuật toán

### K-Means

K-Means chia dữ liệu thành số cụm cho trước. Trong dự án này:

- `k = 6`
- `random_state = 42`
- số vòng lặp tối đa: `300`

Giá trị `k = 6` được chọn vì cột `quality` có 6 mức: `3, 4, 5, 6, 7, 8`.

### DBSCAN

DBSCAN gom cụm dựa trên mật độ điểm, không cần biết trước số cụm.

Tham số hiện tại:

- `eps = 1.3`
- `min_samples = 5`

Những điểm không thuộc cụm mật độ nào được gán nhãn `-1`, tức là điểm nhiễu.

### PCA

Dữ liệu ban đầu có 11 đặc trưng nên khó quan sát trực tiếp. PCA được dùng để chiếu dữ liệu về 2 thành phần chính:

- `PC1`
- `PC2`

Hai thành phần này chỉ phục vụ trực quan hóa, không thay thế dữ liệu đầu vào của thuật toán gom cụm.

## Chỉ số đánh giá

Dự án sử dụng 3 chỉ số:

- **ARI**: đo mức độ trùng khớp giữa cụm dự đoán và nhãn thật, có điều chỉnh yếu tố ngẫu nhiên.
- **NMI**: đo lượng thông tin chung giữa nhãn thật và nhãn cụm.
- **Purity**: đo độ tinh khiết của cụm, cho biết mỗi cụm chủ yếu chứa một nhãn `quality` nào.

ARI và NMI càng gần `1` thì kết quả gom cụm càng gần với nhãn thật. Purity càng cao thì mỗi cụm càng tập trung vào một nhóm chất lượng rõ ràng.

## Kết quả hiện tại

Theo báo cáo `clustering_report.html` hiện có:

| Thuật toán | Số cụm | Điểm nhiễu | ARI | NMI | Purity |
|---|---:|---:|---:|---:|---:|
| K-Means | 6 | 0 | 0.0676 | 0.0975 | 0.5528 |
| DBSCAN | 10 | 563 | 0.0177 | 0.0245 | 0.4459 |

Nhận xét ngắn:

- K-Means cho kết quả tốt hơn DBSCAN với bộ tham số hiện tại.
- ARI và NMI đều còn thấp, cho thấy cấu trúc cụm từ 11 đặc trưng hóa lý chưa trùng khớp mạnh với nhãn `quality`.
- Điều này hợp lý với bài toán gom cụm, vì thuật toán không được học trực tiếp từ nhãn chất lượng.

## Cách chạy

Mở notebook:

```bash
jupyter notebook D09_WineQuality_Red_MachineLearning/main.ipynb
```

Sau đó chọn **Run All** để chạy toàn bộ pipeline.

Nếu dùng JupyterLab:

```bash
jupyter lab D09_WineQuality_Red_MachineLearning/main.ipynb
```

Sau khi chạy xong, notebook sẽ:

1. In thông tin dữ liệu và kết quả đánh giá.
2. Tạo hoặc cập nhật file `clustering_report.html`.
3. Sinh các biểu đồ PCA, bảng metric, bảng chéo và bảng mô tả cụm.

## Báo cáo trực quan

File `clustering_report.html` có thể mở trực tiếp bằng trình duyệt. Báo cáo gồm:

- Tổng quan số mẫu, số nhãn `quality`, tỷ lệ PCA.
- Biểu đồ phân tán theo nhãn thật.
- Biểu đồ phân tán theo cụm K-Means.
- Biểu đồ phân tán theo cụm DBSCAN.
- Biểu đồ so sánh ARI, NMI, Purity.
- Bảng chéo giữa `quality` và cụm dự đoán.
- Bảng mô tả từng cụm và nhãn chất lượng chiếm ưu thế.

## Yêu cầu môi trường

Notebook chủ yếu sử dụng thư viện chuẩn của Python:

- `collections`
- `html`
- `math`
- `pathlib`
- `random`
- `zipfile`
- `xml.etree.ElementTree`

Để mở và chạy notebook, cần có Jupyter Notebook hoặc JupyterLab.

## Hướng phát triển

- Thử nghiệm thêm các giá trị `eps` và `min_samples` cho DBSCAN.
- Chạy K-Means với nhiều cách khởi tạo tâm cụm và so sánh kết quả.
- Thêm các phương pháp giảm chiều khác để trực quan hóa.
- So sánh với các mô hình có giám sát như Logistic Regression, Random Forest hoặc SVM nếu mục tiêu là dự đoán `quality`.
