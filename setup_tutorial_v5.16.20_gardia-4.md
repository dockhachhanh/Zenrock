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
# 2. Cài Đặt Các Phụ Thuộc
Cập nhật hệ thống và cài đặt các công cụ cần thiết:
```bash
sudo apt -q update
sudo apt -qy install curl git jq lz4 build-essential unzip
sudo apt -qy upgrade
```
# 3. Cài Đặt Go
Cài đặt Go phiên bản 1.24.2:
```bash
sudo rm -rf /usr/local/go
curl -Ls https://go.dev/dl/go1.24.2.linux-amd64.tar.gz | sudo tar -xzf - -C /usr/local
echo 'export PATH=$PATH:/usr/local/go/bin' | sudo tee /etc/profile.d/golang.sh
echo 'export PATH=$PATH:$HOME/go/bin' >> $HOME/.profile
source $HOME/.profile
go version
```
# 4. Tải và Xây Dựng Binary Zenrock
Tải mã nguồn và xây dựng binary zenrockd:
```bash
cd $HOME
rm -rf zrchain
git clone https://github.com/zenrocklabs/zrchain.git
cd zrchain
git checkout v5.16.20
make build
```
Chuẩn bị binary cho Cosmovisor:
```bash
mkdir -p $HOME/.zrchain/cosmovisor/genesis/bin
mv build/zenrockd $HOME/.zrchain/cosmovisor/genesis/bin/
rm -rf build
```
Tạo liên kết tượng trưng:
```bash
ln -sf $HOME/.zrchain/cosmovisor/genesis $HOME/.zrchain/cosmovisor/current
sudo ln -sf $HOME/.zrchain/cosmovisor/current/bin/zenrockd /usr/local/bin/zenrockd
```
Kiểm tra phiên bản:
```bash
zenrockd version
```
Đảm bảo đầu ra là v5.16.20.
# 5. Cài Đặt Cosmovisor
Cài đặt Cosmovisor phiên bản 1.6.0:
```bash
go install cosmossdk.io/tools/cosmovisor/cmd/cosmovisor@v1.6.0
cosmovisor version
```
Tạo thư mục backup và đặt quyền:
```bash
mkdir -p $HOME/.zrchain/backups
chown -R quai:quai $HOME/.zrchain
chmod -R 755 $HOME/.zrchain
```
# 6. Chuẩn Bị cho Nâng Cấp v5rev5
Blockchain yêu cầu nâng cấp v5rev5 tại block height 230500, sử dụng cùng phiên bản v5.16.20. Tạo thư mục nâng cấp và sao chép binary:
```bash
mkdir -p $HOME/.zrchain/cosmovisor/upgrades/v5rev5/bin
cp $HOME/.zrchain/cosmovisor/genesis/bin/zenrockd $HOME/.zrchain/cosmovisor/upgrades/v5rev5/bin/
chown -R quai:quai $HOME/.zrchain/cosmovisor/upgrades/v5rev5
chmod -R 755 $HOME/.zrchain/cosmovisor/upgrades/v5rev5
```
Kiểm tra binary:
```bash
$HOME/.zrchain/cosmovisor/upgrades/v5rev5/bin/zenrockd version
```
# 7. Tạo Systemd Service
Tạo file dịch vụ systemd:
```bash
sudo tee /etc/systemd/system/zenrock-testnet.service > /dev/null << EOF
[Unit]
Description=Zenrock node service
After=network-online.target

[Service]
User=quai
ExecStart=$(which cosmovisor) run start --home $HOME/.zrchain
Restart=on-failure
RestartSec=10
LimitNOFILE=65535
Environment="DAEMON_HOME=$HOME/.zrchain"
Environment="DAEMON_NAME=zenrockd"
Environment="DAEMON_DATA_BACKUP_DIR=$HOME/.zrchain/backups"
Environment="DAEMON_ALLOW_DOWNLOAD_BINARIES=false"
Environment="DAEMON_RESTART_AFTER_UPGRADE=true"
Environment="PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin:$HOME/.zrchain/cosmovisor/current/bin"

[Install]
WantedBy=multi-user.target
EOF
```
Kích hoạt và reload service:
```bash
sudo systemctl daemon-reload
sudo systemctl enable zenrock-testnet.service
```
# 8. Cấu Hình Node
Cấu hình client:
```bash
zenrockd config set client chain-id gardia-4
zenrockd config set client keyring-backend test
zenrockd config set client node tcp://localhost:18257
```
# 9. Khởi Tạo Node
Khởi tạo node với moniker:
```bash
zenrockd init "$MONIKER" --chain-id gardia-4
```
Tải genesis và addrbook:
```bash
curl -Ls https://snapshots.kjnodes.com/zenrock-testnet/genesis.json > $HOME/.zrchain/config/genesis.json
curl -Ls https://snapshots.kjnodes.com/zenrock-testnet/addrbook.json > $HOME/.zrchain/config/addrbook.json
```
Thêm seeds:
```bash
sed -i -e "s|^seeds *=.*|seeds = \"3f472746f46493309650e5a033076689996c8881@zenrock-testnet.rpc.kjnodes.com:18259\"|" $HOME/.zrchain/config/config.toml
```
Thiết lập minimum gas price:
```bash
sed -i -e "s|^minimum-gas-prices *=.*|minimum-gas-prices = \"2.5urock\"|" $HOME/.zrchain/config/app.toml
```
Thiết lập pruning:
```bash
sed -i \
  -e 's|^pruning *=.*|pruning = "custom"|' \
  -e 's|^pruning-keep-recent *=.*|pruning-keep-recent = "100"|' \
  -e 's|^pruning-keep-every *=.*|pruning-keep-every = "0"|' \
  -e 's|^pruning-interval *=.*|pruning-interval = "19"|' \
  $HOME/.zrchain/config/app.toml
```
Thiết lập custom ports:
```bash
sed -i -e "s%^proxy_app = \"tcp://127.0.0.1:26658\"%proxy_app = \"tcp://127.0.0.1:18258\"%; s%^laddr = \"tcp://127.0.0.1:26657\"%laddr = \"tcp://127.0.0.1:18257\"%; s%^pprof_laddr = \"localhost:6060\"%pprof_laddr = \"localhost:18260\"%; s%^laddr = \"tcp://0.0.0.0:26656\"%laddr = \"tcp://0.0.0.0:18256\"%; s%^prometheus_listen_addr = \":26660\"%prometheus_listen_addr = \":18266\"%" $HOME/.zrchain/config/config.toml
sed -i -e "s%^address = \"tcp://0.0.0.0:1317\"%address = \"tcp://0.0.0.0:18217\"%; s%^address = \":8080\"%address = \":18280\"%; s%^address = \"0.0.0.0:9090\"%address = \"0.0.0.0:18290\"%; s%^address = \"0.0.0.0:9091\"%address = \"0.0.0.0:18291\"%; s%:8545%:18245%; s%:8546%:18246%; s%:6065%:18265%" $HOME/.zrchain/config/app.toml
```
# 10. Tải Snapshot
Tải snapshot mới nhất để đồng bộ nhanh:
```bash
curl -L https://snapshots.kjnodes.com/zenrock-testnet/snapshot_latest.tar.lz4 | tar -Ilz4 -xf - -C $HOME/.zrchain
```
Sao chép upgrade-info.json (nếu có):
```bash
[[ -f $HOME/.zrchain/data/upgrade-info.json ]] && cp $HOME/.zrchain/data/upgrade-info.json $HOME/.zrchain/cosmovisor/genesis/upgrade-info.json
```
# 11. Khởi Động Node
Khởi động dịch vụ:
```bash
sudo systemctl start zenrock-testnet.service
```
Kiểm tra trạng thái:
```bash
sudo systemctl status zenrock-testnet.service
```
Kiểm tra logs:
```bash
sudo journalctl -u zenrock-testnet.service -f --no-hostname -o cat
```
Kiểm tra trạng thái đồng bộ:
```bash
zenrockd status --node tcp://localhost:18257 | jq .SyncInfo
```
Nếu "catching_up": false, node đã đồng bộ.
