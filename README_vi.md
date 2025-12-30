# CoastSat - Hướng dẫn Tiếng Việt

[![Last Commit](https://img.shields.io/github/last-commit/kvos/CoastSat)](
https://github.com/kvos/CoastSat/commits/)
[![GitHub release](https://img.shields.io/github/release/kvos/CoastSat)](https://GitHub.com/kvos/CoastSat/releases/)
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.2779293.svg)](https://doi.org/10.5281/zenodo.2779293)
[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)

## Giới thiệu

CoastSat là một bộ công cụ phần mềm mã nguồn mở được viết bằng Python, cho phép người dùng thu thập chuỗi dữ liệu thời gian về vị trí đường bờ biển tại bất kỳ bờ biển nào trên thế giới từ 39 năm (và đang tăng) hình ảnh vệ tinh công khai.

![Alt text](https://github.com/kvos/CoastSat/blob/master/doc/example.gif)

## Mô tả Thư viện

### Tổng quan
CoastSat là một công cụ mạnh mẽ cho phép các nhà khoa học và kỹ sư ven biển:
- Tự động trích xuất đường bờ biển từ hình ảnh vệ tinh
- Phân tích sự thay đổi của bờ biển theo thời gian
- Nghiên cứu tác động của biến đổi khí hậu và các hiện tượng tự nhiên đến bờ biển

Thư viện sử dụng công nghệ viễn thám vệ tinh để cung cấp dữ liệu đường bờ dài hạn với chi phí thấp, có khả năng giải quyết các thang thời gian quan trọng đối với các nhà khoa học và kỹ sư ven biển tại các địa điểm không có đo đạc thực địa.

### Các tính năng chính

1. **Truy xuất hình ảnh vệ tinh tự động**
   - Tích hợp với Google Earth Engine để tải hình ảnh từ Landsat 5, 7, 8, 9 và Sentinel-2
   - Tiền xử lý tiên tiến: chiếu lại các băng tần, tăng độ phân giải, lọc mây nâng cao
   - Hỗ trợ vùng quan tâm tùy chỉnh và khoảng thời gian linh hoạt

2. **Phát hiện đường bờ biển tự động**
   - Thuật toán phát hiện độ phân giải sub-pixel
   - Phân loại hình ảnh thành 4 lớp: cát, nước, sóng vỡ, và các đặc điểm đất liền khác
   - Tối ưu hóa đặc biệt cho bờ biển cát
   - Tùy chọn kiểm soát chất lượng thủ công hoặc tự động

3. **Phân tích chuỗi thời gian**
   - Tính toán giao điểm giữa đường bờ 2D và các tuyến vuông góc với bờ
   - Hiệu chỉnh triều dựa trên mực nước và độ dốc bãi biển
   - Xử lý hậu kỳ: loại bỏ nhiễu, tính trung bình theo mùa
   - Phân tích xu hướng dài hạn

4. **Công cụ trực quan hóa**
   - Tạo hoạt ảnh MP4 từ chuỗi hình ảnh vệ tinh
   - Xuất dữ liệu sang định dạng GeoJSON cho GIS
   - Đồ họa tương tác để kiểm tra và điều chỉnh

### Ứng dụng

CoastSat được sử dụng rộng rãi trong:
- **Nghiên cứu khoa học**: Nghiên cứu sự biến đổi bờ biển do biến đổi khí hậu, El Niño/La Niña
- **Quản lý ven biển**: Theo dõi xói mòn và bồi tụ bờ biển
- **Quy hoạch đô thị**: Đánh giá rủi ro và lập kế hoạch phát triển vùng ven biển
- **Giáo dục**: Công cụ học tập về viễn thám và địa lý ven biển

### Tham khảo Nâng cao

Để tìm hiểu về ước lượng độ sâu ven biển (coastal bathymetry) thông qua phân tích Biến đổi Fourier Không gian (Spatial DFT), tham khảo:
- **Tài liệu S2Shores**: https://s2shores.readthedocs.io/en/latest/tutorials/spatial_dft/spatial_dft.html#coastal-bathymetry-estimation-via-spatial-dft

Phương pháp này cho phép ước lượng độ sâu vùng ven biển từ hình ảnh vệ tinh bằng cách phân tích các mẫu sóng trong không gian.

## Mục lục

- [Cài đặt](#cài-đặt)
- [Hướng dẫn Sử dụng](#hướng-dẫn-sử-dụng)
  - [Truy xuất hình ảnh vệ tinh](#truy-xuất-hình-ảnh-vệ-tinh)
  - [Phát hiện đường bờ](#phát hiện-đường-bờ)
  - [Phân tích chuỗi thời gian](#phân-tích-chuỗi-thời-gian)
  - [Hiệu chỉnh triều](#hiệu-chỉnh-triều)
  - [Xử lý hậu kỳ](#xử-lý-hậu-kỳ)
- [Ví dụ](#ví-dụ)
- [Đóng góp](#đóng-góp)
- [Tài liệu tham khảo](#tài-liệu-tham-khảo)

## Cài đặt

### Bước 1: Tạo môi trường với Anaconda

Để chạy CoastSat, bạn cần cài đặt các gói Python cần thiết trong một môi trường riêng. Chúng ta sẽ sử dụng **Anaconda**, có thể tải miễn phí tại [đây](https://www.anaconda.com/download/).

**Lưu ý**: Nếu bạn là người dùng nâng cao và đã cài đặt **Mamba**, hãy sử dụng Mamba vì nó sẽ cài đặt nhanh hơn và ít vấn đề hơn.

#### Các bước cài đặt:

1. Mở Anaconda Prompt (trên Mac và Linux, mở cửa sổ terminal)

2. Sử dụng lệnh `cd` để đi đến thư mục chứa repository này:
   ```
   cd C:\Users\TenBan\Documents\CoastSat
   ```

3. Tạo môi trường mới tên `coastsat` với tất cả các gói cần thiết:
   ```
   conda create -n coastsat
   conda activate coastsat
   conda install -c conda-forge geopandas -y
   conda install -c conda-forge earthengine-api scikit-image matplotlib astropy notebook -y
   pip install pyqt5 imageio-ffmpeg
   ```

4. Kích hoạt môi trường:
   ```
   conda activate coastsat
   ```

Dấu hiệu thành công: dòng lệnh của bạn sẽ bắt đầu với `(coastsat)`.

#### Xử lý lỗi

Nếu gặp lỗi trong quá trình cài đặt, hãy thử dọn dẹp với lệnh:
```
conda clean --all
```

Sau đó thử cài đặt lại `coastsat`.

### Bước 2: Kích hoạt Google Earth Engine Python API

1. **Đăng ký tài khoản**: Truy cập https://signup.earthengine.google.com/ để yêu cầu quyền truy cập Google Earth Engine

2. **Cài đặt gcloud CLI**: 
   - Truy cập https://cloud.google.com/sdk/docs/install
   - Tải và cài đặt gcloud CLI
   - Sau khi cài đặt, nó sẽ tự động khởi chạy và cho phép bạn xác thực với tài khoản GEE (hoặc Gmail)

3. **Khởi động lại**: Đóng và mở lại Anaconda Prompt

⚠️ **Quan trọng**: Luôn nhớ kích hoạt môi trường với `conda activate coastsat` mỗi khi sử dụng CoastSat.

## Hướng dẫn Sử dụng

### Khởi động

CoastSat cung cấp hai cách sử dụng:

#### 1. Sử dụng Jupyter Notebook (Khuyến nghị cho người mới)

```bash
conda activate coastsat
jupyter notebook
```

Sau đó mở file `example_jupyter.ipynb` trong trình duyệt web. Jupyter Notebook kết hợp văn bản định dạng và mã nguồn. Để chạy mã, đặt con trỏ vào ô mã và nhấn `Shift + Enter`.

![image](https://user-images.githubusercontent.com/7217258/165960239-e8870f7e-0dab-416e-bbdd-089b136b7d20.png)

#### 2. Sử dụng Python Script

Nếu bạn thích sử dụng IDE như **Spyder**, sử dụng file `example.py`.

**Lưu ý cho Spyder**: Đảm bảo Graphics Backend được đặt thành **Automatic** (không phải **Inline**). Thay đổi tại: Preferences > IPython console > Graphics.

### Truy xuất hình ảnh vệ tinh

#### Các tham số cần thiết:

```python
# Tọa độ vùng quan tâm (kinh độ/vĩ độ theo WGS84)
# Lưu ý: Không vượt quá 100 km²
polygon = [[[151.2957, -33.7012],
            [151.2957, -33.6868],
            [151.3021, -33.6868],
            [151.3021, -33.7012],
            [151.2957, -33.7012]]]

# Khoảng thời gian
dates = ['2017-12-01', '2018-01-01']

# Danh sách vệ tinh
sat_list = ['L5', 'L7', 'L8', 'L9', 'S2']

# Tên địa điểm
sitename = 'NARRABEEN'

# Đường dẫn lưu dữ liệu
filepath = os.path.join(os.getcwd(), 'data')

# Collection của Landsat ('C01' hoặc 'C02')
landsat_collection = 'C02'
```

#### Chạy truy xuất:

```python
metadata = SDS_download.retrieve_images(inputs)
```

Lệnh này sẽ tải hình ảnh vệ tinh và lưu dưới dạng file .TIF trong thư mục `filepath/sitename`. Metadata chứa thông tin về thời gian chụp, hệ quy chiếu và độ chính xác hình học.

⚠️ **Lưu ý quan trọng**: Diện tích polygon không được vượt quá 100 km². Đối với bờ biển dài, chia thành nhiều polygon nhỏ hơn.

### Phát hiện đường bờ

#### Cài đặt cơ bản:

```python
settings = {
    # Ngưỡng độ che phủ mây (0-1)
    'cloud_thresh': 0.5,
    
    # Vùng đệm xung quanh điểm mây (mét)
    'dist_clouds': 300,
    
    # Mã EPSG cho hệ tọa độ đầu ra
    'output_epsg': 28356,
    
    # Kiểm tra thủ công từng đường bờ
    'check_detection': False,
    
    # Điều chỉnh thủ công ngưỡng phát hiện
    'adjust_detection': False,
    
    # Lưu hình ảnh kết quả
    'save_figure': True
}
```

#### Tạo hoạt ảnh MP4:

```python
# Lưu hình ảnh dạng JPG
SDS_preprocess.save_jpg(metadata, settings)

# Tạo video MP4
fps = 4  # Số khung hình mỗi giây
fn_animation = 'animation.mp4'
SDS_tools.make_animation_mp4(fp_images, fps, fn_animation)
```

#### Đường bờ tham chiếu (Rất khuyến nghị):

Trước khi chạy phát hiện hàng loạt, bạn nên số hóa thủ công một đường bờ tham chiếu trên một hình ảnh không có mây:

```python
settings['reference_shoreline'] = SDS_preprocess.get_reference_sl_manual(metadata, settings)
settings['max_dist_ref'] = 100  # Khoảng cách tối đa cho phép (mét)
```

![ref_shoreline](https://user-images.githubusercontent.com/7217258/70408922-063c6e00-1a9e-11ea-8775-fc62e9855774.gif)

#### Chạy phát hiện hàng loạt:

```python
output = SDS_shoreline.extract_shorelines(metadata, settings)
```

Khi `check_detection = True`, bạn có thể:
- Nhấn phím **mũi tên phải** (→) để giữ đường bờ
- Nhấn phím **mũi tên trái** (←) để bỏ qua đường bờ
- Nhấn **Escape** để thoát

![map_shorelines](https://user-images.githubusercontent.com/7217258/60766769-fafda480-a0f1-11e9-8f91-419d848ff98d.gif)

#### Kết quả đầu ra:

Kết quả được lưu ở hai định dạng trong thư mục `filepath/data/SITENAME`:
1. **SITENAME_output.pkl**: File Python chứa tọa độ đường bờ, thời gian, độ chính xác
2. **SITENAME_output.geojson**: File có thể mở trong phần mềm GIS (QGIS, ArcGIS)

### Phân tích chuỗi thời gian

#### Định nghĩa các tuyến cắt:

Có 3 cách để tạo các tuyến cắt vuông góc với bờ:

1. **Vẽ tương tác**:
```python
transects = SDS_transects.draw_transects(output, settings)
```

2. **Tải từ file GeoJSON**:
```python
transects = SDS_tools.transects_from_geojson('duong_dan/file.geojson')
```

3. **Tạo thủ công**:
```python
transects = dict([])
transects['Tuyen 1'] = np.array([[342836, 6269215], [343315, 6269071]])
transects['Tuyen 2'] = np.array([[342482, 6268466], [342958, 6268310]])
```

⚠️ **Lưu ý**: Các điểm phải ở hệ tọa độ được định nghĩa bởi `settings['output_epsg']`.

#### Tính giao điểm (Chế độ chất lượng cao):

```python
settings_transects = {
    'along_dist': 25,          # Khoảng cách dọc bờ (m)
    'min_points': 3,           # Số điểm tối thiểu
    'max_std': 15.0,           # Độ lệch chuẩn tối đa (m)
    'max_range': 30.0,         # Phạm vi tối đa (m)
    'min_chainage': -100,      # Khoảng cách tối thiểu (m)
    'multiple_inter': 'auto',  # Xử lý giao điểm đa (auto/nan/max)
    'auto_prc': 0.1           # Ngưỡng tự động
}

cross_distance = SDS_transects.compute_intersection_QA(
    output, transects, settings_transects
)
```

![transects](https://user-images.githubusercontent.com/7217258/49990925-8b985a00-ffd3-11e8-8c54-57e4bf8082dd.gif)

### Hiệu chỉnh triều

Để hiệu chỉnh ảnh hưởng của triều lên đường bờ, bạn cần:

1. **Dữ liệu mực nước**: File CSV chứa chuỗi thời gian mực nước (theo giờ UTC)
   - Ví dụ: [NARRA_tides.csv](https://github.com/kvos/CoastSat/blob/master/examples/NARRA_tides.csv)
   - Mốc cao độ: xấp xỉ Mực nước biển trung bình

2. **Độ dốc mặt bãi biển**: Ước lượng cho mỗi tuyến cắt
   - Có thể tính toán bằng [CoastSat.slope](https://github.com/kvos/CoastSat.slope)
   - Tham khảo: [Vos et al. 2020](https://doi.org/10.1029/2020GL088365)

**Lưu ý**: Hiệu chỉnh sóng dâng (wave setup) và sóng tràn (runup) không được tích hợp. Xem thêm [Castelle et al. 2021](https://doi.org/10.1016/j.geomorph.2021.107707).

### Xử lý hậu kỳ

#### Loại bỏ nhiễu:

```python
settings_outliers = {
    'max_cross_change': 40,    # Thay đổi tối đa cho phép (m)
    'otsu_threshold': [-0.5, 0] # Ngưỡng Otsu hợp lệ
}

output_clean = SDS_transects.reject_outliers(
    cross_distance, output, settings_outliers
)
```

![image](https://user-images.githubusercontent.com/7217258/182162154-9d8da81d-a5fc-486e-baf6-55e2a5782096.png)

#### Tính trung bình theo mùa:

```python
monthly_data = SDS_transects.monthly_averages(
    cross_distance, output
)

seasonal_data = SDS_transects.seasonal_averages(
    cross_distance, output
)
```

![NA1_seasonally](https://github.com/kvos/CoastSat/assets/7217258/c98cfb7e-b6c6-45d6-9168-86b3c7cb5ed9)

⚠️ **Quan trọng**: Để ước lượng xu hướng dài hạn, nên sử dụng dữ liệu trung bình theo mùa vì mật độ dữ liệu không đồng đều theo thời gian.

## Ví dụ

### Ví dụ đầy đủ cho bãi biển Narrabeen-Collaroy (Úc)

```python
import os
import numpy as np
from coastsat import SDS_download, SDS_preprocess, SDS_shoreline, SDS_transects

# 1. Định nghĩa vùng quan tâm
inputs = {
    'polygon': [[[151.2957, -33.7012],
                 [151.2957, -33.6868],
                 [151.3021, -33.6868],
                 [151.3021, -33.7012],
                 [151.2957, -33.7012]]],
    'dates': ['2017-12-01', '2018-01-01'],
    'sat_list': ['L8', 'S2'],
    'sitename': 'NARRABEEN',
    'filepath': os.path.join(os.getcwd(), 'data'),
    'landsat_collection': 'C02'
}

# 2. Tải hình ảnh
metadata = SDS_download.retrieve_images(inputs)

# 3. Cài đặt phát hiện
settings = {
    'cloud_thresh': 0.5,
    'dist_clouds': 300,
    'output_epsg': 28356,
    'check_detection': True,
    'save_figure': True
}

# 4. Tạo đường bờ tham chiếu
settings['reference_shoreline'] = SDS_preprocess.get_reference_sl_manual(
    metadata, settings
)
settings['max_dist_ref'] = 100

# 5. Trích xuất đường bờ
output = SDS_shoreline.extract_shorelines(metadata, settings)

# 6. Vẽ tuyến cắt
transects = SDS_transects.draw_transects(output, settings)

# 7. Tính giao điểm
cross_distance = SDS_transects.compute_intersection_QA(
    output, transects, settings
)

# 8. Loại bỏ nhiễu và tính trung bình
output_clean = SDS_transects.reject_outliers(cross_distance, output)
seasonal_data = SDS_transects.seasonal_averages(cross_distance, output)
```

## Tính năng Nâng cao

### Huấn luyện lại bộ phân loại

CoastSat sử dụng thuật toán phân loại hình ảnh để gán nhãn mỗi pixel thành 4 lớp: cát, nước, sóng vỡ và các đặc điểm đất liền khác. Nếu bộ phân loại mặc định không hoạt động tốt tại địa điểm của bạn:

1. Thử các bộ phân loại có sẵn bằng cách thay đổi `settings['sand_color']`:
   - `'default'`: Mặc định
   - `'dark'`: Cho bãi biển cát đen/xám
   - `'bright'`: Cho bãi biển cát trắng
   - `'latest'`: Chứa tất cả dữ liệu huấn luyện

2. Huấn luyện bộ phân loại mới:
   - Xem hướng dẫn: [re-train CoastSat classifier](https://github.com/kvos/CoastSat/blob/master/doc/train_new_classifier.md)

### Các tham số nâng cao

- `min_beach_area`: Diện tích tối thiểu cho lớp 'cát' (mặc định: 4500 m²)
- `min_length_sl`: Độ dài tối thiểu của chu vi đường bờ (mặc định: 500 m)
- `cloud_mask_issue`: Xử lý vấn đề mặt nạ mây với bãi biển sáng (mặc định: False)
- `pan_off`: Tắt tăng độ phân giải pan-sharpening (mặc định: False)
- `s2cloudless_prob`: Ngưỡng xác suất mây cho Sentinel-2 (mặc định: 60)

## Đóng góp

Gặp vấn đề? Hãy đăng issue tại [trang Issues](https://github.com/kvos/coastsat/issues).

Muốn đóng góp?
1. Fork repository
2. Tạo branch mới
3. Commit thay đổi của bạn
4. Tạo Pull Request

## Tài liệu tham khảo

### Các repository liên quan

- [CoastSat.slope](https://github.com/kvos/CoastSat.slope): Ước lượng độ dốc mặt bãi biển
- [SDS_Benchmark](https://github.com/SatelliteShorelines/SDS_Benchmark): Bộ kiểm tra cho thuật toán
- [CoastSat.PlanetScope](https://github.com/ydoherty/CoastSat.PlanetScope): Cho hình ảnh PlanetScope
- [CoastSeg](https://github.com/dbuscombe-usgs/CoastSeg): Phân đoạn hình ảnh, deep learning
- [InletTracker](https://github.com/VHeimhuber/InletTracker): Theo dõi cửa sông

### Các bài báo chính

- **Thuật toán phát hiện**: Vos et al. (2019). Environmental Modelling and Software. https://doi.org/10.1016/j.envsoft.2019.104528

- **Đánh giá độ chính xác**: Vos et al. (2019). Coastal Engineering. https://doi.org/10.1016/j.coastaleng.2019.04.004

- **Ước lượng độ dốc bãi biển**: Vos et al. (2020). Geophysical Research Letters. https://doi.org/10.1029/2020GL088365

- **Nghiên cứu Thái Bình Dương**: Vos et al. (2023). Nature Geosciences. https://doi.org/10.1038/s41561-022-01117-8

- **Môi trường triều cường**: Castelle et al. (2021). Geomorphology. https://doi.org/10.1016/j.geomorph.2021.107707

### Bộ dữ liệu

- **Thái Bình Dương**: https://doi.org/10.5281/zenodo.7758183
- **Bờ Đại Tây Dương Mỹ**: https://doi.org/10.5066/P9BQQTCI
- **Độ dốc bãi biển Úc**: https://doi.org/10.5281/zenodo.7272538

## Tài nguyên bổ sung

### Website CoastSat
Truy cập [CoastSat website](http://coastsat.wrl.unsw.edu.au/) để:
- Khám phá và tải bộ dữ liệu đường bờ quy mô khu vực
- Xem dữ liệu cho Pacific Rim, bờ biển Đại Tây Dương Mỹ
- Truy cập các tài nguyên học tập và hướng dẫn

### Hỗ trợ và Cộng đồng
- **Gitter Chat**: [CoastSat/community](https://gitter.im/CoastSat/community)
- **GitHub Issues**: [CoastSat Issues](https://github.com/kvos/CoastSat/issues)
- **Discussions**: Tham gia thảo luận trên GitHub Discussions

## Giấy phép

CoastSat được phát hành dưới giấy phép [GNU GPLv3](https://www.gnu.org/licenses/gpl-3.0).

## Trích dẫn

Nếu bạn sử dụng CoastSat trong nghiên cứu của mình, vui lòng trích dẫn:

```
Vos K., Splinter K.D., Harley M.D., Simmons J.A., Turner I.L. (2019). 
CoastSat: a Google Earth Engine-enabled Python toolkit to extract shorelines 
from publicly available satellite imagery. Environmental Modelling and Software. 
122, 104528. https://doi.org/10.1016/j.envsoft.2019.104528
```

---

**Phiên bản Tiếng Anh**: Xem [README.md](README.md) cho phiên bản tiếng Anh đầy đủ.

**Cập nhật lần cuối**: 2025
