# icinga2 cơ bản (Cấu hình trên CentOS 7)

### Thêm host muốn giám sát bằng Wizard

#### 1. Cấu hình trên icinga2

Sử dụng Wizard bằng câu lệnh:

```
icinga2 node wizard
```
<img src="http://image.prntscr.com/image/d40e8e726db9435e85c6a9ffed4d9ac3.png">

Khởi động lại icinga2

```
systemctl restart icinga2
```

Tạo Ticket cho host muốn giám sát:

```
icinga2 pki ticket --cn "Windows-7-Demo"
```

<img src="http://image.prntscr.com/image/1f5d3b2b69314194b682c6705a247908.png">


**Chú ý:** **"Windows-7-Demo"**: là tên của host muốn giám sát, có thể đặt tự do nhưng khi cấu hình agent trên host đó phải điền đúng tên và ticket

#### 2. Cấu hình trên host (Windows 7)

##### 2.1 Tải Agent cho Windows

https://packages.icinga.org/windows/

##### 2.2 Cài đặt Agent

Bấm **Next** để chuyển sang bước tiếp theo

<img src="http://image.prntscr.com/image/d1b7bd5cd5a84683bf1c1fc09631cf08.png">

Bấm **I agree** để Đồng ý với các Lisence của icinga2

<img src="http://image.prntscr.com/image/510e0f572d25414cb00c3eceeb4ccfa0.png">

Bấm **Next** để tiếp tục

<img src="http://image.prntscr.com/image/510e0f572d25414cb00c3eceeb4ccfa0.png">

Bấm **Install** để cài đặt

<img src="http://image.prntscr.com/image/54917a17aa534da3a4df14e2eddfc3d7.png">

Chờ khoảng 1 phút để quá trình cài đặt diễn ra.

Bấm **Finish** để khởi động Agent

<img src="http://image.prntscr.com/image/7a528858d5334d418df59e49c2221ec5.png">

Bấm vào **Reconfigure** để cấu hình

<img src="http://image.prntscr.com/image/24305faaada647468d6e58e7a8610f35.png">

Sau đó, icinga2 agent sẽ hiện ra 1 bảng để chúng ta điền các thông tin cấu hình:

<img src="http://image.prntscr.com/image/a45ccf561f3c49eb8ae4c5e5c9f606e5.png">

Làm tiếp tục như hình

<img src="http://image.prntscr.com/image/cd3e800aaa004d82be451d3130e50e77.png">

Bấm **Next** để tiếp tục

<img src="http://image.prntscr.com/image/edf9844830e04758bf872a4e6d565093.png">

Chờ một chút cho agent hoạt động và khởi chạy Service trên host. Bấm **Finish** để hoàn tất quá trình.

<img src="http://image.prntscr.com/image/e8b8215c79bb4e4a946caf95926c4d31.png">

#### 2. Giám sát host trên icinga2

Khởi động lại dịch vụ và update các node

```
systemctl restart icinga2
icinga2 node update-config
```
<img src="http://image.prntscr.com/image/ae04725c908644e09c99ccb0516c866c.png">

Liệt kê các node đang giám sát

```
icinga2 node list
```

<img src="http://image.prntscr.com/image/c787f0da70324d45a14112bc6356c8a3.png">

#### 3. Giám sát trên Web

Truy cập vào IP hoặc FQDN của icinga

`http://youricinga2.com/icingaweb2`

<img src="http://image.prntscr.com/image/ff41b50d159b4da780ed1166a4cb3ff4.png">

Click vào **Tab Overviews > Hosts**

<img src="http://image.prntscr.com/image/e33913525d3c4340b255399d8ac1c4ff.png">

Chọn host **Windows-7-Demo**

Chúng ta sẽ kiểm tra dịch vụ như DISK, LOAD, PROC,..

<img src="http://image.prntscr.com/image/0f479276da6c4d70ae4cb119cefcff1c.png">
