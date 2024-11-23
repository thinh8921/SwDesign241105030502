## Bài thực hành Lab4.md  
### Thiết kế các ca sử dụng cho hệ thống "Payroll System" và giải thích lý do  
**1.Use case Login**    
**Mô tả chi tiết**  
Chức năng: Xác thực thông tin đăng nhập của người dùng.  
Mục tiêu: Xác thực thông tin đăng nhập của người dùng để đảm bảo quyền truy cập hợp lệ vào hệ thống, bảo vệ dữ liệu và điều hướng người dùng đến giao diện chính.  
Tác nhân: Any User (Nhân viên/Quản lý/Quản trị viên).  
Luồng sự kiện:  
1. Người dùng truy cập màn hình đăng nhập.  
2. Người dùng nhập thông tin đăng nhập (username và password).  
3. Hệ thống kiểm tra thông tin:  
3a. Nếu hợp lệ: Hệ thống chuyển người dùng đến dashboard.  
3b. Nếu không hợp lệ: Hệ thống thông báo lỗi.  

Lý do thiết kế:  
- Xác thực người dùng: Đảm bảo chỉ những người dùng hợp lệ (Nhân viên, Quản lý, Quản trị viên) mới có thể truy cập hệ thống.  
- Bảo vệ dữ liệu: Ngăn chặn truy cập trái phép, đảm bảo tính bảo mật cho dữ liệu hệ thống.  
- Truy cập chức năng hệ thống: Là bước đầu tiên để người dùng được phép sử dụng các tính năng khác của hệ thống.  
- Trải nghiệm người dùng: Thông báo lỗi khi thông tin không hợp lệ giúp hướng dẫn người dùng nhập lại đúng cách.  
- Tăng cường bảo mật: Giới hạn quyền truy cập dựa trên vai trò của người dùng (Nhân viên, Quản lý, Quản trị viên).  

**Sơ đồ Use case**  
Code:
```  
@startuml
actor "Any User" as User
usecase "Login" as UC1
User --> UC1 : Access Login
@enduml
```  
Link sơ đồ:  https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bTYSab-aOAIOrwbGcXnQf6IGc8ncC5LMfoQd5YSgg3aav-UcGSHTpRa0iafwEhQWJWALWgEoScfnSKAO3LS3gbvAK0p0G000F__0m00

Sơ đồ:  
![Diagram](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bTYSab-aOAIOrwbGcXnQf6IGc8ncC5LMfoQd5YSgg3aav-UcGSHTpRa0iafwEhQWJWALWgEoScfnSKAO3LS3gbvAK0p0G000F__0m00)  
  
**2. Use case Maintain Timecard**  
**Mô tả chi tiết**   
Chức năng: Quản lý, chỉnh sửa, và lưu trữ thẻ chấm công.  
Mục tiêu: Quản lý, chỉnh sửa và lưu trữ thông tin thẻ chấm công, đồng thời hỗ trợ xác minh dữ liệu để đảm bảo tính chính xác và minh bạch trong việc ghi nhận thời gian làm việc.  
Tác nhân:  
- Nhân viên: Trực tiếp thao tác trên thẻ chấm công.  
- Quản lý dự án: Có thể xem và xác minh dữ liệu (nếu cần).  

Luồng sự kiện:  
1. Người dùng khởi động quy trình Maintain Timecard  
Người dùng chọn chức năng "Quản lý thẻ chấm công" trên giao diện (TimecardForm).  
Hệ thống chuyển yêu cầu đến TimecardController.  
2. Lấy dữ liệu thẻ chấm công  
TimecardController kiểm tra thẻ chấm công hiện tại thông qua đối tượng Timecard.  
Nếu thẻ chưa tồn tại, một thẻ mới sẽ được tạo.  
Dữ liệu được lấy từ cơ sở dữ liệu (ProjectManagementDatabase).  
3. Hiển thị thẻ chấm công  
TimecardController gửi dữ liệu về giao diện (TimecardForm).  
Người dùng có thể xem và chỉnh sửa thông tin.  
4. Cập nhật thẻ chấm công  
Người dùng nhập giờ làm việc hoặc mã charge code (charge numbers).  
Thông tin được gửi lại TimecardController để cập nhật dữ liệu.  
5. Lưu thẻ chấm công  
Sau khi chỉnh sửa xong, người dùng chọn "Lưu thẻ chấm công".  
TimecardController lưu dữ liệu vào cơ sở dữ liệu thông qua ProjectManagementDatabase.  

Lý do thiết kế:  
- Quản lý thời gian làm việc hiệu quả:  
Cho phép người dùng dễ dàng nhập và chỉnh sửa dữ liệu về giờ làm việc hoặc mã charge code.  
Đảm bảo dữ liệu được ghi nhận chính xác và đầy đủ.  
- Tính minh bạch và chính xác: Giúp theo dõi thời gian làm việc minh bạch, hỗ trợ tính lương đúng quy trình và giảm sai sót trong việc quản lý.  
- Tăng tính tự động hóa:  
Hệ thống tự động kiểm tra và tạo thẻ chấm công nếu chưa tồn tại.  
Tự động hiển thị dữ liệu từ cơ sở dữ liệu, giảm sai sót thủ công.  
- Hỗ trợ quản lý: Quản lý dự án có thể xem và xác minh dữ liệu thẻ chấm công, đảm bảo tính hợp lệ của thông tin.  
- Khả năng mở rộng: Thiết kế dựa trên các đối tượng như Timecard và Database, dễ dàng tích hợp hoặc mở rộng thêm tính năng trong tương lai.  
- Tối ưu hóa quy trình: Giảm thời gian xử lý và tăng hiệu quả nhờ hệ thống hóa các bước quản lý dữ liệu chấm công.  

**Sơ đồ Use case**  
Code:
```  
@startuml
actor "Employee" as Employee
actor "Project Manager" as Manager
usecase "Maintain Timecard" as UC2
Employee --> UC2 : Manage Timecard
Manager --> UC2 : Verify Timecard
@enduml
```  
Link sơ đồ:  https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bTYSab-aOAIQsv1JdvbQggIGcAn0em3ammeoizAJIvHy4tCIqnFBGAhWRAvIejJanEBKnMKV1Cpyqg0M24aCnSeL9G2LXRgRCG5Cqv1LzSE9A1W1TKDLye5DGr9HLXgKMPQ9KA5GsfU2j2z00000F__0m00

Sơ đồ:  
![Diagram](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bTYSab-aOAIQsv1JdvbQggIGcAn0em3ammeoizAJIvHy4tCIqnFBGAhWRAvIejJanEBKnMKV1Cpyqg0M24aCnSeL9G2LXRgRCG5Cqv1LzSE9A1W1TKDLye5DGr9HLXgKMPQ9KA5GsfU2j2z00000F__0m00)  
  
**3. Usse case Run Payroll**  
**Mô tả chi tiết**   
Chức năng: Tính lương và thực hiện thanh toán cho nhân viên.  
Mục tiêu: Tự động hóa quy trình tính lương, đảm bảo thanh toán đúng hạn và chính xác thông qua các phương thức thanh toán linh hoạt.  
Tác nhân:  
- System Clock: Tự động khởi động quy trình tính lương vào ngày trả lương.  
- Bank System: Hỗ trợ xử lý giao dịch chuyển khoản.  
- rinter: In bảng lương hoặc paycheck. Report.     

Luồng sự kiện:  
1. Khởi động quy trì
SystemClockInterface kiểm tra ngày hiện tại có phải ngày trả lương không.  
Nếu đúng, kích hoạt quy trình tính lương (PayrollController.runPayroll()).  
2. Lấy dữ liệu lương  
PayrollController:  
- Lấy dữ liệu thẻ chấm công (getTimecard()).  
- Lấy các đơn đặt hàng (Purchase Orders) với nhân viên làm việc theo hoa hồng.  
3. Tính toán lương  
Tính toán tổng lương cho từng nhân viên, dựa trên:  
- Giờ làm việc trên thẻ chấm công.  
- Hoa hồng từ đơn đặt hàng.  
- Các khoản phụ cấp và khấu trừ.  
4. Xác định phương thức thanh toán  
PayrollController kiểm tra phương thức thanh toán của từng nhân viên:  
- Chuyển khoản: Gửi thông tin thanh toán đến BankSystem.  
- Paycheck (nhận trực tiếp): Tạo bảng lương và in qua Printer.  
5. Thực hiện thanh toán  
Gửi lệnh thanh toán đến ngân hàng (nếu là chuyển khoản).  
In paycheck và phân phối (nếu là nhận trực tiếp).  

Lý do thiết kế  
- Tự động hóa quy trình: Hệ thống tự động thực hiện tính toán và chi trả lương vào ngày trả lương, giảm thiểu sai sót và tiết kiệm thời gian.  
- Tính chính xác: Dựa trên dữ liệu thẻ chấm công, đơn hàng hoa hồng, phụ cấp và khấu trừ để đảm bảo lương được tính đúng cho từng nhân viên.  
- Đáp ứng linh hoạt: Hỗ trợ nhiều phương thức thanh toán (chuyển khoản hoặc nhận paycheck), phù hợp với nhu cầu của nhân viên.  
- Tích hợp hệ thống: Liên kết với Bank System để xử lý giao dịch và Printer để in paycheck, đảm bảo quy trình tính lương liền mạch.  
- Bảo mật: Quy trình xử lý dữ liệu nhạy cảm như lương và giao dịch ngân hàng đảm bảo sự an toàn, hạn chế sai phạm.  
- Hỗ trợ quản lý: Tạo báo cáo hoặc paycheck giúp quản lý minh bạch trong việc trả lương.  

**Sơ đồ Use case**  
Code:
```  
@startuml
actor "System Clock" as SystemClock
actor "Bank System" as BankSystem
actor "Printer" as Printer
usecase "Run Payroll" as UC3
SystemClock --> UC3 : Start Payroll Process
BankSystem --> UC3 : Process Payment
Printer --> UC3 : Print Paycheck
@enduml
```  
Link sơ đồ:  https://www.planttext.com/api/plantuml/png/L8yz3i8m38NtdCBgtecD0LNq0XKL1x229L3p8yNEqBCnz4XSWIHDHDdytllaPt_Usy22GQ8r2hNu0Dsyif25qNYzT80Ckr5qOwxebkeN9EjTDc8ABoSKIbfd5PaqCa5tYmucN8CtfW3tyQGEBT3tb-p16UPyN6FJ8g-9MVtg3cWDCsp9YQgjVqHoSgwVb7uPo3tItry0003__mC0  

Sơ đồ:  
![Diagram](https://www.planttext.com/api/plantuml/png/L8yz3i8m38NtdCBgtecD0LNq0XKL1x229L3p8yNEqBCnz4XSWIHDHDdytllaPt_Usy22GQ8r2hNu0Dsyif25qNYzT80Ckr5qOwxebkeN9EjTDc8ABoSKIbfd5PaqCa5tYmucN8CtfW3tyQGEBT3tb-p16UPyN6FJ8g-9MVtg3cWDCsp9YQgjVqHoSgwVb7uPo3tItry0003__mC0)  
  
**Sơ đồ Use case chung**  
Code:
```  
@startuml
actor "Any User" as User
actor "Employee" as Employee
actor "Project Manager" as Manager
actor "System Clock" as SystemClock
actor "Bank System" as BankSystem
actor "Printer" as Printer

usecase "Login" as UC1
usecase "Maintain Timecard" as UC2
usecase "Run Payroll" as UC3

User --> UC1 : Access Login
Employee --> UC2 : Manage Timecard
Manager --> UC2 : Verify Timecard
SystemClock --> UC3 : Start Payroll Process
BankSystem --> UC3 : Process Payment
Printer --> UC3 : Print Paycheck

@enduml
```  
Link sơ đồ:  https://www.planttext.com/api/plantuml/png/L94zJWCn48NxESLe-nGa7GLAYEY8516W7pb3ME8VP7iBdus28t45REyOByLAC-zzw_4y_tnzRqCa7oUZWLHq7eUTJVWIs0z8eHRDU32VsYNcQhIccKVlFbX5F92bY_miTKDEAKGskDTENQi_2xLlp3tPg-WLAVtSza6ZZJ90Qe0fiAB0E3owosZdc-zlkdoW3EOFdqUJ9NyMPDsHfydYaP9tMekv0IZhusfrLqx3MzmfnI5W7G8j0V7NsPyN_Xi24i22U6K_lgLEB28GQfEfKtcITfkyfIjZeMUnGCKii64RGIBvHsIb-EgTSz2mPNikp_qB003__mC0 

Sơ đồ:  
![Diagram](https://www.planttext.com/api/plantuml/png/L94zJWCn48NxESLe-nGa7GLAYEY8516W7pb3ME8VP7iBdus28t45REyOByLAC-zzw_4y_tnzRqCa7oUZWLHq7eUTJVWIs0z8eHRDU32VsYNcQhIccKVlFbX5F92bY_miTKDEAKGskDTENQi_2xLlp3tPg-WLAVtSza6ZZJ90Qe0fiAB0E3owosZdc-zlkdoW3EOFdqUJ9NyMPDsHfydYaP9tMekv0IZhusfrLqx3MzmfnI5W7G8j0V7NsPyN_Xi24i22U6K_lgLEB28GQfEfKtcITfkyfIjZeMUnGCKii64RGIBvHsIb-EgTSz2mPNikp_qB003__mC0)  
  
  Tham khảo website: https://www.planttext.com/

