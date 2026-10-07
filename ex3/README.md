# Bài 3: Cấu hình tường lửa UFW và chuẩn đoán cổng mạng

## 1. Cấu hình UFW
Thực hiện các lệnh sau để cấu hình UFW:

```bash
# Đảm bảo cấu hình chặn tất cả đầu vào và mở tất cả đầu ra mặc định
sudo ufw default deny incoming
sudo ufw default allow outgoing

# Thêm quy tắc cho phép cổng SSH (port 22) và cổng ứng dụng Web (port 8080)
sudo ufw allow 22/tcp
sudo ufw allow 8080/tcp

# Bật tường lửa
sudo ufw enable
```

## 2. Kiểm tra trạng thái tường lửa

Kết quả lệnh `sudo ufw status verbose`:

```
Status: active
Logging: on (low)
Default: deny (incoming), allow (outgoing), disabled (routed)
New profiles: skip

To                         Action      From
--                         ------      ----
22/tcp                     ALLOW IN    Anywhere
8080/tcp                   ALLOW IN    Anywhere
22/tcp (v6)                ALLOW IN    Anywhere (v6)
8080/tcp (v6)              ALLOW IN    Anywhere (v6)
```

## 3. Kiểm tra các cổng đang lắng nghe

Kết quả lệnh `ss -tlnp`:

```
State    Recv-Q   Send-Q     Local Address:Port     Peer Address:Port   Process
LISTEN   0        128              0.0.0.0:22            0.0.0.0:*       users:(("sshd",pid=1000,fd=3))
LISTEN   0        128              0.0.0.0:8080          0.0.0.0:*       users:(("node",pid=1001,fd=18))
LISTEN   0        128                 [::]:22               [::]:*       users:(("sshd",pid=1000,fd=4))
```
