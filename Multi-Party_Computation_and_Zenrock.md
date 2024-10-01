# Multi-Party Computation (MPC) và Zenrock

## Giới thiệu về MPC
Zenrock sử dụng giao thức **Multi-Party Computation** (MPC) để tạo ra nhiều bí mật độc lập từ khóa riêng điều khiển tài sản kỹ thuật số. Những bí mật này được phân phối giữa các nút MPC, trong đó một số nút được Zenrock vận hành, nhưng phần lớn sẽ được quản lý bởi các bên thứ ba.

## Quy trình ký và tạo khóa
Khi chủ sở hữu tài sản muốn ký một giao dịch hoặc tạo khóa công khai, yêu cầu sẽ được gửi đến các nút MPC. Mỗi nút sẽ tính toán phần của khóa và chữ ký, sau đó kết hợp lại để tạo thành khóa hoặc chữ ký hoàn chỉnh. Kết quả sẽ được công bố trên hợp đồng thông minh **zrSign**.

## Lợi ích của MPC
- **Tiếp cận dễ dàng**: Thay thế quản lý khóa riêng phức tạp giúp tài sản kỹ thuật số trở nên dễ dàng tiếp cận mà không làm giảm bảo mật.
- **Giao dịch ngay lập tức**: Người dùng có thể truyền phát giao dịch mà không sợ mất mát.

## An ninh cấp độ tổ chức
Khóa riêng lưu trữ trực tuyến thường là mục tiêu của tin tặc. MPC cho phép lưu trữ tài sản tiền điện tử mà không làm giảm bảo mật và phân phối các bí mật khóa riêng trên một kiến trúc phân tán, loại bỏ điểm thất bại duy nhất. Kẻ tấn công cần phải xâm nhập vào tất cả các máy trong mạng MPC.

## Quản lý linh hoạt
Các nút MPC có thể được ánh xạ tới các yêu cầu tổ chức cụ thể, với số lượng khác nhau của người ủy thác được sắp xếp thành các tập hợp và giới hạn theo ngưỡng cụ thể.

## Tối ưu cho tích hợp Omnichain
MPC là công nghệ ngoại tuyến tốt nhất cho thế giới đa chuỗi (omnichain), hoạt động độc lập với blockchain cơ sở, đảm bảo tính tương thích và khả năng truy cập rộng rãi.

## MPC là tương lai
Giống như Bitcoin đã loại bỏ sự tin cậy khỏi giao dịch, MPC có thể loại bỏ sự tin cậy khỏi quản lý khóa riêng. MPC được điều khiển bởi đồng thuận phi tập trung có thể giải phóng tài sản kỹ thuật số khỏi các vấn đề của quản lý khóa riêng tập trung.

## So sánh với các dịch vụ quản lý khóa trên chuỗi hiện tại
- **Ví đa chữ ký (Multisig Wallets)**: Yêu cầu nhiều chữ ký từ các bên khác nhau để thực hiện giao dịch, thích hợp cho việc kiểm soát chung các quỹ.
- **Shamir's Secret Sharing**: Chia sẻ dữ liệu nhạy cảm thành các phần và yêu cầu một tập hợp cụ thể để khôi phục lại toàn bộ, nhưng cần phải tập hợp lại trên một máy duy nhất.
- **Multi-Party Computation (dMPC)**: Cho phép nhiều bên cùng tính toán một hàm trong khi giữ bí mật đầu vào của họ.

## Cách thức hoạt động của Zenrock
Zenrock thực hiện dMPC và làm cho nó trở nên khả dụng thông qua hợp đồng thông minh **zrSign**.
