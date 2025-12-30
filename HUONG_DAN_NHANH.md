# Hướng Dẫn Nhanh CoastSat

**📖 [Tài liệu đầy đủ](README_vi.md)** | **🌐 [English](README.md)**

## Bắt đầu trong 5 phút

### Bước 1: Cài đặt nhanh

```bash
# Tạo môi trường
conda create -n coastsat
conda activate coastsat

# Cài đặt các gói
conda install -c conda-forge geopandas -y
conda install -c conda-forge earthengine-api scikit-image matplotlib astropy notebook -y
pip install pyqt5 imageio-ffmpeg
```

### Bước 2: Thiết lập Google Earth Engine

1. Đăng ký tại: https://signup.earthengine.google.com/
2. Cài đặt gcloud CLI: https://cloud.google.com/sdk/docs/install
3. Xác thực tài khoản sau khi cài đặt

### Bước 3: Chạy ví dụ

```bash
conda activate coastsat
jupyter notebook
```

Mở file `example_jupyter.ipynb` và chạy từng ô (Shift + Enter)

## Quy trình làm việc cơ bản

### 1. Tải hình ảnh

```python
import os
from coastsat import SDS_download

inputs = {
    'polygon': [[[kinh_do_1, vi_do_1],
                 [kinh_do_2, vi_do_2],
                 [kinh_do_3, vi_do_3],
                 [kinh_do_4, vi_do_4],
                 [kinh_do_1, vi_do_1]]],  # Đóng polygon
    'dates': ['2020-01-01', '2020-12-31'],
    'sat_list': ['L8', 'S2'],
    'sitename': 'TEN_BAI_BIEN',
    'filepath': os.path.join(os.getcwd(), 'data')
}

metadata = SDS_download.retrieve_images(inputs)
```

### 2. Phát hiện đường bờ

```python
from coastsat import SDS_shoreline, SDS_preprocess

settings = {
    'cloud_thresh': 0.5,
    'output_epsg': 32648,  # Thay bằng EPSG của khu vực bạn
    'check_detection': True
}

# Tạo đường bờ tham chiếu (khuyến nghị)
settings['reference_shoreline'] = SDS_preprocess.get_reference_sl_manual(
    metadata, settings
)
settings['max_dist_ref'] = 100

# Trích xuất đường bờ
output = SDS_shoreline.extract_shorelines(metadata, settings)
```

### 3. Phân tích

```python
from coastsat import SDS_transects

# Vẽ tuyến cắt
transects = SDS_transects.draw_transects(output, settings)

# Tính giao điểm
cross_distance = SDS_transects.compute_intersection_QA(
    output, transects, settings
)
```

## Mã EPSG phổ biến cho Việt Nam

- **VN-2000 Múi 3**: 3405 (kinh độ 104°45' - 107°45')
- **UTM Zone 48N**: 32648 (kinh độ 102° - 108°)
- **UTM Zone 49N**: 32649 (kinh độ 108° - 114°)

Tìm EPSG cho khu vực của bạn tại: http://spatialreference.org/

## Lỗi thường gặp

### Lỗi: "No images found"
- Kiểm tra polygon có nằm trong vùng bờ biển không
- Thử mở rộng khoảng thời gian
- Giảm `cloud_thresh` nếu khu vực nhiều mây

### Lỗi: "Authentication failed"
- Chạy lại: `gcloud auth login`
- Đảm bảo tài khoản đã được cấp quyền GEE

### Lỗi: Không phát hiện được đường bờ
- Giảm `min_beach_area` cho bãi biển nhỏ
- Thay đổi `sand_color` thành 'dark' hoặc 'bright'
- Tăng `max_dist_ref` nếu bờ biển thay đổi nhiều

## Mẹo sử dụng

1. **Polygon nhỏ hơn**: Bắt đầu với vùng nhỏ (<10 km²) để kiểm tra
2. **Kiểm tra thủ công**: Đặt `check_detection: True` lần đầu tiên
3. **Đường bờ tham chiếu**: Luôn sử dụng để cải thiện độ chính xác
4. **Lưu thường xuyên**: Kết quả được lưu tự động trong `data/SITENAME/`

## Đọc kết quả

Kết quả được lưu trong 2 file:

1. **SITENAME_output.pkl**: Đọc bằng Python
```python
import pickle
with open('data/SITENAME/SITENAME_output.pkl', 'rb') as f:
    output = pickle.load(f)
    
# Xem tọa độ đường bờ đầu tiên
print(output['shorelines'][0])
```

2. **SITENAME_output.geojson**: Mở bằng QGIS/ArcGIS

## Tài nguyên học thêm

- **Tài liệu đầy đủ**: [README_vi.md](README_vi.md)
- **Ví dụ nâng cao**: `example_jupyter.ipynb`
- **Ước lượng độ sâu**: https://s2shores.readthedocs.io/en/latest/tutorials/spatial_dft/
- **Hỗ trợ**: https://github.com/kvos/CoastSat/issues

## Tham khảo nhanh các hàm

| Chức năng | Hàm |
|-----------|-----|
| Tải hình ảnh | `SDS_download.retrieve_images()` |
| Tạo đường bờ tham chiếu | `SDS_preprocess.get_reference_sl_manual()` |
| Phát hiện đường bờ | `SDS_shoreline.extract_shorelines()` |
| Vẽ tuyến cắt | `SDS_transects.draw_transects()` |
| Tính giao điểm | `SDS_transects.compute_intersection_QA()` |
| Loại bỏ nhiễu | `SDS_transects.reject_outliers()` |
| Trung bình theo mùa | `SDS_transects.seasonal_averages()` |
| Tạo video | `SDS_tools.make_animation_mp4()` |

---

**Cần trợ giúp?** Mở issue tại: https://github.com/kvos/CoastSat/issues
