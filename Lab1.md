# Lab 1 - PHÂN TÍCH KIẾN TRÚC, CƠ CHẾ, CA SỬ DỤNG

## 1. Phân tích kiến trúc

### 1.1. Đề xuất Kiến trúc

#### 1.1.1 Kiến trúc Tổng thể
- **Client-Server Architecture**: Sử dụng mô hình kiến trúc client-server để phân tách các yêu cầu của người dùng từ các dịch vụ xử lý dữ liệu trên máy chủ. Nhân viên có thể sử dụng ứng dụng máy tính để bàn để gửi thông tin, trong khi hệ thống sẽ xử lý các yêu cầu trên máy chủ.

#### 1.1.2 Thành phần Kiến trúc

- **Client Layer**:
  - *Windows Desktop Application*: Giao diện thân thiện cho nhân viên nhập các thông tin như thời gian làm việc, đơn hàng, và tùy chọn thanh toán.
  - *Reporting Module*: Cung cấp tính năng tạo báo cáo cho nhân viên, bao gồm giờ làm việc, số tiền đã nhận, và thời gian nghỉ phép.

- **Business Logic Layer**:
  - *Payroll Processing Engine*: Xử lý việc tính toán tiền lương, yêu cầu thanh toán của nhân viên và tạo báo cáo.
  - *Timecard Management*: Quản lý việc ghi nhận thời gian làm việc và lưu trữ dữ liệu.
  - *Commission Calculation*: Tính toán hoa hồng cho nhân viên có lương cố định dựa trên doanh thu.

- **Data Access Layer**:
  - *Employee Database*: Cơ sở dữ liệu lưu trữ thông tin về nhân viên, giờ làm việc, và đơn hàng.
  - *Project Management Database (DB2)*: Kết nối tới cơ sở dữ liệu hiện tại để lấy thông tin dự án và charge numbers, mà không cần thay thế hệ thống hiện tại.

- **Integration Layer**:
  - *Payment Processing Module*: Hỗ trợ thanh toán qua chuyển khoản ngân hàng, gửi thư, hoặc nhận tại công ty, đáp ứng sự linh hoạt cho nhân viên.

### 1.2. Biểu đồ Package
![Diagram](https://www.planttext.com/api/plantuml/png/X99BQiCm48RtFiMGVQvGaZfP5188eT15o68g3qADf16IJ36X9-kYH-eLAZzArTQnjPt_CVEXp_UFLOZeOsrquL1SK18iIgt8HjXXGtu1rmBIEpqfM_5hW0s5IsG7Q-Uq4XWLstElE99Z7vMLiEUgrdGktegVqFiwA4iXm8wb4d_23zXurXeEdaNIj1bRAvD-Y7vKXWJw2lPeKvf9wmsJaerHoS4MIjIYriD6UVK68y9QYAxzL-_MECqD4RIIPmpVVMcF5n8ngyiKUVI3ZIHzr_d_fCwNdPHXcSG9o-NT99E9MUyTvJNhkiLoDAwtZ02ShPc4E---pNL5jce_yXS0003__mC0)

## 2. Cơ chế phân tích

### 2.1. Đề xuất Cơ chế

#### 2.1.1 Quản lý Thời gian làm việc
- **Giải thích**: Cơ chế này cho phép nhân viên ghi nhận và điều chỉnh thời gian làm việc, đảm bảo tính chính xác trong việc thanh toán.

#### 2.1.2 Tính toán Tiền lương
- **Giải thích**: Tính lương cho cả nhân viên theo giờ và nhân viên lương cố định, bao gồm cả phụ cấp ngoài giờ.

#### 2.1.3 Quản lý Hoa hồng
- **Giải thích**: Tính toán hoa hồng dựa trên doanh thu từ đơn hàng, đảm bảo phần thưởng công bằng cho nhân viên dựa trên hiệu suất.

#### 2.1.4 Tích hợp Cơ sở dữ liệu
- **Giải thích**: Kết nối tới cơ sở dữ liệu dự án hiện tại để lấy thông tin charge numbers mà không thay thế hệ thống, giảm thiểu chi phí và rủi ro.

#### 2.1.5 Chọn Phương thức Thanh toán
- **Giải thích**: Cho phép nhân viên lựa chọn các phương thức thanh toán linh hoạt như mail, chuyển khoản hoặc nhận trực tiếp.

#### 2.1.6 Báo cáo cho Nhân viên
- **Giải thích**: Cung cấp khả năng truy vấn và báo cáo về giờ làm, tổng tiền lương và thời gian nghỉ phép.

#### 2.1.7 Tự động hóa Quy trình Thanh toán
- **Giải thích**: Thiết lập quy trình tự động thanh toán hàng tuần và cuối tháng, giảm thiểu can thiệp thủ công và nâng cao tính chính xác.

### 2.2. Kết quả Mong đợi
- Các cơ chế phù hợp hỗ trợ phát triển hệ thống payroll mới, đảm bảo tính chính xác, an toàn, và dễ sử dụng cho nhân viên và quản trị viên.

## 3. Phân tích ca sử dụng Payment

### 3.1. Xác định các lớp phân tích

#### 3.1.1 Các lớp chính
- **Employee**
  - Nhiệm vụ: Đại diện nhân viên, có khả năng chọn phương thức thanh toán.
  - Thuộc tính: `employeeID`, `name`, `paymentMethod`, `address`, `bankName`, `accountNumber`.

- **PaymentMethod**
  - Nhiệm vụ: Đại diện các phương thức thanh toán.
  - Thuộc tính: `methodID`, `methodName` (pick-up, mail, direct deposit).

- **PaymentService**
  - Nhiệm vụ: Xử lý yêu cầu liên quan đến việc chọn phương thức thanh toán và cập nhật thông tin nhân viên.

### 3.2. Biểu đồ Sequence
![Diagram](https://www.planttext.com/api/plantuml/png/Z99BJiCm48RtFiKeArZq0fM2ocl9GweuW6KFnAfVs9D8EGI7A3jOiU-2HQJUWnDm1PpYKBKAK6_6Jlxv_o-UVAxUPv5ueDfenWMv09V6QzSYCfyUAw4yjmJ5BMyDMffZQ9J00dY4l6UiBE6wwfujDAfxjI2gZzMJ1L-jtzPB-m2KpYyY5Muh8DSjBPGb6s9WSZ8uJI7WOusHSjWLKkNaqJ7Bxtlfq3O5gQBNlCtQ6q_AsPZ41-ByXX1HezWZC9kIhBacEF_sAxmIYqdj2mPfZH8AP-zLCFEDOw9BSAWZ_ZWOhlGVxVaoJgKC6FilwvMZp3wuHadSAdTYf0ef7oHw5nNz7tZ6xU82AS6DXMxbENLNZbQoyNdLNdB2WqQRB-vkqz6FT9Pi-p_q2m00__y30000)

### 3.3 Quan hệ giữa các lớp
- *Employee* có một phương thức thanh toán *PaymentMethod*.
- *PaymentService* xử lý yêu cầu chọn phương thức thanh toán và cập nhật thông tin cho *Employee*.

### 3.4. Biểu đồ lớp
![Diagram](https://www.planttext.com/api/plantuml/png/P56n3e8m4Dtx5HSc7HXS6Go33WuI4xwWj1SbqeBjrOGOlyp1J_8N1Am4IfVcthjxxrtxURrJIzoGKnKJ5RSMzggfwXOH7Wow4mDwuB1B82TJwhCdD5SOG0rl5Mew8brgcS1fMleMBgL1QuF1WkjhjjJZGjHEK-PKWMRadinddUcFWTLGBkB-u9b9A9IZkPVYlpg0mPj3IpERrTgJhf6SCEGwoV45eqq4SJnSywG9MAnGa8Kj2wmdCwDEuhtwTfQYblrlVG400F__0m00)

### 3.5 Giải thích
- *Employee*: Người dùng tương tác với hệ thống để chọn phương thức thanh toán.
- *PaymentMethod*: Cung cấp các lựa chọn thanh toán.
- *PaymentService*: Đảm bảo yêu cầu của *Employee* được xử lý đúng cách.

## 4. Phân tích ca sử dụng Maintain Timecard
### 4.1. Xác định các lớp phân tích
### 4.1.1. Các lớp chính
- **Employee**
  - Nhiệm vụ: Đại diện cho người sử dụng hệ thống, có khả năng nhập và gửi thông tin thời gian.
  - Thuộc tính: employeeID, name, role, loggedInStatus.
    
- **Timecard**
Nhiệm vụ: Lưu trữ thông tin thời gian làm việc của nhân viên cho từng kỳ trả lương.
  - Thuộc tính: timecardID, employeeID, startDate, endDate, submittedDate, status, totalHours.
    
- **ChargeNumber**
  - Nhiệm vụ: Đại diện cho các dự án mà nhân viên có thể ghi nhận giờ làm việc.
  - Thuộc tính: chargeNumberID, projectName, availableHours.

- **ProjectManagementDatabase**
  - Nhiệm vụ: Cung cấp danh sách charge numbers cho hệ thống.
  - Thuộc tính: connectionStatus.
    
- **TimecardService**
  - Nhiệm vụ: Xử lý các thao tác liên quan đến thời gian làm việc của nhân viên (lưu, gửi).
  - Thuộc tính: maxHoursPerEmployee.
    
### 4.2. Biểu đồ Sequence
 ![Diagram](https://www.planttext.com/api/plantuml/png/b9A_JiCm48TtFyKfKnbu0QIWIg4gB2pDmcYS8ptXEC5_8dLcOEK5a90Oa92wCJK3G_iYVG9U0JiafOeA4XaiA_dTTz_P-Mm-niPoRLqX6HUsr30fAbak45dbNvEWYYiBKKe52gwp6UgQ14R03NJxmy4saIQCnJ5i7ZVtAWSrtwwM5SGnwtl0yMbFEG5PvgH6Hst5rVhDWTYkNXrONzM4jNaYo8chNm4QxnmQsnjuLFSffD8a1Amch35nMgFQ3wP9oFJK4yZ8L98lzXB1wl9xW9oy2yZrSm6rtpw8eL7evVcepqkdpGw_4pMynW5wkcsMz8zPZRikw8zHQoufunPx0oujJ5jl3t-fG7fl1luPgg6TjMYBsPclzwKXjKV_EIHHgXlIHPitXifmUIWDTerkv-jtV-k3VWT9tN5Fj2xrABfGhJtCWtlacIfZREpNy9D-0G00__y30000)
 
### 4.3. Quan hệ giữa các lớp
- Employee có một hoặc nhiều Timecard.
- Timecard chứa một hoặc nhiều ChargeNumber.
- ProjectManagementDatabase cung cấp danh sách ChargeNumber cho Timecard.
- TimecardService tương tác với Timecard và ProjectManagementDatabase để thực hiện các thao tác.
  
### 4.4. Biểu đồ lớp
 ![Diagram](https://www.planttext.com/api/plantuml/png/X5BBJiCm4BpxAwmSaLBHQmweWeBeWQfI-86Dimgk_AZiJGH2V1a7FebVm0vvD4qBEUGmE-kPdTtlpw-L9t1KQyM40k_vlJue-uR8tnaFNygn0pRhZEVafAcwWW6D9v2pwXHIjggmt9YSW6gVyLiRE63O1-i4dwL60QuS1Aa3Pe8NdRGZh862TlptT5FEC5yNMXBXcKhdR_8mMGBrQ6iN2W_A0essxrx0LRYjTO5ki2wEm9dBWxDx5BITnmODI0M5mlDIkz_69p1GeKOJHuK2_BWZOOq936d_Zpb7rqWnjcfuRLLtwFhL7naOhY5P9ZnDUNAzM5mbuyuoBXo643s_OGCuvKw2og9L0cbYm-Mv_dmXvDZ8SYBP3zNtBISMTIiG-MmLZYBU-Wy0003__mC0)
 
### 4.5. Giải thích
- Employee là người tương tác với hệ thống để quản lý thời gian làm việc.
- Timecard lưu giữ tất cả thông tin liên quan đến thời gian làm việc của nhân viên cho một kỳ trả lương nhất định.
- ChargeNumber cho phép nhân viên ghi nhận giờ làm việc theo các dự án cụ thể.
- ProjectManagementDatabase cung cấp dữ liệu cần thiết cho hệ thống.
- TimecardService thực hiện các thao tác cần thiết cho việc xử lý thời gian làm việc và đảm bảo các quy tắc nghiệp vụ được tuân thủ.

## 5. Hợp nhất kết quả phân tích
### 5.1. Hợp Nhất 2 Ca Sử Dụng: Select Payment Method và Maintain Timecard
#### 5.1.1. Các Lớp
- Employee: Là lớp trung tâm trong cả hai ca sử dụng, chứa thông tin của nhân viên và liên kết với cả Timecard và PaymentMethod.
- TimecardService và PaymentService: Hai dịch vụ này chịu trách nhiệm xử lý yêu cầu và cập nhật thông tin cho nhân viên.

#### 5.1.1.2. Luồng Hoạt Động Chung
- Nhân viên đăng nhập vào hệ thống.
- Nhân viên có thể chọn giữa việc duy trì thẻ thời gian hoặc lựa chọn phương thức thanh toán.
- Dữ liệu của nhân viên sẽ được cập nhật dựa trên các hành động mà họ thực hiện trong từng ca sử dụng.

### 5.2. Giới thiệu
- Tài liệu mô tả hai ca sử dụng chính trong hệ thống quản lý nhân viên: "Select Payment Method" và "Maintain Timecard."

### 5.3. Ca Sử Dụng 1: Select Payment Method
#### 5.3.1. Mô tả
- Cho phép nhân viên chọn phương thức thanh toán cho lương (nhận tiền mặt, qua thư, hoặc chuyển khoản).

#### 5.3.2. Luồng Sự Kiện
- Nhân viên yêu cầu chọn phương thức thanh toán.
- Hệ thống hiển thị các tùy chọn.
- Nhân viên chọn phương thức và cung cấp thông tin cần thiết.
- Hệ thống cập nhật thông tin thanh toán.
#### 5.3.3. Các Lớp Phân Tích
- Employee
- PaymentMethod
- PaymentService
  
#### 5.3.4. Biểu đồ Sequence
![Diagram](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bTYSab-aO9hRa5EVcLgAbS1K3WpERCWCQz4GIaWiJ8tDQyaEBMeB3CvLKaXiLW1okRYihLLyCiul2XFeIppyAeyXUICXxjxynGACevjEBOmBrsX1CXVcQnWQyi5Crf1rmwcsqgXABMmDBMu16g1Rsf9HdwAXYONL1wa5ARDIY4bixWW9x7Ilw0aCp-l6AWAgud5gJcfoGHCAYr8IIn9HRVK8JKl1HGI00000F__0m00)

### 5.4. Ca Sử Dụng 2: Maintain Timecard
#### 5.4.1. Mô tả
- Cho phép nhân viên cập nhật và gửi thẻ thời gian ghi lại giờ làm việc.

#### 5.4.2. Luồng Sự Kiện
- Nhân viên yêu cầu xem thẻ thời gian.
- Hệ thống hiển thị thẻ hiện tại hoặc tạo mới.
- Nhân viên nhập giờ làm và chọn charge.
- Hệ thống xác thực và lưu thông tin.
  
#### 5.4.3. Các Lớp Phân Tích
- Employee
- Timecard
- TimecardService
  
#### 5.4.4. Biểu đồ Sequence
  ![Diagram](https://www.planttext.com/api/plantuml/png/T90n3i8m34NtdCBg10CNg1JK1Oc9fLmWf8PQQfoGf9Lw61P692v01uQUX1Dm1LgfbHXWyRVix_Sblxjd5gBoiJQLK3fQ3nlZAjiY2ZUCIPDJ727Paq6jV96ZRqXZ0Yh0r0iX9UpA_ihGK7zZqA_7tG6NWqI8WtHZxIu49r8CKeev0rRhcPA2ntED8Sv9YwMOLgDhlaYXeE0grNxPVjAG8_gjhNtu1zAMZ-HDNXyCXK2M1sE6N8ol-0000F__0m00)
  
### 5.5. Kết luận
Hai ca sử dụng này giúp quản lý thông tin lương bổng và thời gian làm việc của nhân viên, đảm bảo tính chính xác và hiệu quả trong quy trình xử lý.
