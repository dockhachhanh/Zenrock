# Zenrock Project Overview

## Giới thiệu về Zenrock

Chào mừng đến với **Zenrock**! Dự án Zenrock là sự kết hợp độc đáo giữa công nghệ blockchain và **MPC** (Tính toán đa bên), cung cấp một giải pháp dễ sử dụng cho các nhà phát triển Web3. Zenrock cho phép truy cập không cần giấy phép đến quản lý khóa cá nhân cấp độ tổ chức thông qua hợp đồng thông minh trên bất kỳ chuỗi nào hoặc API ngoại tuyến.

Người dùng có thể tương tác trực tiếp với các dApp yêu thích trên các mạng được hỗ trợ mà không cần cầu nối giữa các mạng. Các chữ ký và khóa công khai được lưu trữ an toàn trên Zenrock, giúp người dùng chỉ cần tạo giao dịch chưa ký và xuất bản nó lên nút RPC của mạng đích. Thiết kế này giúp người dùng kiểm soát tài sản từ xa và giảm thiểu số lượng hợp đồng thông minh cần thiết, đồng thời giảm thời gian và chi phí giao dịch.

### Sản phẩm của Zenrock

1. **zrSign**: Giải pháp hợp đồng thông minh mở rộng công nghệ MPC cho các mạng hỗ trợ hợp đồng thông minh.
2. **zrChain**: Blockchain riêng của Zenrock, nơi lưu trữ token gốc **ROCK** và cung cấp các công cụ quản lý khóa và tài sản.
3. **zenBTC**: Sản phẩm Bitcoin bọc, sử dụng hạ tầng dMPC, cung cấp giải pháp an toàn và minh bạch hơn cho Bitcoin.

---

## Giới thiệu về zrChain

**Zenrock Blockchain** là sản phẩm chính của dự án, nhằm cung cấp cơ sở hạ tầng bảo mật vững chắc cho tương lai đa chuỗi (omnichain). Dự án cung cấp các mô-đun tùy chỉnh cho quản lý danh tính và tài sản, giúp xây dựng ứng dụng tương tác với các mạng blockchain lớn.

### Chính sách

- **Chính sách** xác định các điều kiện cần thiết để xử lý yêu cầu từ các khóa như MPC của Zenrock. Các chính sách này bao gồm các bên tham gia có quyền phê duyệt hoặc từ chối yêu cầu.
- Khi một yêu cầu được tạo ra (ví dụ: yêu cầu chữ ký), các hành động sẽ được thực hiện theo quy định của chính sách trong không gian làm việc (workspace).

### Dịch vụ đã được xác thực

- zrChain tích hợp với **Eigenlayer**, cung cấp bảo mật kinh tế bằng cách yêu cầu tài sản bảo đảm cho các hợp đồng thông minh liên kết với mô-đun xác thực của zrChain.
- Nếu các validator vi phạm quy tắc, họ có thể bị phạt và mất stake trên zrChain cũng như trên hợp đồng thông minh trên Ethereum.

### Hợp đồng thông minh với CosmWasm

- Zenrock hỗ trợ **CosmWasm**, một ngôn ngữ hợp đồng thông minh dựa trên Rust, cho phép phát triển các trường hợp sử dụng linh hoạt và ứng dụng phân cấp nhanh chóng.

---

## Giới thiệu về zrSign

**zrSign** là giải pháp hợp đồng thông minh dựa trên Solidity dành cho các nhà phát triển mạng EVM, cho phép yêu cầu khóa và chữ ký từ các MPC. 

### Phiên bản zrSign

zrSign cung cấp hai phiên bản: **zrSign Direct** và **zrSign Omni**.

- **zrSign Direct**: Kết quả yêu cầu được trả trực tiếp về hợp đồng thông minh.
- **zrSign Omni**: Kết quả yêu cầu được quản lý thông qua zrChain, giúp tích hợp các tính năng của zrChain vào các dApp trên chuỗi EVM.

Cả hai phiên bản đều được triển khai bằng Solidity và có thể sử dụng để yêu cầu khóa và chữ ký từ MPC của Zenrock. zrSign Omni còn cung cấp các chức năng để quản lý không gian làm việc tương tự như zrChain, mang lại lợi ích của zrChain cho các nhà phát triển.

---

## Kết luận

Zenrock là một dự án toàn diện nhằm cung cấp cơ sở hạ tầng an toàn và dễ dàng cho các nhà phát triển trong việc xây dựng các ứng dụng đa chuỗi. Các sản phẩm của Zenrock, đặc biệt là zrChain và zrSign, cung cấp các tính năng mạnh mẽ cho việc quản lý tài sản và tương tác giữa các chuỗi khác nhau mà không gặp phải những khó khăn thường thấy như cầu nối hoặc chi phí giao dịch cao.
