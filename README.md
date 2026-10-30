# BÀI 6

## I. CẦU TRÚC THƯ MỤC LƯU TRỮ & PHÂN QUYỀN (FOLDER STRUCTURE & PERMISSION)

```text
Green-Tech_Root/
├── .env (Mật khẩu cảm biến - CHẶN ĐỒNG BỘ LÊN CLOUD)
├── 01_Sensor_Code/            [Mô hình Hybrid Workflow cho Dev]
│   ├── firmware/
│   └── drivers/
├── 02_Investor_Reports/       [Dành cho Nhà đầu tư - Quyền Viewer]
│   ├── Q1_Financial_Report.pdf
│   └── Progress_Report.pdf
└── 03_Vendor_Specs/           [Dành cho Đối tác thiết bị - Quyền Commenter]
    └── Hardware_Specifications.docx
```

## 2. Bảng phân quyền chi tiết (Access control Matrix)
| Thư mục / Tệp tin | Đối tượng | Mức quyền hạn | Biện pháp bảo mật & Ràng buộc nghiệp vụ |
| :--- | :--- | :---: | :--- |
| **Toàn bộ Dự án** | Trưởng nhóm cũ $\rightarrow$ Trưởng nhóm mới | **Owner** | Sử dụng tính năng **Transfer Ownership** để bàn giao toàn quyền sở hữu khi kết thúc bài tập nhóm theo đúng quy định. |
| **01_Sensor_Code** | Đội ngũ Kỹ thuật (Dev Team) | **Editor** | Cho phép chỉnh sửa mã nguồn, lập trình các tính năng cho cảm biến nông nghiệp. |
| **02_Investor_Reports**| Nhà đầu tư (Investors) | **Viewer** | **Chỉ xem báo cáo**, khóa toàn bộ tính năng tải xuống (Download), sao chép (Copy) và in ấn (Print) để tránh rò rỉ số liệu tài chính. |
| **03_Vendor_Specs** | Đối tác cung cấp thiết bị | **Commenter** | Chỉ cho phép xem và **bình luận góp ý** thông số kỹ thuật, không có quyền sửa đổi trực tiếp vào tài liệu gốc. |
| **.env** | Hệ thống chạy Local | **No Sync** | **Tuyệt đối không đẩy lên mạng/Cloud**. File này chứa mật khẩu cảm biến, phải đưa vào danh mục ẩn (`.gitignore` hoặc chặn đồng bộ) để tránh rò rỉ quyền quản trị phần cứng. |
---

## II. CẤU TRÚC KÊNH TRAO ĐỔI (CHANNELS) & QUY TRÌNH CHUYỂN ĐỔI BUG THÀNH TASK

Không gian làm việc số (Lark/Slack) của đội kỹ thuật Green-Tech được cấu trúc mạch lạc để tránh loãng thông tin và tối ưu hóa quy trình xử lý lỗi:

### 1. Kiến trúc các Kênh giao tiếp
*   `#green-tech-announcements`: Chỉ dùng để cập nhật thông báo quan trọng từ Trưởng dự án (Khóa quyền nhắn tin của thành viên).
*   `#green-tech-devs`: Không gian thảo luận kỹ thuật, review code và theo dõi hoạt động của cảm biến.
*   `#green-tech-bugs-report`: Kênh tiếp nhận và cô lập tất cả các thông báo báo lỗi phần cứng/phần mềm.

### 2. Quy trình chuyển đổi cuộc thảo luận lỗi thành Task có Deadline (Chức năng 3)
Khi phát hiện lỗi cảm biến trong kênh `#green-tech-bugs-report`, đội ngũ sẽ không trò chuyện lan man mà tuân thủ quy trình chuyển đổi bất đồng bộ sau: