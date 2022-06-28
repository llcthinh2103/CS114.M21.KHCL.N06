<p align="center">
  <a href="https://www.uit.edu.vn/" title="Trường Đại học Công nghệ Thông tin" style="border: 5;">
    <img src="https://i.imgur.com/WmMnSRt.png" alt="Trường Đại học Công nghệ Thông tin | University of Information Technology">
  </a>
</p>

<!-- Title -->
<h1 align="center"><b>ĐỒ ÁN CUỐI KÌ</b></h1>
<h1 align="center"><b>PHÁT HIỆN MỘT SỐ LOẠI BỆNH TRÊN LÁ CÂY SẦU RIÊNG</b></h1>

# **BẢNG MỤC LỤC**

1. [Tổng Quan Về Đồ Án](#tongquan)
2. [Các Nghiên Cứu Về Bài Toán](#cacnghiencuu)
3. [Xây Dựng Bộ Dữ Liệu](#dulieu)
4. [Training Và Đánh Giá Model](#training)
5. [Hướng Phát Triển Ứng Dụng Và Cải Tiến](#ungdung)
6. [Nguồn Tham Khảo](#thamkhao)

<a name="tongquan"></a>
# **1. TỔNG QUAN VỀ ĐỒ ÁN** 
## **1.1 MÔ TẢ BÀI TOÁN**
* Ngữ cảnh ứng dụng:
    * Trong những năm gần đây, diện tích trồng cây sầu riêng luôn được mở rộng từ đồng bằng sông Cửu Long đến tận miền Đông Tây Nguyên, nguyên do là cây mang lại hiệu quả kinh tế bởi năng suất cao, chất lượng ngon đáp ứng được yêu cầu của người tiêu dùng ngay cả trong nước và xuất khẩu.

<p align="center">
<img src="https://user-images.githubusercontent.com/79462324/174416173-1fecf800-518c-4ad2-925f-1eeeb46df569.jpg" style="display: block;margin-left: auto;margin-right: auto;width: 50%; height:50%;"/>
<br>
<a style="text-align: center">Hình . Hình minh họa cây sầu riêng (Nguồn : Internet) </a>
</p>


   
   * Theo Bộ Nông nghiệp và Phát triển nông thôn, tổng kim ngạch xuất nhập khẩu hàng nông, lâm, thủy sản 5 tháng đầu năm 2022 ước đạt khoảng 41,3 tỷ USD, tăng 8,6% so cùng kỳ năm 2021. Đây được xem là tín hiệu khả quan, dù dịch COVID-19 đã đang làm đứt gãy nhiều chuỗi sản xuất, tiêu thụ và xuất khẩu. Tại khu vực Đồng Bằng Sông Cửu Long, trong giỏ hàng thì trái cây lại một lần nữa khẳng định vị thế khi có giá trị xuất khẩu tăng, trong đó đặc biệt phải kể đến là sầu riêng. Cụ thể, xuất khẩu sầu riêng đạt 5 triệu USD, tăng 424% so với cùng kỳ năm 2021. 
<p align="center">
<img src="https://user-images.githubusercontent.com/79462324/174417607-81a4e020-1f50-4b99-af09-783184ce1eb4.png" style="display: block;margin-left: auto;margin-right: auto;width: 50%; height:50%;"/>
<br>
<a style="text-align: center">Hình . Hình minh họa cây sầu riêng (Nguồn : Internet) </a>
</p>

   * Tuy nhiên, với sức tiêu thụ ngày càng khổng lồ của người tiêu dùng trong và cả ngoài nước, chất lượng của quả sầu riêng vẫn chưa đáp ứng được các tiêu chuẩn về độ ngọt, hàm lượng dinh dưỡng, trọng lượng,... Nhằm nâng cao chất lượng của quả sầu riêng, việc phát hiện và xử lý những loại bệnh trên lá của cây là rất quan trọng. Nhận thấy được vấn đề đó nên nhóm đã quyết định áp dụng những kiến thức của mình và những công nghệ trong lĩnh vực Machine Learning để giải quyết bài toán phát hiện một số loại bệnh trên lá cây sầu riêng.
   * Mô hình hướng tới đối tượng người dùng là người trồng sầu riêng. Mục đích là xây dựng một mô hình ứng dụng có thể giúp người nông dân phát hiện chính xác hơn các loại bệnh đang gặp phải trên lá cây để có hướng chữa trị phù hợp để loại bỏ bệnh và các tác nhân gây bệnh. 

* Input: 
    * Một tấm ảnh chụp hình lá của cây sầu riêng đang bị bệnh.
    * Ảnh chụp mặt trên của lá 
    * Ảnh chụp góc thẳng trực diện và lá
    * Ảnh không bị nhiễu và có ánh sáng tốt 
    * Ảnh chụp cách lá ít nhất một khoảng 10 cm
* Output: Một tấm ảnh với bounding box bao quanh lá bị bệnh và tên loại bệnh nằm trên bbox tương ứng

<p align="center">
<img src="https://user-images.githubusercontent.com/79583501/173473224-71645756-2cd7-4338-b7d2-f6be40182d81.png" style="display: block;margin-left: auto;margin-right: auto;width: 50%; height:50%;"/>
<br>
<a style="text-align: center">Hình . Ví dụ về input và output ChayLa</a>
</p>

<p align="center">
<img src="https://user-images.githubusercontent.com/79583501/173473511-27444508-db74-4f58-a8c0-8f410b06a990.png" style="display: block;margin-left: auto;margin-right: auto;width: 75%; height:75%;"/>
<br>
<a style="text-align: center">Hình . Ví dụ về input và output DomTrang</a>
</p>


## **1.2 MÔ TẢ DỮ LIỆU**

* Bộ dữ liệu của mô hình được nhóm thu thập từ một số vườn chuyên trồng sầu riêng trên địa bàn huyện Chợ Lách, tỉnh Bến Tre. Trong quá trình thu thập dữ liệu, nhóm gặp nhiều khó khăn như điều kiện di chuyển đến các vườn sầu riêng khá xa so với nơi ở hiện tại ở TPHCM (130km). Hơn nữa, để đến được các vườn sầu riêng cần phải đi xuồng qua sông lớn đến các cù lao chuyên canh tác sầu riêng. Và do sầu riêng là cây ăn quả lâu năm nên kích thước rất lớn và cao, gây khó khăn cho việc thu thập dữ liệu. 
<p align="center">
<img src="https://user-images.githubusercontent.com/79462324/174419313-25682449-dce3-42cc-9b02-9d904826300a.png" style="display: block;margin-left: auto;margin-right: auto;width: 50%; height:50%;"/>
<br>
<a style="text-align: center">Hình . Ảnh quá trình thu thập dữ liệu tại vườn sầu riêng thuộc Thị trấn Chợ Lách, huyện Chợ Lách, tỉnh Bến Tre</a>
</p>

* Bộ dữ liệu về lá cây sầu riêng hiện nay chưa có ai thu thập nên số lượng dữ liệu mà nhóm có vẫn còn hạn chế do dữ liệu tự thu thập và xử lý. Mục đích của việc tự thu thập dữ liệu là để phù hợp với ngữ cảnh ứng dụng của bài toán. 

<a name="cacnghiencuu"></a>
# **2. CÁC NGHIÊN CỨU TRƯỚC ĐÓ**
Hiện nay, trong lĩnh vực thị giác máy tính nói riêng hay lĩnh vực máy học nói chung, các vấn đề phân loại (classification) và nhận diện vật thể (object detection) xuất hiện rất nhiều trong bài toán đã được đặt ra và đã được giải quyết. Những bài toán này được giải quyết bằng các mô hình machine learning và deep learning như YOLO, VGG-16, Resnet-50 dựa trên kiến trúc mạng CNN (Convolutional Neural Network) và nhiều mô hình với các kiến trúc khác.

<a name="dulieu"></a>
# **3. XÂY DỰNG BỘ DỮ LIỆU**
## **3.1 QUÁ TRÌNH THU THẬP**
* Dữ liệu được nhóm thu thập thủ công bằng camera của điện thoại.
* Điện thoại sử dụng: Vivo S1, SamSung Galaxy J4+
* Mỗi tấm ảnh gốc có kích thước 3456 x 4608 (camera nằm ngang), 4608 x 3456 (camera nằm dọc)
* Bộ dữ liệu được thu thập trong hai ngày 30/05/2022 và 15/06/2022 
<p align="center">
<img src="https://user-images.githubusercontent.com/79462324/174421483-c2f3a794-56f5-49bb-958c-fbb7e1bceacb.png" style="display: block;margin-left: auto;margin-right: auto;width: 75%; height:75%;"/>
<br>
<a style="text-align: center">Hình . Độ phân giải và camera sử dụng </a>
</p>

* File ảnh được lưu trữ trong cùng 1 folder trên máy tính dưới dạng tệp .jpg
* Thống kê về thời gian và chi tiết về dữ liệu: 
 
  

</p>
<p align="center">
<img src="https://user-images.githubusercontent.com/79462324/174469081-badb3852-d62c-4a63-b79b-ae18cb75b459.png" style="display: block;margin-left: auto;margin-right: auto;width: 75%; height:75%;"/>
<br>
<a style="text-align: center">Bảng . Thời gian, địa điểm thu thập và chi tiết về dữ liệu</a>
</p>



## **3.2 TIÊU CHÍ KHI THU THẬP DỮ LIỆU**
* Chụp toàn bộ chiếc lá hoặc chùm lá bị bệnh.
* Chụp rõ nét phần lá bị bệnh.
* Đảm bảo ánh sáng ban ngày.

## **3.3 GÁN NHÃN DỮ LIỆU**
* Nhóm sử dụng Roboflow để gán nhãn dữ liệu [9].
<p align="center">
<img src="https://user-images.githubusercontent.com/79583501/173475500-dca5d64a-a847-49e2-8952-303a810da625.png" style="display: block;margin-left: auto;margin-right: auto;width: 75%; height:75%;"/>
<br>
<a style="text-align: center">Hình . Gán nhãn dữ liệu trên roboflow</a>
</p>

* Tiêu chí khi gán nhãn:
    * Gán phần lá bị bệnh (không bao gồm cuốn)
    * Gán nhãn đối với các lá bị che khuất, mờ, nhỏ
    * Nếu lá bị che khuất phần lớn thì sẽ không gán


<p align="center">
<img src="https://user-images.githubusercontent.com/79583501/176161740-955b14cf-aee5-498b-a52a-05dd191206b0.png" style="display: block;margin-left: auto;margin-right: auto;width: 75%; height:75%;"/>
<br>
<a style="text-align: center">Hình . Ví dụ gán nhãn dữ liệu</a>
</p>






**Label 1: Bệnh cháy lá**
* Bệnh cháy lá sầu riêng có thể phát sinh trên cả lá non và lá già, biểu hiện ban đầu là những đốm nhỏ, sũng nước, sau đó chúng liên kết lại thành mảng bất dạng nhũn nước hay phỏng nước sôi trên lá. Sau đó những đốm bệnh này khô đi và chuyển sang màu nâu sáng với rìa màu nâu tối khiến cho lá bị biến dạng và bị quăn lại [6].
<p align="center">
<img src="https://user-images.githubusercontent.com/79583501/171002992-38021761-1b44-4d33-b79d-3d6c4d14cd63.png" style="display: block;margin-left: auto;margin-right: auto;width: 100%; height:100%;"/>
<br>
<a style="text-align: center">Hình . Một số ví dụ về bệnh cháy lá</a>
</p>

**Label 2: Bệnh đốm trắng**
* Bệnh thường xuất hiện chủ yếu trên lá già trong những điều kiện độ ẩm cao, mật độ cây trong vườn dày đặc, rậm rạp. Đặc biệt xuất hiện ở giai đoạn trước và sau khi thu hoạch cho cây đang suy yếu trong thời gian mang trái. Lá bị bệnh thường có những đốm nhung có màu sắc giống như sắt rỉ hoặc màu vàng cam, một thời gian sau chuyển sang màu xanh xám. Những đốm này có thể tụ họp lại thành mảng lớn trên lá [7].
<p align="center">
<img src="https://user-images.githubusercontent.com/79583501/171003346-7fcb90d1-2dca-4df7-a45f-1c85d4cf9db8.png" style="display: block;margin-left: auto;margin-right: auto;width: 100%; height:100%;"/>
<br>
<a style="text-align: center">Hình . Một số ví dụ về bệnh đốm lá (đốm trắng) </a>
</p>

## **3.4. THỐNG KÊ BỘ DỮ LIỆU** 
* Bộ dữ liệu:
    * train: bao gồm 150 được tăng cường lên thành 1500 ảnh
    * validation: bao gồm 50 ảnh
    * test: bao gồm 100 ảnh
<p align="center">
<img src="https://user-images.githubusercontent.com/79583501/174441538-a31e8391-3faa-4f06-9154-0c7a8defa24f.png" style="display: block;margin-left: auto;margin-right: auto;width: 50%; height:50%;"/>
<br>
<a style="text-align: center">Hình . Thống kê dữ liệu</a>
</p>

* Train dataset sau khi đã tăng cường dữ liệu có tổng số object là 3284, trong đó:
    * 1378 đối tượng lớp ChayLa
    * 1906 đối tượng lớp DomTrang
* Validation dataset có tổng số object là 130, trong đó:
    * 51 đối tượng lớp ChayLa
    * 79 đối tượng lớp DomTrang
* Test dataset  có tổng số object là 262, trong đó:
    * 94 đối tượng lớp ChayLa
    * 168 đối tượng lớp DomTrang
<p align="center">
<img src="https://user-images.githubusercontent.com/79583501/174441522-0f2d7f9f-c1e4-4647-9cb2-9abf35fe33cb.png" style="display: block;margin-left: auto;margin-right: auto;width: 50%; height:50%;"/>
<br>
<a style="text-align: center">Hình . Thống kê dữ liệu</a>
</p>

<a name="training"></a>
# **4. TRAINING VÀ ĐÁNH GIÁ MODEL**
## **4.1 Nội dung dataset**
### **4.1.1 YOLO**
* Đối với các model YOLO thì trong tập dataset sẽ gồm các file ảnh và các file *.txt ứng với mỗi tấm ảnh.
* Nội dung của file txt: mỗi object được biểu diễn bằng 1 dòng \<object-class> \<x-center> \<y-center> \<width> \<height>
    * Trong đó \<object-class> là số nguyên trong đoạn [0, 1] với số lượng class = 2
    * \<x-center> \<y-center> \<width> \<height> là các số thực được chuẩn hóa có giá trị nằm trong đoạn [0, 1], biểu diễn bouding box của đối tượng.
</p>       
<p align="center">
<img src="https://user-images.githubusercontent.com/79583501/173480508-75503845-a466-4487-9369-562ee2b33e97.png" style="display: block;margin-left: auto;margin-right: auto;width: 75%; height:75%;"/>
<br>
<a style="text-align: center">Hình . Format label YOLO</a>
</p>

### **4.1.2 Faster RCNN**
* Đối với các model RCNN thì trong tập dataset sẽ gồm các file ảnh và duy nhất file *.json chứa thông tin cho toàn bộ dataset.
* Nội dung của file json: 
    * Đối với mỗi object được biểu diễn bằng 1 đoạn sau: 
    <"image_id": *>, là id của hình ảnh do file *.json chứa thông tin cho toàn bộ dataset
    <"category_id": *>, là số nguyên trong đoạn [0, 1] tượng trưng cho class của vật thể đó.
    <"bbox": x-min y-min width height> với x-min , y-min là tọa độ điểm góc trên cùng bên trái với chiều rộng và chiều cao của bounding box.

<p align="center">
<img src="https://user-images.githubusercontent.com/79583501/173480424-d62191c2-7cf8-42dc-8ac9-087d52da1812.png" style="display: block;margin-left: auto;margin-right: auto;width: 50%; height:50%;"/>
<br>
<a style="text-align: center">Hình . Format label COCO</a>
</p>

<p align="center">
<img src=https://user-images.githubusercontent.com/79445118/174465336-cd6a6d72-6e8e-4041-b5e7-66810bde6f0d.png style="display: block;margin-left: auto;margin-right: auto;width: 100%; height:100%;"/>
<br>
<a style="text-align: center">Hình . Cách tính các giá trị x, y, width, height</a>
</p>    
    
<p align="center">
<img src=https://user-images.githubusercontent.com/79445118/175347550-13c97d29-450c-4d2f-a9b5-4ddf2ae36299.png style="display: block;margin-left: auto;margin-right: auto;width: 100%; height:100%;"/>
<br>
<a style="text-align: center">Hình . Cách tính các giá trị x, y, width, height</a>


## **4.2 CẤU HÌNH TRAINING**
<p align="center">
<img src="https://user-images.githubusercontent.com/79583501/171001486-19287188-83ef-42b0-98ce-981c36e2c36b.png" style="display: block;margin-left: auto;margin-right: auto;width: 100%; height:100%;"/>
<br>
<a style="text-align: center">Hình . Cấu trúc YOLOv4</a>
</p>

## **4.3 TRAINING MODEL**
### **4.3.1 YOLOv4**

#### **4.3.1.1 SƠ LƯỢC VỀ YOLOv4**
* YOLOv4 được giới thiệu bởi Alexey Bochoknovskiy, Chien-Yao Wang, and Hong-Yuan Mark Liao trong bài báo YOLOv4: Optimal Speed and Accuracy of Object Detection xuất bản ngày 23/4/2020 [1]

* YOLO là một mô hình mạng CNN cho việc phát hiện, nhận dạng, phân loại đối tượng. YOLO được tạo ra từ việc kết hợp giữa các convolutional layers và connected layers. Trong đó các convolutional layers sẽ trích xuất ra các đặc trưng của ảnh, còn full-connected layers sẽ dự đoán ra xác suất đó và bounding box của đối tượng. 

* Hiện nay, yolov4 vẫn được đánh giá là một trong những model để xây dựng state-of-the-art objects detector tốt nhất.


<p align="center">
<img src="https://user-images.githubusercontent.com/79583501/171307372-bb8b4868-4d3a-454c-adf5-eab1c939b085.png" style="display: block;margin-left: auto;margin-right: auto;width: 50%; height:50%;"/>
<br>
<a style="text-align: center">Hình . So sánh performance YOLOv4[1]</a>
</p>

* YOLOv4 runs twice faster than EfficientDet with comparable performance. Improves YOLOv3’s AP and FPS by 10% and 12%, respectively. YOLOv4 can achive 43.5% AP (65.7% AP50) for the MS COCO dataset at a realtime speed of ∼65 FPS on Tesla V100
<p align="center">
<img src="https://user-images.githubusercontent.com/79583501/171000673-06d74018-9757-4b93-aaab-23d96abfbdfe.png" style="display: block;margin-left: auto;margin-right: auto;width: 100%; height:100%;"/>
<br>
<a style="text-align: center">Hình . Cấu trúc YOLOv4[1]</a>
</p>

#### **4.3.1.2 THIẾT LẬP TRAINING**
* Clone github chứa source code YOLOv4: https://github.com/AlexeyAB/darknet
<p align="center">
<img src="https://user-images.githubusercontent.com/79583501/174467712-10d22a52-ac07-495a-a775-4f4030806a11.png" style="display: block;margin-left: auto;margin-right: auto;width: 40%; height:40%;"/>
<br>
<a style="text-align: center">Hình . File valid.txt</a>
</p>

* Thiết lập các thông số trong file Makefile để sử dụng GPU cho việc training
<p align="center">
<img src="https://user-images.githubusercontent.com/79583501/174467575-d7b00eb7-6b71-4a95-8c38-84bd5076584e.png" style="display: block;margin-left: auto;margin-right: auto;width: 40%; height:40%;"/>
<br>
<a style="text-align: center">Hình . File valid.txt</a>
</p>

* Thiết lập các thông số của model YOLOv4 trong file yolov4-custom.cfg:
    * batch = 64 `số lượng sample cho một iteration`
    * subdivisions = 16 `số block = batch / subdivisions để đưa vào GPU để sử lý song song`
    * max_batches = 4000 (Bằng số class * 2000) `số iterations để training model`
    * steps = 3200, 3600 (Bằng 0.8 * max_batches, 0.9 * max_batches) `learning rate sẽ được điều chỉnh sau 80%, 90% max_batches`
    * width = 416, height = 416 `YOLOv4 sẽ resize ảnh trước khi cho vào mô hình`
    * classes = 2 (Số class). Chỉnh sửa dòng classes=80 ở các layee [yolo]thành số lượng classes có trong dataset
    * filters = 21. Chỉnh sửa dòng filter = 255 ở layer conv ngay trước layer [yolo] thành (số classes + 5) * 3 `số convolutional kernels có trong layer đó`

`Các thông số khác trong file config có thể xem thêm tại đây: `
* https://github.com/AlexeyAB/darknet/wiki/CFG-Parameters-in-the-%5Bnet%5D-section
* https://github.com/AlexeyAB/darknet/wiki/CFG-Parameters-in-the-different-layers

<p align="center">
<img src="https://user-images.githubusercontent.com/79583501/171085332-e76d9e1d-df86-479b-b7c9-fccec6f22831.png" style="display: block;margin-left: auto;margin-right: auto;width: 50%; height:50%;"/>
<br>
<a style="text-align: center">Hình . Cấu hình training</a>
</p>

<p align="center">
<img src="https://user-images.githubusercontent.com/79583501/171085414-aebb5e64-caea-455e-b2a3-f63bb8d2ccf3.png" style="display: block;margin-left: auto;margin-right: auto;width: 25%; height:25%;"/>
<br>
<a style="text-align: center">Hình . Cấu hình training</a>
</p>

<p align="center">
<img src="https://user-images.githubusercontent.com/79583501/171085453-0c938965-60a6-46ee-af31-846157f4d49c.png" style="display: block;margin-left: auto;margin-right: auto;width: 25%; height:25%;"/>
<br>
<a style="text-align: center">Hình . Cấu hình training</a>
</p>

* Tạo file obj.names chứa tên của các class
<p align="center">
<img src="https://user-images.githubusercontent.com/79583501/174467662-4fe2deac-eaaf-4bdd-8ab9-bd2d528e906d.png" style="display: block;margin-left: auto;margin-right: auto;width: 25%; height:25%;"/>
<br>
<a style="text-align: center">Hình . File obj.names</a>
</p>

* Tạo folder backup trong folder darknet để lại lại các trọng số của model trong quá trình training

* Tạo file obj.data có nội dung như sau
    * Số classes có trong dataset
    * File train.txt chứa các đường dẫn dẫn đến ảnh trong tập train
    * File valid.txt chứa các đường dẫn dẫn đến ảnh trong tập test (valid)
    * backup folder chứa file weights khi huấn luyện mô hình
<p align="center">
<img src="https://user-images.githubusercontent.com/79583501/171179655-968ac023-d903-45e9-a1ec-916a9058096a.png" style="display: block;margin-left: auto;margin-right: auto;width: 25%; height:25%;"/>
<br>
<a style="text-align: center">Hình . File obj.data</a>
</p>

* Tạo file train.txt chứa đường dẫn tới các ảnh dùng để train
<p align="center">
<img src="https://user-images.githubusercontent.com/79583501/175900896-2adff01d-7163-466f-bbfb-308fef92e3a0.png" style="display: block;margin-left: auto;margin-right: auto;width: 75%; height:75%;"/>
<br>
<a style="text-align: center">Hình . File train.txt</a>
</p>

* Tạo file valid.txt chứa đường dẫn tới các ảnh dùng để đánh giá trong quá trình train

<p align="center">
<img src="https://user-images.githubusercontent.com/79583501/175901918-59d1b326-a3ae-4ed0-9dc1-045030205a5f.png" style="display: block;margin-left: auto;margin-right: auto;width: 75%; height:75%;"/>
<br>
<a style="text-align: center">Hình . File valid.txt</a>
</p>





#### **4.3.1.3 TIẾN HÀNH TRAINING**
* Trong quá trình train model các file trọng số được lưu lại:
    * yolov4-custom_last.weights (Trọng số của interation mới nhất)
    * yolov4-custom_best.weights (Trọng số tốt nhất)
    * Các file trọng số được lưu lại cứ mỗi 1000 iteration
* Cú pháp tiến hành training
<p align="center">
  ./darknet <đường dẫn file obj.data> <đường dẫn file config> <đường dẫn file trọng số>
</p>
  
* Tiến hành training lần đầu

<p align="center">
<img src="https://user-images.githubusercontent.com/79583501/171991176-1936258f-07f4-4844-a9f1-f455dfe2da71.png" style="display: block;margin-left: auto;margin-right: auto;width: 75%; height:75%;"/>
<br>
<a style="text-align: center">Hình . Tiến hành training YOLOv4</a>
</p>

* Do giới hạn sử dụng GPU của google colab nên trong quá trình training cần dừng lại để chờ được cấp lại GPU. Tiếp tục training trên file trọng số mới nhất như sau:
<p align="center">
<img src="https://user-images.githubusercontent.com/79583501/171991207-5fe5e8d8-46b7-4e08-9a18-a1e50510ccf9.png" style="display: block;margin-left: auto;margin-right: auto;width: 75%; height:75%;"/>
<br>
<a style="text-align: center">Hình . Tiếp tục training YOLOv4</a>
</p>

### **4.3.2 FASTER R-CNN**

#### **4.3.2.1 SƠ LƯỢC VỀ FASTER R-CNN**  
* Faster R-CNN là một mô hình single-stage, được giới thiệu bởi Shaoqing Ren, Kaiming He, Ross Girshick, and Jian Sun trong bài báo Towards Real-Time Object Detection with Region Proposal Networks vào năm 2016
* Faster R-CNN là một phương pháp cải tiến hơn dựa trên 2 phương pháp trước đó là R_CNN và Fast R-CNN. Faster R-CNN là sự kết hợp giữa Fast-RCNN với một mạng mới có tên gọi là Region Proposal Network(RPN)
* Bằng việc sử dụng RPN để tìm ra vùng có khả năng chứa đối tượng, Faster R-CNN đã tiết kiệm được nhiều thời gian hơn so với cách sử dụng thuật toán Selective Search 
<p align="center">
<img src="https://user-images.githubusercontent.com/79583501/175292035-d2fcbd11-ca78-43fa-a607-babc46637182.png" style="display: block;margin-left: auto;margin-right: auto;width: 75%; height:75%;"/>
<br>
<a style="text-align: center">Hình . Cấu trúc của Faster R-CNN [2]</a>
</p>
  
  
#### **4.2.2.2 THIẾT LẬP TRAINING**
Nhóm sử dụng detectron 2, Detetron2 là một framework để xây dựng bài toán Object Detetion and Segmentation. Nhóm sử dụng X101-FPN là model pretrained để tiến hành huấn luyện trên tập dữ liệu mới [10].
<p align="center">
<img src="https://user-images.githubusercontent.com/79583501/171989700-e8dcac29-84ca-4ff4-9ee5-5b4159bbbcd2.png" style="display: block;margin-left: auto;margin-right: auto;width: 75%; height:75%;"/>
<br>
<a style="text-align: center">Hình . Chọn pretrained model</a>
</p>

`Detectron2 Model Zoo and Baselines:` https://github.com/facebookresearch/detectron2/blob/main/MODEL_ZOO.md
  
  
Các tham số đã được điều chỉnh:
    * IMS_PER_BATCH
    * MAX_ITER
    * NUM_CLASSES
    * EVA_PERIOD
    * CHECKPOINT_PERIOD
    * OUTPUT_DIR
  

### **4.3.3 YOLOv5**
#### **4.3.3.1 SƠ LƯỢC VỀ YOLOv5**
YOLOv5 là một mô hình Object Detection thuộc họ mô hình YOLO. Nếu các bạn chưa biết thì 3 phiên bản YOLO đầu tiên được phát triển bởi Joseph Redmon. Sau đó, Alexey Bochkovskiy cho ra mắt YOLOv4 với sự cải thiện cả về tốc độ cũng như độ chính xác. Và rồi YOLOv5 được công bố gần đây với những so sánh ban đầu cho thấy độ chính xác tương đương YOLOv4 và có tốc độ nhanh hơn khi thực hiện dự đoán (tuy nhiên vẫn có rất nhiều hoài nghi về độ tin cậy của những so sánh này vì YOLOv5 mới được ra mắt trên GitHub chứ chưa có bài báo chính thức nào cả).
#### **4.2.3.2 THIẾT LẬP TRAINING**
* Tạo file data.yaml như sau:
<p align="center">
<img src="https://user-images.githubusercontent.com/79583501/174467789-ecdc1b03-c792-4022-a951-90639686a60a.png" style="display: block;margin-left: auto;margin-right: auto;width: 75%; height:75%;"/>
<br>
<a style="text-align: center">Hình . File data.yaml</a>
</p>

* Thiết lập training
    * batch: 32 `số ảnh được xử lý trong 1 iteration`
    * img: 416 `kích thước mà mô hình sẽ resize để xử lý`
    * epochs: 500 `số iterations training`
    * weights: pretrained weights của model được chọn sử dụng
* Nhóm chọn pretrained model YOLOv5s để tiến hành huấn luyện [8]
<p align="center">
<img src="https://user-images.githubusercontent.com/79583501/172003627-13fc664d-bc19-4953-9ec9-e16a380eb72b.png" style="display: block;margin-left: auto;margin-right: auto;width: 75%; height:75%;"/>
<br>
<a style="text-align: center">Hình . Chọn pretrained model</a>
</p>

`YOLOv5 pretrained model:` https://github.com/ultralytics/yolov5#pretrained-checkpoints  

#### **4.3.3.3 TIẾN HÀNH TRAINING**
* Tiến hành training lần đầu
<p align="center">
<img src="https://user-images.githubusercontent.com/79583501/171991086-44dc560d-9a35-4317-8550-0dc2c5112aae.png" style="display: block;margin-left: auto;margin-right: auto;width: 75%; height:75%;"/>
<br>
<a style="text-align: center">Hình . Tiến hành training YOLOv5</a>
</p>

* Tiếp tục training trên file trọng số mới nhất
<p align="center">
<img src="https://user-images.githubusercontent.com/79583501/172000648-b14adb95-3681-4b23-a0ce-f5c16a53f6bf.png" style="display: block;margin-left: auto;margin-right: auto;width: 25%; height:25%;"/>
<br>
<a style="text-align: center">Hình . Tiếp tục training trên file trọng số mới nhất</a>
</p>

* Trong quá trình train model các file trọng số được lưu lại:
    * last.pt (Trọng số của interation mới nhất)
    * best.pt (Trọng số tốt nhất)

## **4.4 ĐÁNH GIÁ MODEL**
### **4.4.1 METRIC ĐÁNH GIÁ**
* Để đánh giá các model detector và cũng như để so sánh các model với nhau thì nhóm sẽ sử dụng thông số mAP (mean average precision), đặc biệt tập trung vô các chỉ số mAP như AP, AP50, AP75. mAP cũng là một các đánh giá phổ biển cho các model detector hiện nay.
  
* Trước khi vào phần đánh giá mAP, nhóm xin trình bày lại các khái niệm có liên quan trước:
    * **IoU (Intersection Over Union)**: độ do overlap giữa các bbox, cụ thể là giữa grounth truth bounding box, bbox mà nhóm đã gán nhãn với bounding box mà mô hình dự đoán. 
<p align="center">
<img src="https://user-images.githubusercontent.com/79583501/172040923-471cd707-b884-473f-a667-1ef56502d5bf.png" style="display: block;margin-left: auto;margin-right: auto;width: 75%; height:75%;"/>
<br>
<a style="text-align: center">Hình . IOU (Nguồn : Internet)</a>
</p>
  
* a
    * Giá trị IoU sẽ có giá trị nằm trong đoạn [0,1]. Dựa vào đó có thể xác định được cái kết quả:
        * **True Positive (TP)**: những bbox có IOU >= ngưỡng
        * **False Positive (FP)**: những bbox có IOU < ngưỡng
        * **False Negative (FN)**: những bbox model không dự đoán được 
                                                             
<p align="center">
<img src="https://user-images.githubusercontent.com/79583501/176114186-3747e218-f0fb-4be7-9d65-c3221b73a1b3.png" style="display: block;margin-left: auto;margin-right: auto;width: 75%; height:75%;"/>
<br>
<a style="text-align: center">Hình . Ví dụ về TP, FP và FN [11]</a>
</p>
  
* a
    * **Precision**: cho biết tỉ lệ bbox được dự đoán có IOU >= ngưỡng 
    $$Precision = \frac{TP}{TP + FP} = \frac{TP}{All detections}$$
    * **Recall**: cho biết tỉ lệ bbox được sự đoán có IOU >= ngưỡng trên tổng số ground-truth bbox 
    $$Recall = \frac{TP}{TP + FN} = \frac{TP}{All ground-truth}$$
    * Nếu có nhiều predicted bbox xếp chồng lên nhau trong cùng một ground-truth bbox thì ta sẽ chọn predicted bbox có IoU lớn nhất là TP, còn lại là FP   
    * **AP (Average precision)**: là chỉ số được tính dựa trên precision và recall. Trong các bài toán detection, với mỗi chỉ số IOU khác nhau ta sẽ có chỉ số precision và recall khác nhau.
Khi tổng hợp lại các precision và recall ở các ngưỡng IoU khác nhau, ta sẽ có biểu đồ precision-recall curve (PR-Curve)

  
<p align="center">
<img src="https://user-images.githubusercontent.com/79583501/175804097-d5dde0fb-b348-43af-933f-d369b6dae02f.png" style="display: block;margin-left: auto;margin-right: auto;width: 75%; height:75%;"/>
<br>
<a style="text-align: center">Hình . Ví dụ về Precision-Recall Curve (Nguồn : Internet)</a>
</p>

* a
    * Khi đó AP sẽ là diện tích phần nằm dưới PR-Curve. Khi đó mAP sẽ là trung bình các AP của tất cả các lớp.
    * IoU có ý nghĩa quan trọng đối với chỉ số mAP và việc lựa chọn giá trị của IoU sẽ ảnh hưởng đến kết quả đánh giá của model. Khi ngưỡng IoU thay đổi Precision – Recall cũng thay đổi. Trong các bài toán detection, chúng ta tính toán chỉ số precision và recall với một ngưỡng IoU cho trước, ví dụ đơn giản nhất là nếu ta cho ngưỡng IoU bằng 0.4 và chỉ số IoU sau khi tính toán trên bbox được dự đoán là 0.5 thì ta tính rằng bbox được dự đoán đó là đúng, tuy nhiên nếu đặt ngưỡng IoU bằng 0.6 thì với chỉ số IoU sau khi tính toán trên bbox được dự đoán là 0.5 thì bbox được dự đoán đó là sai. Do đó, tại một giá trị IoU xác định,ta có thể do/đánh giá được mô hình một cách tốt nhất.
    


<p align="center">
<img src="https://user-images.githubusercontent.com/79583501/176115743-d1f5969f-fc8a-442e-aca9-8897d8827408.png" style="display: block;margin-left: auto;margin-right: auto;width: 75%; height:75%;"/>
<br>
<a style="text-align: center">Hình . Mean Average Precision [11]</a>
</p>
    
    

### **4.4.2 KẾT QUẢ ĐÁNH GIÁ**
* YOLOv4
<p align="center">
<img src="https://user-images.githubusercontent.com/79583501/175068337-f9920efc-d6a8-4fa0-8a90-d8aa0add9b38.png" style="display: block;margin-left: auto;margin-right: auto;width: 75%; height:75%;"/>
<br>
<a style="text-align: center">Hình . Kết quả đánh giá model YOLOv4</a>
</p>
<br/>
<br/>
<div align="center">
  
| Class    |      AP50         | 
|----------|:-----------------:|
| ChayLa   |  0.6545           | 
| DomLa    |  0.6258           |  

</div>
  
<p align="center">
Bảng . Kết quả đánh giá model YOLOv4
</p>
  
  
* YOLOv5
  
<p align="center">
<img src="https://user-images.githubusercontent.com/79583501/175068447-88483234-9215-4e68-888a-3dd2c31e51ce.png" style="display: block;margin-left: auto;margin-right: auto;width: 75%; height:75%;"/>
<br>
<a style="text-align: center">Hình . Kết quả đánh giá model YOLOv5</a>
</p>
  
<br/>
<br/>
  
<div align="center">
  
| Class    |      AP50        |  
|----------|:----------------:| 
| ChayLa   |  0.5840          |  
| DomLa    |  0.7620          |  

</div>

<p align="center">
Bảng . Kết quả đánh giá model YOLOv5
</p>
  
  
* Faster R-CNN
<p align="center">
<img src="https://user-images.githubusercontent.com/79583501/175298328-b79f8e9a-03cf-4bfd-a26e-7547d4acb9d4.png" style="display: block;margin-left: auto;margin-right: auto;width: 75%; height:75%;"/>
<br>
<a style="text-align: center">Hình . Kết quả đánh giá model Faster R-CNN</a>
</p>

<br/>
<br/>
  
<div align="center">
  
| Class       |      AP50        |  
|-------------|:----------------:|
| ChayLa      |  0.6822          |  
| DomTrang    |  0.7576          |  
</div>
  
  
  
<p align="center">
Bảng . Kết quả đánh giá model Faster R-CNN
</p>
<a name="thamkhao"></a>
  
  
  
* Tổng kết đánh giá AP50
 <div align="center">
  
| Class            |      ChayLa      |     DomTrang     |     All       |
|------------------|:----------------:|:----------------:|:-------------:|
| YOLOv4           |  0.6545          |  0.6258          |  0.6401       |
| YOLOv5           |  0.5840          |  0.7260          |  0.6550       |
| Faster R-CNN     |  <ins>0.6822     |  <ins>0.7576     |  <ins>0.7100  |
</div>

   
-> Khi đánh giá bằng điểm AP@0.5, Faster RCNN đều cho kết quả tốt hơn cả 2 model còn lại
* Một số hình ảnh test :
   
<p align="center">
<img src="https://user-images.githubusercontent.com/79462324/175332365-bffa5671-95fb-470b-8bb3-f33550b5eb2b.png" style="display: block;margin-left: auto;margin-right: auto;width: 100%; height:100%;"/>
<br>
<a style="text-align: center">Hình . Kết quả test</a>
</p>
   
> Cả ba model đều cho kết quả chính xác khi detect được 2 lá bị bệnh.
   
   
   
<p align="center">
<img src="https://user-images.githubusercontent.com/79462324/175335978-ce112080-815a-4582-963e-72695c91be0c.png" style="display: block;margin-left: auto;margin-right: auto;width: 100%; height:100%;"/>
<br>
<a style="text-align: center">Hình . Kết quả test</a>
</p>
   
> YOLOv4 cho kết quả chính xác, YOLOv5 và Faster R-CNN detect sai lá bình thường thành lá bệnh cháy lá.
   
   
<p align="center">
<img src="https://user-images.githubusercontent.com/79462324/175336571-9aedc676-416f-423e-8a64-4019d511e72f.png" style="display: block;margin-left: auto;margin-right: auto;width: 100%; height:100%;"/>
<br>
<a style="text-align: center">Hình . Kết quả test</a>
</p>
   
> YOLOv4 cho kết quả chính xác, YOLOv5 và Faster R-CNN vẫn detect sai lá bình thường thành lá bệnh cháy lá. Nhưng ở Faster R-CNN vượt trội hơn là detect đúng 1 lá bị cả 2 bệnh.
   
   
   
<p align="center">
<img src="https://user-images.githubusercontent.com/79462324/175337189-d3009849-350d-415e-8a6a-b66f8ba8e127.png" style="display: block;margin-left: auto;margin-right: auto;width: 100%; height:100%;"/>
<br>
<a style="text-align: center">Hình . Kết quả test</a>
</p>
   
> YOLOv4, YOLOv5 cho kết quả chính xác. Nhưng Faster R-CNN detect 1 lá bị cả 2 bệnh. Do bệnh cháy lá trên thân lá cũng có đốm nên Faster R-CNN bị nhầm lẫn. 
 
   
<p align="center">
<img src="https://user-images.githubusercontent.com/79462324/175337926-6071e62b-1621-440c-b626-523631292033.png" style="display: block;margin-left: auto;margin-right: auto;width: 100%; height:100%;"/>
<br>
<a style="text-align: center">Hình . Kết quả test</a>
</p>
   
> Với ảnh có nhiều lá, YOLOv4 và YOLOv5 cho kết quả đúng nhưng bị thiếu khá nhiều bbox. Faster R-CNN detect số bbox nhiều hơn, và độ chính xác cao nhưng vẫn nhầm lẫn lá bình thường với lá bị cháy lá. 
   
* **Test trên bộ ảnh lá bình thường (không bị cháy lá hay đốm trắng):**
   * Cả 3 mô hình vẫn detect sai một số object lá bình thường thành lá bệnh. Cụ thể số object sai trong việc detect lá thường thành lá bệnh: 
      * YOLOv5: 55 object
      * YOLOv4: 40 object
      * Faster R-CNN: 84 object
       (Một ảnh có thể chứa nhiều object)
 <p align="center">
<img src="https://user-images.githubusercontent.com/79462324/175340453-264b7809-67f4-4728-97f0-6e0b5f6b5ba6.png" style="display: block;margin-left: auto;margin-right: auto;width: 100%; height:100%;"/>
<br>
<a style="text-align: center">Hình . Kết quả test</a>
</p>
   
> Test với ảnh lá bình thường, cả 3 model đều có tỉ lệ cao dự đoán sai lá bình thường thành lá bị bệnh cháy lá.
   

  

* **Nhận xét chung:**
    * Nhìn chung kết quả thử nghiệm đều khá tốt. Các mô hình đều nhận diện chính xác các object chính và những object phụ, mờ, 1 góc lá trong ảnh và bệnh đi kèm từng object.  
    * Nhưng do dữ liệu còn hạn chế nên mô hình vẫn tồn tại một số lỗi như :  
      * Một số lá bình thường bị detect nhầm thành bệnh cháy lá và đốm trắng do 1 số ảnh trong tập train bệnh còn nhẹ và khá giống với lá bình thường.
      * Một số lá bị cháy lá nhưng vẫn có những đốm tròn ở thân lá làm cho model bị nhầm lẫn với bệnh đốm trắng.
      * Cả 3 mô hình đều có những trường hợp detect ra 1 phần lá bị bệnh (đối tượng không đủ từ cuốn đến chóp lá). Trường hợp này xảy ra nhiều hơn đối với model YOLOv5  và Faster R-CNN
  

   
* **Nhật xét riêng từng model:**
     * **YOLOv4:**  
       * Luôn detect chính xác cá bbox và các nhãn ứng với groundtruth. 
       * Đặc điểm của YOLOv4 là sẽ detect rất tốt những object có kích thước lớn trong ảnh. Nhưng nhũng object có kích thước nhỏ, bị che chắn, hoặc bị mờ thì không detect ra được.
        => YOLOv4 thích hợp để detect những ảnh chụp chính diện lá, kích thước object lớn và rõ nét.
   
   
   
   
<p align="center">
<img src="https://user-images.githubusercontent.com/79462324/175807266-621ffb53-200b-4064-9d02-5512d3db6977.png" style="display: block;margin-left: auto;margin-right: auto;width: 100%; height:100%;"/>
<br>
<a style="text-align: center">Hình . Kết quả test</a>
</p>
</p>

   
   
*   
     * **YOLOv5:**  
       * YOLOv5 cũng detect ra được những object chính, những object đầy đủ các thành phần như YOLOv4. Nhưng YOLOv5 detect được nhiều object hơn (bao gồm cả object bị che chắn, hay mờ nhòe)
       * Nhưng YOLOv5 vẫn còn nhầm lẫn giữ lá bình thường và lá bị bệnh cháy lá.
   
   
<p align="center">
<img src="https://user-images.githubusercontent.com/79462324/175807506-9c4ee777-1356-496f-b0ad-cccd110477cc.png" style="display: block;margin-left: auto;margin-right: auto;width: 100%; height:100%;"/>
<br>
<a style="text-align: center">Hình . Kết quả test</a>
</p>
</p>

   
   
* 
     * **Faster R-CNN:**  
       * Faster R-CNN cũng detect ra được những object chính, object đầy đủ các thành phần như YOLOv4 và YOLOv5. 
       * Faster R-CNN cũng detect được nhiều object hơn tương tự như YOLOv5 (bao gồm cả object bị che chắn, hay mờ nhòe).
       * Faster R-CNN cũng nhầm lẫn giữ lá bình thường và lá bị bệnh cháy lá.
       * Faster R-CNN hiệu quả hơn YOLOv5 ở chỗ Faster R-CNN detect ra được cả 2 bệnh trên cùng 1 lá mắc phải. Điểu mà YOLOv4 và YOLOv5 không thể.
   
<p align="center">
<img src="https://user-images.githubusercontent.com/79462324/175806323-5162834c-9b44-4202-a942-429aecfc0681.png" style="display: block;margin-left: auto;margin-right: auto;width: 100%; height:100%;"/>
<br>
<a style="text-align: center">Hình . Ví dụ về Faster R-CNN detect được nhiều object nhỏ, bị che, mờ nhòe nhiều hơn so với YOLOv4 và YOLOv5</a>
</p>
   
<p align="center">
<img src="https://user-images.githubusercontent.com/79462324/175807695-fa459fd3-9cf5-41cd-b2fd-7d5f3b06c24e.png" style="display: block;margin-left: auto;margin-right: auto;width: 100%; height:100%;"/>
<br>
<a style="text-align: center">Hình . Faster R-CNN detect ra được cả những object bị che chắn, mờ nhòe và nhầm lẫn giữ lá bình thường và lá bị bệnh cháy lá.</a>
</p>
</p>

  
<p align="center">
<img src="https://user-images.githubusercontent.com/79462324/175808049-f8eb3f66-c246-418d-a2d9-348be3355421.png" style="display: block;margin-left: auto;margin-right: auto;width: 100%; height:100%;"/>
<br>
<a style="text-align: center">Hình . Ví dụ về Faster R-CNN detect đúng cả 2 bệnh trên cùng 1 lá mắc phải (YOLOv4 và YOLOv5 không detect được)</a>
</p>
   
<a name="ungdung"></a>
# **5. HƯỚNG PHÁT TRIỂN ỨNG DỤNG VÀ CẢI TIẾN**
* **Cách cải tiến:**
    * Về dữ liệu:
        * Tăng cường sự đa dạng của dự liệu bằng cách thu thập thêm nhiều ảnh về các bệnh khác nhau, thu thập dữ liệu tại nhiều thời điểm trong ngày, thu thập dữ liệu khi cây ở nhiều thời điểm phát triển khác nhau.
        * Áp dụng thêm các kỹ thuật Data Augmentation (mosaic, blur, contrast, cutout, ...). Chọn lựa phù hợp các kỹ thuật tăng cường khác nhau để phù hợp với bộ dữ liệu.
        * Quá trình thu thập dữ liệu cũng cần kỹ càng hơn. Cần xác định đúng điều kiện ánh nhiên hay cách chụp ảnh để phù hợp với ngữ cảnh bài toán.
    * Về mô hình:
        * Áp dụng thêm nhiều pretrained model khác nhau để có thể tìm được mô hình phù hợp nhất với bài toán và bộ dữ liệu
        * Áp dụng một số kỹ thuật như thay đổi cấu trúc mô hình, tùy chỉnh tham số để có thể cải thiện mô hình hơn
* **Hướng phát triển:**
    * Hướng tới việc phát hiện các loại bệnh trên nhiều loại lá cây trồng khác nhau dựa trên các đặc điểm giống nhau của các loại bệnh khi xuất hiện trên lá.
   
<a name="thamkhao"></a>
# **6. NGUỒN THAM KHẢO**
[1] Alexey Bochkovskiy, Chien-Yao Wang, Hong-Yuan Mark Liao, In YOLOv4: Optimal Speed and Accuracy of Object Detection. arXiv:2004.10934, 2020

[2] Shaoqing Ren, Kaiming He, Ross Girshick, and Jian Sun, In Faster R-CNN: Towards Real-Time Object Detection with Region Proposal Networks. arXiv:1506.01497, 2016

[3] Alexey. 2021. darknet. GitHub; [2022]. https://github.com/AlexeyAB/darknet

[4] Jacob Solawetz. "How to Train Detectron2 on Custom Object Detection Data", roboflow, https://blog.roboflow.com/how-to-train-detectron2/. [2022]
   
[5] Roboflow. 2021. yolov5-custom-training-tutorial. GitHub; [2022] https://github.com/roboflow-ai/yolov5-custom-training-tutorial

[6] Agridrone. "Bệnh cháy lá sầu riêng nguyên nhân và cách phòng trừ". Adgidrone. [2022]
   
[7] Agridrone. "Bệnh đốm lá trên cây sầu riêng". Adgidrone. [2022]
   
[8] Ultralytics. 2022. yolov5. GitHub. https://github.com/ultralytics/yolov5 [2022]

[9] Roboflow. https://roboflow.com/ 
   
[10] Meta Research. 2021. detectron2. GitHub; [2022]. https://github.com/facebookresearch/detectron2
   
[11] Aqeel Anwar. "What is Average Precision in Object Detection & Localization Algorithms and how to calculate it?", towardsdatascience, https://towardsdatascience.com/what-is-average-precision-in-object-detection-localization-algorithms-and-how-to-calculate-it-3f330efe697b. [2022]
