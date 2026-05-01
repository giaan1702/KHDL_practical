# PCA Eigenfaces (KHDL_EIgentFace)

Notebook `PCA.ipynb` thực hiện bài toán **Eigenfaces bằng PCA**:

- Chuẩn hoá ảnh khuôn mặt → PCA để lấy **K eigenfaces**
- **Tái tạo** ảnh khuôn mặt của sinh viên từ không gian PCA
- **Tìm 3 khuôn mặt giống nhất** trong tập dữ liệu bằng khoảng cách Euclidean trong không gian PCA

## Yêu cầu đầu vào

Tạo các thư mục/đường dẫn đúng như cấu hình trong notebook:

- `face_dataset/`: chứa ảnh dataset (`.jpg`, `.png`, `.jpeg`)
- `myface/102230279.jpg`: ảnh khuôn mặt của bạn (đổi tên/đường dẫn nếu cần)

Các tham số chính (trong **Bước 0** của `PCA.ipynb`):

- `DATASET_PATH = "face_dataset"`
- `MY_FACE_PATH = "myface/102230279.jpg"`
- `H, W = 160, 120`
- `OUTPUT_EIGEN_DIR = "face_new"`
- `VAR_TARGET = 0.9` (chọn \(K\) theo % phương sai tích luỹ)
- `RECON_MSE_TARGET = None` (nếu đặt số, sẽ ưu tiên chọn \(K\) theo MSE tái tạo)

Notebook có tiền xử lý (tuỳ chọn): phát hiện mặt bằng Haar Cascade, fallback crop giữa ảnh, CLAHE, denoise (median/gaussian).

## Cài đặt môi trường

Chạy với Python 3.x và cài các thư viện:

```bash
pip install numpy matplotlib scikit-learn opencv-python
```

## Cách chạy

1. Mở `PCA.ipynb`
2. Kiểm tra lại cấu hình ở **Bước 0** (đường dẫn dataset, ảnh của bạn, `H, W`, các tuỳ chọn tiền xử lý)
3. Chạy **Run All** (hoặc chạy lần lượt từ trên xuống)

## Output (kết quả)

Sau khi chạy xong notebook sẽ sinh các file chính:

- **Yêu cầu 1**: thư mục `face_new/`
  - `face_new/face_new.png`: lưới ảnh chứa \(K\) eigenfaces
  - `face_new/eigenface_###.png`: từng eigenface riêng lẻ
- **Yêu cầu 2**: `myface.png`
  - So sánh ảnh gốc và ảnh tái tạo (Reconstructed, \(K\) đã chọn)
- **Yêu cầu 3**: `myface_and_otherface.png`
  - Ảnh của sinh viên + 3 ảnh gần nhất (kèm distance)

Ngoài ra notebook in ra:

- `Selected K = ...` theo `VAR_TARGET` hoặc `RECON_MSE_TARGET`
- Vector PCA của ảnh sinh viên (một vài phần tử đầu) và distance tới các ảnh match

## Ghi chú

- Nếu máy không có file Haar cascade để detect mặt, notebook sẽ tự chuyển sang **center crop** và vẫn chạy được.
- Nếu bạn muốn đổi ảnh của mình, chỉ cần cập nhật `MY_FACE_PATH` trong notebook.

