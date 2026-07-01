# 1.Định nghĩa:

`Phần mở rộng (extension) của một AWS Region`

Mỗi Local Zone có:

- Connection riêng đến internet
- Support Direct Connect
- Geographic proximity đến users

# 2. Mục đích

- Low latency sensitive app
- Compliance (data đặt ở quốc gia cụ thể,..)

# 3. Cách dùng

- Enable Local Zone (first step)
- Create subnet trong Local Zone
- Launch resources trong Local Zone subnet → Resources đặt gần users
- **Kết luận**: AWS Local Zones là extension của AWS Region đặt gần các thành phố lớn lớn để cung cấp compute, storage, database services gần người dùng cuối, cho phép chạy ứng dụng nhạy cảm latency (gaming, streaming, AR/VR) và tuân thủ data residency requirements (y tế, ngân hàng)
