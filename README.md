
# 🏢 Thiết Kế Mạng cho Công Ty Outsource O-UIT

## 📖 Giới thiệu
Dự án này trình bày giải pháp **thiết kế hệ thống mạng** cho công ty Outsource O-UIT, bao gồm **Trụ sở chính (HQ)** và **Chi nhánh**.  
Thiết kế tập trung vào **tính sẵn sàng cao**, **bảo mật**, và **khả năng mở rộng**, đảm bảo kết nối liền mạch giữa các địa điểm.

---

## ✅ Tính năng chính
- **Hệ thống mạng nhiều chi nhánh**: HQ tại Thủ Đức & Chi nhánh tại Quận 3.
- **Phân chia VLAN theo phòng ban** để tăng cường bảo mật và quản lý lưu lượng.
- **Kết nối VPN Site-to-Site** sử dụng GRE kết hợp IPsec để bảo mật dữ liệu.
- **Đảm bảo tính sẵn sàng cao** với HSRP làm gateway dự phòng.
- **Định tuyến động** với OSPF để tối ưu đường đi.
- **Kết nối không dây** bằng các Access Point hỗ trợ Wi-Fi 6 của Cisco.
- **DHCP & NAT** cho cấp phát IP và truy cập Internet.
- **ACL** kiểm soát lưu lượng giữa các VLAN.

---

## 🏗 Kiến trúc mạng
### Thiết kế logic
- **Mô hình 3 lớp**: Core, Distribution, Access.
- VLAN cho từng phòng ban:
  - HQ: Developer (30), Tester (40), IT Manager (50), Technical Manager (60), Project Manager (70), HR (80), Business Analyst (90), CEO (100), Data Center (110)
  - Chi nhánh: Developer (10), Tester (20)

### Thiết kế vật lý
- **Thiết bị sử dụng**:
  - Router: Cisco ISR4331/K9
  - Switch: Cisco Catalyst 2960 (L2), Cisco C9200 (L3)
  - Access Point: Cisco CBW150AX-S (Wi-Fi 6)
- **Dự phòng**: Sử dụng HSRP trên các thiết bị Layer 3.

---

## 📡 Địa chỉ IP & VLAN
- HQ: Subnet từ `192.168.30.0/26` đến `192.168.110.0/26`
- Chi nhánh: Subnet từ `192.168.10.0/26` đến `192.168.20.0/26`
- GRE VPN Tunnel: `172.16.100.0/30` đến `172.16.103.0/30`
- Địa chỉ IP ảo HSRP cho từng VLAN.

---

## 💰 Chi phí dự kiến
### Thiết bị
| Thiết bị | Model | Số lượng | Giá (VND) |
|----------|-------|----------|-----------|
| Router | Cisco ISR4331/K9 | 4 | 160,000,000 |
| Switch L2 | Cisco Catalyst 2960 | 15 | 585,000,000 |
| Switch L3 | Cisco C9200-24P-E | 4 | 320,000,000 |
| Access Point | Cisco CBW150AX-S | 6 | 24,000,000 |
| **Tổng** |  |  | **1,089,000,000** |

### Dịch vụ
- Internet (F300 Plus): 9,900,000 VND/tháng
- VPN, bảo trì, Azure VM: 11,200,000 VND/tháng

---

## 🛠 Các bước triển khai
1. Cấu hình VLAN & định tuyến liên VLAN trên Switch L3.
2. Thiết lập OSPF trên Router để định tuyến động.
3. Cấu hình VPN GRE giữa HQ và chi nhánh.
4. Thiết lập HSRP cho gateway dự phòng.
5. Kích hoạt DHCP & NAT để cấp phát IP và truy cập Internet.
6. Áp dụng ACL để kiểm soát lưu lượng.
7. Cấu hình Access Point cho kết nối không dây.

---

## ⚠️ Hạn chế hiện tại
- Chưa có hệ thống **giám sát mạng tập trung** → Đề xuất triển khai **Zabbix / PRTG**.
- VPN chưa mã hóa mạnh → Cần triển khai **IPsec**.
- Wi-Fi chưa phân VLAN nội bộ đúng mong đợi.

---

## 👥 Nhóm thực hiện
- 22521490 – Nguyễn Đức Toàn  
- 22521212 – Nguyễn Đặng Khánh Quốc  
- 22521344 – Đặng Chí Thành  
- 22521469 – Nguyễn Cao Tiến  

---

## 📚 Tài liệu tham khảo
- Cisco Docs: [Cấu hình DHCP & VLAN](https://www.cisco.com/en/US/docs/routers/access/800/850/software/configuration/guide/dhcpvlan.htm)
- YouTube: [Cấu hình HSRP nhiều VLAN](https://www.youtube.com/watch?v=9-JY_On0-vY)
- CNTTShop: [Cấu hình ACL trên Cisco](https://cnttshop.vn/blogs/cisco/huong-dan-cau-hinh-access-list-tren-cisco-voi-lab-cu-the)
