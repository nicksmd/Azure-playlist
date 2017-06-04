
Azure cung cấp 3 sản phẩm load balance khác nhau tùy vào mục đích sử dụng.

#### 1.Traffic manager

![](https://azure.microsoft.com/svghandler/traffic-manager/?width=600&height=315)

Tiếp nhận và phân phối incoming request ở tầng DNS.
Chức năng chính: nếu bạn có server được host ở các địa điểm khác nhau (trên
nhiều châu lục khác nhau) và muốn khách hàng trải nghiệm đỗ trễ thấp nhất,
Traffic manager là giải pháp.

#### 2. Application gateway

<img src="https://github.com/nicksmd/Azure-playlist/blob/master/Azure-Application-Gateway.png?raw=true" width="320" height="320">

Tiếp nhận và phân phối incoming request ở tầng 7 OSI, tức dựa vào
thông tin chứa trong tầng Application để quyết định phân phối request.
Hoạt động như
một reverse proxy service.

Chức năng chính: phù hợp để sử dụng nếu bạn muốn phân phối request dựa trên
ứng dụng: ví dụ dựa trên cấu trúc URL, cookie, session.

#### 3. Load balancer

![](https://azure.microsoft.com/svghandler/load-balancer/?width=600&height=315)

Tiếp nhận và phân phối incoming request ở tầng 4 OSI (tầng Transport).
Tức dựa vào IP của nguồn và đích, port trong package header mà không dựa vào content bên trong packet.
Chỉ hoạt động với các thực thể thuộc cùng 1 azure data center.

**Ví dụ**
Cần xây dựng 1 website phục vụ 2 loại dữ liệu: video và các webpage. Các server
cuẩ hệ thống phải được host ở nhiều địa điểm khác nhau trên thế giới để
đảm bảo khi 1 server sập thì hệ thống vẫn tiếp tục hoạt động cũng như độ trễ đến
khách hàng trên toàn thế giới là nhỏ nhất. Các developer quyết định tất cả các
URL có pattern /video/* sẽ được phục vụ bởi 1 nhóm các server riêng biệt.
Điều này sẽ tăng tính mở rộng độc lập (independent scalability).

Ngoài ra, các server phục vụ nội dung webpages sẽ giao tiếp với 1 nhóm nhiều
server có chức năng là database.

Sử dụng đồng thời Traffic Manager, Application Gateway và Load Balancer, ta có
thể xây dựng hệ thống trên như sau:

![](https://docs.microsoft.com/en-us/azure/traffic-manager/media/traffic-manager-load-balancing-azure/scenario-diagram.png)

* **Traffic Manager** được sử dụng để phân phối request từ user đến các server gần họ nhất.
* **Application Gateway** được dùng để phân phối request dựa trên URL patter, các URL có dạng
/video/* sẽ được chuyển đến server chưa video.
* **Load Balancer** sẽ phân phối request đến các database riêng biệt trong cùng 1 data center.




