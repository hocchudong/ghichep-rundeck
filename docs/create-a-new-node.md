#Cách tạo một node mới với Rundeck.

- Để tạo một node mới chúng ta cần tạo một project mới :

![scr4]()

- Chúng ta ấn vào `New Project` và tiến hành đặt tên cho Project đó :

- Trở lại trang chủ để xem danh sách các Project :

![scr5]()

- Ấn vào config (NÚt hình bánh răng phía trê màn hình bên phải ) chúng ta sẽ thấy được đường dẫn file cấu hình :

![scr6]()

- Dùng trình soạn thảo vi chỉnh sửa file  `/var/rundeck/projects/Test-Project/etc/resources.xml` 

- Khai báo nội dung của node mới bằng những tùy chọn cấu hình như sau :

```sh
  <node name="datpt"
        tags="Create_a_new_node"
        osFamily="unix"
        username="datpt"
        hostname="26.26.26.11"
        ssh-keypath="/var/lib/rundeck/datpt.key"
  />
```

#### Lưu ý : thẻ <node/> phải nằm bên trong thẻ <project><project/>

- Ví dụ về 1 file cấu hình hoàn chỉnh gồm 2 node như sau :

```sh
<?xml version="1.0" encoding="UTF-8"?>

<project>
  <node name="localhost" description="Rundeck server node" tags="" hostname="localhost" osArch="amd64" osFamily="unix" osName="Linux" osVersion="3.13.0-106-generic" username="rundeck"/>
  <node name="datpt"
        tags="Create_a_new_node"
        osFamily="unix"
        username="datpt"
        hostname="26.26.26.11"
        ssh-keypath="/var/lib/rundeck/datpt.key"
  />

</project>
```

- Sau đó chúng ta khởi động lại dịch vụ :

```sh
service rundeckd restart 
```

- Truy cập lại vào web interface của Rundeck và kiểm tra lại kết quả :

![scr7]()

Updating ....