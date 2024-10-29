# Lab 1 - PHÂN TÍCH KIẾN TRÚC, CƠ CHẾ, CA SỬ DỤNG

## 1. Phân tích kiến trúc

### 1.1. Đề xuất Kiến trúc

#### 1.1.1 Kiến trúc Tổng thể
- **Client-Server Architecture**: Sử dụng mô hình kiến trúc client-server để phân tách các yêu cầu của người dùng và các dịch vụ xử lý dữ liệu. Nhân viên sẽ sử dụng ứng dụng trên máy tính để bàn để gửi thông tin, và hệ thống sẽ xử lý dữ liệu trên máy chủ.

#### 1.1.2 Thành phần Kiến trúc

- **Client Layer**:
  - *Windows Desktop Application*: Giao diện cho nhân viên nhập thông tin như thời gian làm việc, đơn hàng, và tùy chọn thanh toán. Giao diện thân thiện và dễ sử dụng.
  - *Reporting Module*: Cung cấp khả năng truy vấn và tạo báo cáo cho nhân viên về giờ làm việc, số tiền đã nhận, và thời gian nghỉ còn lại.

- **Business Logic Layer**:
  - *Payroll Processing Engine*: Chịu trách nhiệm tính toán tiền lương, xử lý các yêu cầu của nhân viên và tạo báo cáo. Đảm bảo rằng lương được thanh toán chính xác và đúng hạn.
  - *Timecard Management*: Quản lý việc ghi nhận thời gian làm việc của nhân viên, kiểm tra tính hợp lệ và lưu trữ dữ liệu.
  - *Commission Calculation*: Tính toán hoa hồng cho nhân viên có lương cơ bản.

- **Data Access Layer**:
  - *Employee Database*: Cơ sở dữ liệu chứa thông tin nhân viên, giờ làm việc, và đơn hàng. Cung cấp chức năng thêm, xóa và sửa thông tin nhân viên.
  - *Project Management Database (DB2)*: Kết nối tới cơ sở dữ liệu hiện tại để lấy thông tin về dự án và charge numbers mà không cập nhật dữ liệu.

- **Integration Layer**:
  - *Payment Processing Module*: Tích hợp với các phương thức thanh toán như chuyển khoản ngân hàng và gửi thư. Đảm bảo rằng thanh toán được thực hiện đúng phương thức mà nhân viên chọn.

### 1.2. Biểu đồ Package
![Diagram](https://www.planttext.com/api/plantuml/png/X99BQiCm48RtFiMGVQvGaZfP5188eT15o68g3qADf16IJ36X9-kYH-eLAZzArTQnjPt_CVEXp_UFLOZeOsrquL1SK18iIgt8HjXXGtu1rmBIEpqfM_5hW0s5IsG7Q-Uq4XWLstElE99Z7vMLiEUgrdGktegVqFiwA4iXm8wb4d_23zXurXeEdaNIj1bRAvD-Y7vKXWJw2lPeKvf9wmsJaerHoS4MIjIYriD6UVK68y9QYAxzL-_MECqD4RIIPmpVVMcF5n8ngyiKUVI3ZIHzr_d_fCwNdPHXcSG9o-NT99E9MUyTvJNhkiLoDAwtZ02ShPc4E---pNL5jce_yXS0003__mC0)

## 2. Cơ chế phân tích

### 2.1. Đề xuất Cơ chế

#### 2.1.1 Quản lý Thời gian làm việc
- **Giải thích**: Cơ chế này cho phép nhân viên ghi nhận và chỉnh sửa thời gian làm việc của mình trong một khoảng thời gian nhất định. Điều này đảm bảo tính chính xác trong việc thanh toán.

#### 2.1.2 Tính toán Tiền lương
- **Giải thích**: Tính toán lương cho cả nhân viên theo giờ và lương cố định, bao gồm việc tính toán lương ngoài giờ cho nhân viên làm việc trên 8 giờ.

#### 2.1.3 Quản lý Hoa hồng
- **Giải thích**: Tính toán hoa hồng cho nhân viên có lương cố định dựa trên doanh thu từ đơn hàng. Cơ chế này đảm bảo nhân viên được thưởng công bằng dựa trên hiệu suất làm việc.

#### 2.1.4 Tích hợp Cơ sở dữ liệu
- **Giải thích**: Kết nối tới cơ sở dữ liệu dự án hiện tại để lấy thông tin charge numbers mà không cần phải thay thế hệ thống hiện tại. Điều này giảm thiểu chi phí và rủi ro.

#### 2.1.5 Chọn Phương thức Thanh toán
- **Giải thích**: Cho phép nhân viên lựa chọn giữa các phương thức thanh toán khác nhau (mail, chuyển khoản, hoặc nhận trực tiếp). Đảm bảo tính linh hoạt cho nhân viên.

#### 2.1.6 Báo cáo cho Nhân viên
- **Giải thích**: Cung cấp khả năng truy vấn và tạo báo cáo cho nhân viên về giờ làm việc, tổng tiền đã nhận và thời gian nghỉ còn lại. Điều này giúp nhân viên theo dõi thông tin của họ một cách dễ dàng.

#### 2.1.7 Tự động hóa Quy trình Thanh toán
- **Giải thích**: Thiết lập quy trình thanh toán tự động hàng tuần và vào cuối tháng, giúp giảm thiểu sự can thiệp của con người và tăng tính chính xác.

### 2.2. Kết quả Mong đợi
- Danh sách các cơ chế phù hợp sẽ hỗ trợ trong việc phát triển hệ thống payroll mới, đảm bảo tính chính xác, an toàn, và dễ sử dụng cho nhân viên và quản trị viên.

## 3. Phân tích ca sử dụng Payment

### 3.1. Xác định các lớp phân tích

#### 3.1.1 Các lớp chính
- **Employee**
  - Nhiệm vụ: Đại diện cho nhân viên trong hệ thống, có khả năng chọn phương thức thanh toán.
  - Thuộc tính: `employeeID`, `name`, `paymentMethod`, `address`, `bankName`, `accountNumber`.

- **PaymentMethod**
  - Nhiệm vụ: Đại diện cho các phương thức thanh toán có sẵn cho nhân viên.
  - Thuộc tính: `methodID`, `methodName` (pick-up, mail, direct deposit).

- **PaymentService**
  - Nhiệm vụ: Xử lý các yêu cầu liên quan đến việc chọn phương thức thanh toán và cập nhật thông tin nhân viên.
  - Thuộc tính: None.

### 3.2. Biểu đồ Sequence
![Diagram](https://www.planttext.com/api/plantuml/png/Z99BJiCm48RtFiKeArZq0fM2ocl9GweuW6KFnAfVs9D8EGI7A3jOiU-2HQJUWnDm1PpYKBKAK6_6Jlxv_o-UVAxUPv5ueDfenWMv09V6QzSYCfyUAw4yjmJ5BMyDMffZQ9J00dY4l6UiBE6wwfujDAfxjI2gZzMJ1L-jtzPB-m2KpYyY5Muh8DSjBPGb6s9WSZ8uJI7WOusHSjWLKkNaqJ7Bxtlfq3O5gQBNlCtQ6q_AsPZ41-ByXX1HezWZC9kIhBacEF_sAxmIYqdj2mPfZH8AP-zLCFEDOw9BSAWZ_ZWOhlGVxVaoJgKC6FilwvMZp3wuHadSAdTYf0ef7oHw5nNz7tZ6xU82AS6DXMxbENLNZbQoyNdLNdB2WqQRB-vkqz6FT9Pi-p_q2m00__y30000)

### 3.3 Quan hệ giữa các lớp
- *Employee* có một phương thức thanh toán *PaymentMethod*.
- *PaymentService* xử lý việc chọn phương thức thanh toán và cập nhật thông tin cho *Employee*.

### 3.4. Biểu đồ lớp
![Diagram](https://www.planttext.com/api/plantuml/png/P56n3e8m4Dtx5HSc7HXS6Go33WuI4xwWj1SbqeBjrOGOlyp1J_8N1Am4IfVcthjxxrtxURrJIzoGKnKJ5RSMzggfwXOH7Wow4mDwuB1B82TJwhCdD5SOG0rl5Mew8brgcS1fMleMBgL1QuF1WkjhjjJZGjHEK-PKWMRadinddUcFWTLGBkB-u9b9A9IZkPVYlpg0mPj3IpERrTgJhf6SCEGwoV45eqq4SJnSywG9MAnGa8Kj2wmdCwDEuhtwTfQYblrlVG400F__0m00)

### 3.5 Giải thích
- *Employee*: Là người dùng tương tác với hệ thống để chọn phương thức thanh
 toán.
- *PaymentMethod*: Cung cấp các lựa chọn thanh toán cho *Employee*.
- *PaymentService*: Đảm bảo rằng yêu cầu của *Employee* được xử lý đúng cách.

## 4. Kịch bản chi tiết cho các ca sử dụng

### 4.1. Ca Sử dụng: Chọn Phương thức Thanh toán

#### Mô tả
Nhân viên có thể đăng nhập vào hệ thống và chọn một trong ba phương thức thanh toán: nhận tại công ty (pick-up), qua thư (mail), hoặc chuyển khoản trực tiếp (direct deposit).

#### Tác nhân
- **Employee**: Người yêu cầu thay đổi phương thức thanh toán của mình.

#### Kịch bản chính

1. **Employee** đăng nhập vào hệ thống.
2. **Employee** vào phần "Cập nhật Thông tin Thanh toán."
3. **Employee** chọn một trong ba phương thức thanh toán:
   - Nhận tại công ty (pick-up)
   - Qua thư (mail)
   - Chuyển khoản trực tiếp (direct deposit)
4. **Employee** nhập thông tin liên quan:
   - Nếu chọn "mail": nhập địa chỉ nhận thư.
   - Nếu chọn "direct deposit": nhập tên ngân hàng và số tài khoản.
5. **Employee** nhấn "Cập nhật."
6. **PaymentService** kiểm tra tính hợp lệ của thông tin.
7. **PaymentService** lưu thông tin mới và thông báo cho **Employee** về việc cập nhật thành công.

#### Kịch bản thay thế

- **Bước 4a**: Nếu thông tin không hợp lệ, **PaymentService** thông báo lỗi và yêu cầu **Employee** nhập lại thông tin chính xác.

#### Điều kiện tiên quyết
- **Employee** đã có tài khoản và đăng nhập thành công.

#### Điều kiện hậu
- Thông tin thanh toán của **Employee** được cập nhật trong hệ thống.

### 4.2. Ca Sử dụng: Nhận Báo cáo

#### Mô tả
Nhân viên có thể xem báo cáo chi tiết về giờ làm việc, tiền lương đã nhận và thời gian nghỉ phép còn lại.

#### Tác nhân
- **Employee**: Người yêu cầu xem báo cáo cá nhân.

#### Kịch bản chính

1. **Employee** đăng nhập vào hệ thống.
2. **Employee** vào phần "Xem Báo cáo."
3. **Employee** chọn loại báo cáo muốn xem:
   - Giờ làm việc
   - Tiền lương đã nhận
   - Thời gian nghỉ phép còn lại
4. **Reporting Module** lấy dữ liệu từ cơ sở dữ liệu và tạo báo cáo.
5. Hệ thống hiển thị báo cáo cho **Employee** xem.

#### Điều kiện tiên quyết
- **Employee** đã đăng nhập thành công vào hệ thống.

#### Điều kiện hậu
- Báo cáo của **Employee** được hiển thị trên màn hình.

### 4.3. Ca Sử dụng: Tính Toán Lương

#### Mô tả
Hệ thống tự động tính toán tiền lương hàng tuần cho nhân viên, bao gồm các khoản phụ cấp ngoài giờ nếu có.

#### Tác nhân
- **Payroll Processing Engine**: Bộ phận tính toán lương cho nhân viên.

#### Kịch bản chính

1. **Payroll Processing Engine** khởi chạy quy trình tính lương hàng tuần.
2. **Payroll Processing Engine** lấy dữ liệu giờ làm việc của từng nhân viên.
3. Với mỗi nhân viên:
   - Tính tiền lương cơ bản dựa trên số giờ làm việc tiêu chuẩn.
   - Tính phụ cấp ngoài giờ (nếu có) cho nhân viên làm việc hơn 8 giờ/ngày.
   - Tính hoa hồng cho nhân viên có mức lương cơ bản, dựa trên doanh thu đơn hàng.
4. **Payroll Processing Engine** ghi nhận kết quả tính toán trong cơ sở dữ liệu.
5. Thông báo gửi đến **Employee** rằng lương của họ đã được tính toán và sẵn sàng thanh toán.

#### Điều kiện tiên quyết
- Dữ liệu giờ làm việc và doanh thu đơn hàng đã được nhập đầy đủ trong hệ thống.

#### Điều kiện hậu
- Kết quả tính lương được lưu trữ trong cơ sở dữ liệu, và nhân viên được thông báo về khoản lương đã được tính toán.

---

## 5. Biểu đồ Activity của quy trình "Tính Toán Lương"

![Diagram](https://www.planttext.com/api/plantuml/png/VP2n3W8m48Nl-HLVI-5y7G74MaN9LmmdCTy8FG70xPlcZ65Epl1q7nqMrNC30u5C7pBq6JjBdzq6R34OPqnz9PSfyzXtnThPFp4yajLtOlb_K9uZbLRK9bucOWHc5XpU3cnCJ5Zs0xZh1IOTstHT8Nm9APDh9OHK0gDP66vKh5mTcaiiXeGidIhhgkVOEFtoOxWecegKTfu1G8qW7VgRtntCsEN9FVPPzydY1zxsfw8EXfByxnBqggACy_hCLnRLDUPXlZTUm-EuMjm00__0A00)

#### Giải thích biểu đồ
1. Quy trình bắt đầu với việc lấy dữ liệu thời gian làm việc của nhân viên.
2. Tính toán lương cơ bản và phụ cấp ngoài giờ.
3. Tính toán hoa hồng (nếu có).
4. Lưu kết quả và gửi thông báo cho nhân viên về việc tính toán lương hoàn tất.

---

## 6. Kết luận

Hệ thống đề xuất sử dụng kiến trúc client-server và các thành phần cơ bản để xây dựng hệ thống payroll mới. Các cơ chế được phân tích chi tiết đảm bảo tính chính xác và linh hoạt trong việc thanh toán, giúp nhân viên dễ dàng kiểm soát thông tin cá nhân.
