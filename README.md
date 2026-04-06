# 🛒 Olist E-Commerce Analytics: End-to-End Big Data & Machine Learning Pipeline

## Bối cảnh & Mục tiêu dự án
Dự án **Olist E-Commerce Analytics** là một giải pháp dữ liệu toàn diện được thiết kế nhằm giải quyết các bài toán cốt lõi trong vận hành và tiếp thị thương mại điện tử. Lấy cảm hứng từ góc nhìn thực tiễn của ngành E-commerce, hệ thống này khai thác bộ dữ liệu công khai của Olist (Brazil) với hơn 100.000 đơn hàng. Toàn bộ quy trình được phát triển bằng Python và hệ sinh thái PySpark, đi từ bước làm sạch, xử lý ETL, gom cụm 9 bảng dữ liệu quan hệ thành một Master Dataset hoàn chỉnh, cho đến việc triển khai các mô hình học máy (Machine Learning) chuyên sâu.

Thay vì chỉ dừng lại ở phân tích mô tả tĩnh, dự án tập trung vào việc xây dựng một luồng phân tích (ML Pipeline) ứng dụng trực tiếp vào vận hành kinh doanh. Dữ liệu sau khi xử lý được đưa vào các mô hình Phân loại (Classification) và Hồi quy (Regression) để dự đoán chính xác chi phí vận chuyển. Điểm nhấn của dự án nằm ở khả năng thấu hiểu hành vi người dùng: hệ thống tiến hành phân khúc khách hàng theo mô hình RFM kết hợp cùng các thuật toán phân cụm đa dạng (K-Means, Bisecting K-Means, GMM) nhằm nhận diện chính xác tệp khách hàng trung thành và nhóm có nguy cơ rời bỏ. Cùng với đó, trải nghiệm mua sắm được cá nhân hóa triệt để thông qua hệ thống gợi ý sản phẩm (Collaborative Filtering với ALS) và chiến lược bán chéo (Cross-selling) tự động hóa nhờ khai phá luật kết hợp bằng FP-Growth.

Để biến những mô hình kỹ thuật phức tạp thành một sản phẩm có tính ứng dụng cao, toàn bộ pipeline đã được đóng gói và tích hợp thành công lên giao diện web trực quan bằng **Gradio**. Người dùng có thể dễ dàng tương tác, nhập liệu và nhận kết quả dự đoán, gợi ý ngay trên trình duyệt theo thời gian thực.

## Hệ sinh thái Dữ liệu (The Dataset)
Nguồn dữ liệu được khai thác từ bộ [Brazilian E-Commerce Public Dataset by Olist](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce) danh tiếng trên Kaggle. 

Đây là một kho dữ liệu thực tế đồ sộ, ghi nhận hơn 100.000 giao dịch từ năm 2016 đến 2018. Dữ liệu thô ban đầu nằm rải rác ở 9 bảng quan hệ phức tạp (Customers, Orders, Products, Reviews, Geolocation,...). Qua quá trình ETL và làm sạch nghiêm ngặt, dữ liệu đã được hợp nhất thành một **Master Dataset** chuẩn hóa tối ưu với **118,757 dòng** và **45 đặc trưng (features)**, sẵn sàng cho các luồng huấn luyện thuật toán sâu hơn.

## 🛠️ Kiến trúc Công nghệ (Tech Stack)
* **Xử lý Big Data & ML Core:** PySpark 3.5.0, Python 3.12, Spark MLlib
* **Phân tích & Thao tác dữ liệu:** Pandas
* **Trực quan hóa (Data Viz):** Matplotlib, Plotly
* **Triển khai Giao diện (Deployment):** Gradio UI
* **Môi trường phát triển:** Jupyter Notebook, Google Colab / Databricks

## Cấu trúc Pipeline Machine Learning
Luồng xử lý dữ liệu và huấn luyện mô hình được tổ chức bài bản qua 6 giai đoạn, tính toán nối tiếp nhau:

1. **`01_Data_Processing_FN.ipynb` (ETL Pipeline):** Thiết lập luồng làm sạch tự động, xử lý nhiễu/giá trị thiếu, thực hiện các phép Join phức tạp và xuất ra định dạng `.parquet` để tối ưu hóa tốc độ đọc/ghi cho Big Data.
2. **`02_Classification_FN_PL.ipynb` (Predictive Classification):** Xây dựng mô hình Phân loại nhằm dự đoán khả năng khách hàng để lại đánh giá tiêu cực (dựa trên thời gian giao hàng, đặc tính sản phẩm,...), từ đó đưa ra cảnh báo chăm sóc khách hàng kịp thời.
3. **`03_Regression__FN_PL.ipynb` (Logistics Optimization):** Huấn luyện mô hình Hồi quy dự đoán biến số `freight_value` (chi phí vận chuyển) thông qua việc phân tích tương quan giữa khoảng cách địa lý và thông số vật lý của kiện hàng.
4. **`04_Clustering_FN_PL.ipynb` (Customer Segmentation):** Phác họa chân dung khách hàng bằng phân tích RFM (Recency, Frequency, Monetary) kết hợp các thuật toán phân cụm tiên tiến như K-Means, Bisecting K-Means và Gaussian Mixture Model (GMM).
5. **`05_Recommendation_FN_PL.ipynb` (Personalized Recommendation):** Áp dụng thuật toán Collaborative Filtering (Alternating Least Squares - ALS) phân tích các tương tác ngầm (implicit feedback) để xây dựng hệ thống gợi ý sản phẩm mang tính cá nhân hóa cao.
6. **`06_Frequent_Pattern_Mining_FN_PL.ipynb` (Cross-selling Strategy):** Khai phá tập phổ biến bằng FP-Growth và thiết lập luật kết hợp (Association Rules), tạo ra các kịch bản gợi ý mua kèm (thường được mua cùng nhau) tự động và hiệu quả.
7. **`07_WEB_GRADIO_FN.ipynb` (Web UI Deployment):** Tích hợp toàn bộ các mô hình Machine Learning đã huấn luyện thành một ứng dụng web hoàn chỉnh với các tab chức năng chuyên biệt (Dự đoán, Phân cụm khách hàng, Gợi ý cá nhân hóa, Phân tích giỏ hàng), cho phép người dùng phi kỹ thuật dễ dàng thao tác và khai thác giá trị từ dữ liệu.
## Hướng dẫn Triển khai (Getting Started)

**Bước 1: Sao chép kho lưu trữ (Clone the repository)**
```bash
git clone https://github.com/trucptwork-svg/bigdata-customer-analytics-spark.git
cd bigdata-customer-analytics-spark
```

**Bước 2: Cài đặt các thư viện phụ thuộc**
```bash
pip install -r requirements.txt
```

**Bước 3: Khởi chạy Giao diện Tương tác (Web App)**
*(Lưu ý: Đảm bảo các thư mục chứa Pipeline Models đã được đặt đúng vị trí trong `models/` trước khi chạy)*
```bash
python app/app.py
```
Sau khi khởi chạy thành công, mở trình duyệt và truy cập vào `http://localhost:7860` để trải nghiệm trực tiếp các mô hình ML.

*(Ghi chú: Do giới hạn dung lượng của GitHub, bộ Dataset gốc và các file Pipeline Model `.parquet` đã được đưa vào `.gitignore`. Bạn có thể tự tái tạo lại các model này bằng cách chạy tuần tự các notebook trong thư mục `notebooks/`)*

## 👨‍💻 Tác giả (Author)
**Nhóm 11**
