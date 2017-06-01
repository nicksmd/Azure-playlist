Rất nhiều người nói về việc bắt đầu sử dụng Azure nhưng thực sự không biết bắt đầu từ đâu.
Họ nghĩ rằng Azure "chỉ là những máy ảo (VM) được dựng lên trên các data center sở hữu bởi MS"
. Tuy nhiên, Azure cung cấp nhiều dịch vụ hơn thế:


![](http://robertgreiner.com/uploads/images/2014/AzureServicesOverview.png)

##### 1. IaaS (Infrastructure as a Service): Virtual Machines
Một máy chủ trên cloud. Bạn có toàn quyền kiểm soát máy chủ này.
Nếu nhu cầu của bạn là tùy biến nhiều ứng dụng 3rd party và
chạy nhiều app trên cùng 1 server thì IaaS là lựa chọn phù hợp.
Dịch vụ này tương tự như VM của DigitalOcean hay Heroku.

##### 2. PaaS (Platform as a Service): Web app
Tương tự như IaaS, MS cung cấp cho bạn 1 VM. Điểm khác biệt là bạn không cần
maintain VM này mà chỉ cần tập trung vào phát triển phần mềm sau đó deploy
lên (thông qua Git, TFS, hay Visual Studio...) => ưu thế là No Downtime, No VM management.
Nghĩa là không còn lo server bỗng dưng lăn đùng ra chết, không lo bị hack, không
cần tối ưu RAM, CPUs, disk sao cho server chạy mượt nhất.

Nhược điểm chết người của PaaS:
* Không thể truy cập VM từ xa như IaaS
* Việc sử dụng 3rd party software bị giới hạn (gần như bất khả thi)
* Migrate 1 ứng dụng sẵn có lên PaaS hêt sức nhức đầu và lắm bug trong khi
việc một Migrate back 1 ưng dụng xây dựng trên PaaS trở lại 1 ứng dụng
truyền thống cho IaaS cũng nhức não không kém :(.

Một ví dụ đơn giản tôi từng trải qua khi phải phát triển 1 chức năng hết sức
đơn giản (trong 1 hệ thống lớn, đã được deploy lên AZ webapp): convert PDF to
PNG. Vấn đề bắt đầu phức tạp lên khi ta không thể thực hiện điều này mà không sử dụng
các 3rd party lib như GhostScript hay Imagemagick => không thể tích hợp vào hệ thống
sẵn có trên Azure PaaS. Một bài toán đơn giản trở nên hết sức nhức não với
sự giới hạn của Azure PaaS.

**Tại sao Azure PaaS lại giới hạn không cho cài đặt các 3rd party lib?**
* Vấn đề security, bởi vì Azure PaaS chịu trách nhiệm hoàn toàn việc maintain và
bảo mật server nên nó cần giới hạn cài đặt các ứng dụng của bên thứ 3.
* Để đảm bảo không có sự xung đột, chồng chéo sử dụng resource giữa các webapp
trên cùng một máy chủ.

Xem thêm về giơi hạn của PaaS tại [đây](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox)
##### 3. SaaS (Software as a Service): Basecamp, SalfForce, Office 365..:
Các ứng dụng có sẵn được tạo ra bởi các hãng và host lên Cloud, bạn
sử dụng bằng cách subscribe.

##### 4. Serverless Computing: Azure Function
Một bậc tiến hóa mới của PaaS, được MS ra mắt cuối năm 2016. Khác với cái tên
**Serverless**, thực sự vẫn có 1 server, vấn đề là bạn không cần quan tâm đến nó.
Nghe chả khác gì PaaS, điểm khác bọt là gì?
- Với PaaS, bạn có code, commit lên 1 GIT repo, sau đó deploy lên web app.
Nhưng bạn vẫn phải quan tâm đến server.
- Với Serverless, bạn upload code lên và nó chạy luôn. Code được kích hoạt thông
qua http (URL) hoặc 1 trigger event. Hết sức nhanh chóng và đặc biệt bạn có thể
sử dụng các 3rd party app, điều (gần như) bất khả thi ở PaaS.

Nhược điểm của Azure Function là quá trình dev vẫn chưa được hỗ trợ trên IDE mà
phải dev trực tiếp trên azure portal interface.

