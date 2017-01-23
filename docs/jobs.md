#Jobs trong Rundeck.

- Jobs cung cấp một phương tiện để đóng gói một quá trình. Một Job bao gồm một cấu hình đại diện cho một tùy chọn đầu vào, 
các bước tiến hành, một biểu thức lọc phù hợp với các node ở những bước sẽ thực thi, và các thông số 
kiểm soát thực thi mà chỉ định nếu các bước đang chạy song song và làm những gì xử lý như thế nào nếu một lỗi xảy ra trong một các bước.

- Rundeck cho phép bạn tổ chức và thực hiện job và quan sát sự tiến bộ của các job đang đang chạy. Bạn có thể xem danh 
sách những job hiện đang chạy hoặc xem kết quả của các bước thực hiện cá nhân, job cũng có thể được hủy bỏ nếu chúng cần phải được dừng lại.

- Mỗi thực hiện công việc được lưu trữ và chứa thông tin về các node ở bước thực hiện, thành công và thời gian của mỗi bước. 
Sản lượng thực hiện công việc có thể được tải về, chuyển tiếp đến một store ghi bên ngoài hoặc gửi một thông báo qua email, IRC, webhook,.....

- Dưới đây là chi tiết về các tạo job và thông qua một số chức năng .

##Tạo job trên Rundeck.

- Nhấn vào `job` trên thanh chức năng trên web interface Rundeck.

![scr1](/image/Screenshot_1.png)

- Chọn `Create new job`

![scr2](/image/Screenshot_2.png)

- Đặt tên cho job:

![scr3](/image/Screenshot_3.png)

- Chọn cách thức thực thi của job:

```sh
Ở đây chúng ta có thể thấy được 2 lựa chọn , chúng ta có thể tùy chọn tùy theo mục đích sử dụng :
  + Stop at the failed step.
  + Run remaining steps before failing.
```

![scr4](/image/Screenshot_4.png)

- Tiếp theo chúng ta sẽ đến phần `Add a step`

```sh
Tại đây chúng ta sẽ tạo ra các công việc mà chúng ta muốn các remote host phải thực hiện , chúng ta có thể lựa chọn các step đó 
là một hoặc nhiều command, script,....
```

![scr5](/image/Screenshot_5.png)

- Ở đây sẽ ví dụ 1 step là 1 command , mỗi step đều có 1 label , điều này rất có ích vì khi thực thi thì sẽ được lưu lại tất cả lịch sử thực thi, 
do đó khi có label thì khi chúng ta cần check lại các công việc và các step trong công việc đó sẽ dễ dàng hơn, và quản lý cũng có nhiều tiện ích hơn :

![scr6](/image/Screenshot_6.png)

- Ỏ phần node chúng ta chọn `Dispatch to Nodes` để chọn node khác , điền tên node và add vào :

![scr7](/image/Screenshot_7.png)

- Phần `Send Notification?`

```sh
Rundeck cung cấp cho chúng ta một chức năng giúp có thể thông báo các hoạt động của các node đang được quản lý bởi Rundeck web interface, Rundeck cung cấp 
cho chúng ta các phương tiện như mail hoặc webhook.
```

- Ví dụ về một config notification :

![scr8](/image/Screenshot_8.png)

- Tùy chọn `Schedule to run repeatedly? `

```sh
Rundeck cung cấp cho chúng ta một chức năng có thể lập lịch thực thi các công việc, điều hạn chế ở đây là chúng ta không thể chỉ định một ngày trong năm hay bất cứ 
một tùy chọn nào khác mạnh hơn (có thể được cải thiện ở bản tiếp theo - đã có task nâng cấp về scheduler tại trello của nhóm). Thời điểm hiện tại chúng ta chỉ có thể thiết lập 
everyday, every month hoặc các ngày trong tuần, hoặc các ngày trong tháng, sau mỗi tháng chúng ta lại phải thiết lập lại - đây là một điểm khá bất tiện.
```

![scr9](/image/Screenshot_9.png)

- Trên là những chức năng có tác dụng có tốt mà Rundeck cung cấp cho chúng ta , sau khi đã thiết lập hết các tùy chọn chúng ta nhấn vào `Create` để tạo job :

![scr10](/image/Screenshot_10.png)

- Hết = > Bài viết còn sơ sài , mong nhận được đóng góp từ các bạn !!!
