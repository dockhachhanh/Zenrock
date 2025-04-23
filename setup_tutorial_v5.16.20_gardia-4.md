# Hướng Dẫn Cài Đặt Node Zenrock Testnet (Chain ID: gardia-4)
Hướng dẫn này giúp bạn cài đặt và chạy node Zenrock testnet với chain ID gardia-4, sử dụng Cosmovisor để quản lý nâng cấp
---
# Thông Tin Cơ Bản
- Chain ID: gardia-4
- Latest Version Tag: v5.16.20
- Sidecar Version: v5.16.9
- Custom Port: 182
- Binary: zenrockd
- Cosmovisor Version: v1.6.0
---
# Yêu Cầu Hệ Thống
- Hệ điều hành: Ubuntu 20.04 hoặc mới hơn
- RAM: 8GB (khuyến nghị 16GB)
- CPU: 4 cores
- Dung lượng ổ đĩa: 500GB SSD (khuyến nghị NVMe)
- Kết nối mạng ổn định
---
# Các Bước Cài Đặt
## 1. Thiết Lập Tên Validator
Thay thế YOUR_MONIKER_GOES_HERE bằng tên validator của bạn:
```bash
MONIKER="YOUR_MONIKER_GOES_HERE"
```


