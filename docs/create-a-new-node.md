#Tạo node trên Rundeck

```sh
Cách add thêm node tỏng Rundeck
```

- Trong Rundeck Project sẽ chứa các node được quản lý, mỗi project sẽ chứa một, một số node cần quản lý . bây giờ chúng ta tiến hành thực hiện thêm 1 node vào
một project nào đó.

- Trước tiên chọn vào project mà chúng ta muốn thêm node :

![scr1](http://i.imgur.com/VwQNCz4.png)

- Chọn `config` :

![scr2](http://i.imgur.com/xeaP85K.png)

- Ở đây chúng ta thấy được đường dẫn của file cấu hình :

![scr3](http://i.imgur.com/WU4tkFb.png)

- Mở file cấu hình với trình soạn thảo `vi` :

```sh
vi  /var/rundeck/projects/datpt/etc/resources.xml
```

- Sau đó chúng ta thêm một đoạn cấu hình thêm 1 node mới như sau :

```sh

  <node name="datpt"
        tags="datpt"
        osFamily="unix"
        hostname="10.10.10.20"
        username="root"
        ssh-keypath="/var/lib/rundeck/datpt.key"
  />
```

- File hoàn chỉnh sẽ như sau :

```sh
<?xml version="1.0" encoding="UTF-8"?>

<project>
  <node name="localhost" description="Rundeck server node" tags="" hostname="localhost" osArch="amd64" osFamily="unix" osName="Linux" osVersion="3.19.0-25-generic" username="rundeck"/>
  <node name="datpt"
        tags="datpt"
        osFamily="unix"
        hostname="10.10.10.20"
        username="root"
        ssh-keypath="/var/lib/rundeck/datpt.key"

/>
</project>

```

- Lưu lại file cấu hình và kiểm tra xem đã có node mà mình thêm vào chưa :

![scr4](http://i.imgur.com/9sZmbVS.png)

```sh
- Ở đây có 2 node , 1 node là localhost còn node kia là chúng ta vừa mới thêm.
```

- Như thế là đã xong bước thêm node, bước tiếp theo chúng ta cần cấu hình để Rundeck có thể remote được node đó.

- Tại client `10.10.10.20` chúng ta tạo ssh-keygen :

```sh
ssh-keygen -t rsa -b 4096
```

- Chuyển đến thư mục chứa key rồi thực hiện như sau:

```sh
cd /root/.ssh
cat id_rsa.pub > authorized_keys
chmod g-w authorized_keys
```

- Sau đó chúng ta coppy nội dung của file `id_rsa` vào ssh-keypath lúc nãy chúng ta cấu hình ở node , ở đây là `/var/lib/rundeck/datpt.key`

- Thế là chúng ta đã hoàn tất việc thêm 1 node để remote, bây giờ chúng ta kiểm tra xem thế nào :

Vào node : 

![scr5](http://i.imgur.com/A7nz1He.png)

Ấn vào dấu mũi tên để lọc riêng node đó ra :

![scr6](http://i.imgur.com/fMCfRya.png)

- Nhấn vào node để xem chi tiết cấu hình :

![scr7](http://i.imgur.com/TAG0Rt5.png)

Chọn `Action` rồi chọn `Run a command a 1 node` để kiểm tra xem chúng ta đã remote được hay chưa?

![scr8](http://i.imgur.com/smadMeo.png)

Điền lệnh muốn dùng để test, chọn `Run on 1 node` và xem kết quả :

![scr9](http://i.imgur.com/1mE9Asf.png)

#OK !!!

- Với cách tương tự như thế chúng ta có thể thêm nhiều hơn 1 node vào project này và tiến hành quản lý cấu hình cũng như các cong việc khác để tận dụng chức năng của Rundeck.

