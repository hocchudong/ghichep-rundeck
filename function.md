#Một số điều cần chú ý :

* Scheduler

- Option (chưa làm rõ)
- Làm việc theo Workflow ( If a step fails: Stop at the failed step. Run remaining steps before failing. )
  + command
  + Script
  + Job reference
- Node
  + Locally
  + Patch
- If a node fails
  + Fail the step without running on any remaining nodes.
  + Continue running on any remaining nodes before failing the step.
- Send Notification?
  + Success
  + Fail
  + On start
- Schedule to run repeatedly?
  + Thời gian (giờ phút)
  + Ngày tháng.
- Scheduler có bảng liệt kê 

![function](/image/function.png)
