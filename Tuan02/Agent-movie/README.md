# AI Cinema - Telegram Movie Recommendation Bot

Chatbot Telegram thông minh sử dụng AI để gợi ý phim và trả lời các câu hỏi về phim đang chiếu.

## 📋 Mô tả

AI Cinema là một chatbot Telegram được xây dựng trên nền tảng n8n, tích hợp với:
- **TheMovieDB API**: Lấy thông tin phim đang chiếu
- **Groq AI (LLaMA 3.3 70B)**: Phân tích và đưa ra gợi ý phim thông minh
- **Telegram Bot**: Giao diện người dùng

## ✨ Tính năng

- 🎬 Gợi ý phim đang chiếp theo sở thích
- 🎭 Tìm phim theo thể loại (Kinh dị, Hài, Hành động, Tình cảm, Hoạt hình...)
- 📝 Review chi tiết về phim cụ thể
- 💬 Trò chuyện tự nhiên bằng tiếng Việt

## 🛠️ Yêu cầu hệ thống

- Docker Desktop
- Tài khoản Telegram
- API Key từ TheMovieDB
- (Tùy chọn) Ngrok hoặc công cụ tunneling khác để expose webhook

## 📦 Cài đặt

### Bước 1: Clone hoặc tải project

```powershell
cd Agent-movie
```

### Bước 2: Khởi động Docker

Đảm bảo Docker Desktop đang chạy, sau đó chạy lệnh:

```powershell
docker-compose up -d
```

### Bước 3: Truy cập n8n

Mở trình duyệt và truy cập:
```
http://localhost:5678
```

### Bước 4: Import workflow

1. Trong giao diện n8n, chọn **Import from File**
2. Chọn file `AI Cinema.json`
3. Workflow sẽ được import vào n8n

### Bước 5: Cấu hình Credentials

#### 5.1. Telegram Bot

1. Tạo bot mới với [@BotFather](https://t.me/botfather) trên Telegram:
   - Gửi lệnh `/newbot`
   - Đặt tên và username cho bot
   - Lưu lại **Bot Token**

2. Trong n8n:
   - Mở node **Telegram Trigger**
   - Thêm credential mới cho Telegram
   - Nhập Bot Token vừa tạo
   - Lưu lại

#### 5.2. Groq AI (LLaMA Model)

1. Đăng ký tài khoản tại [Groq Console](https://console.groq.com)
2. Tạo API Key
3. Trong n8n:
   - Mở node **Groq Chat Model**
   - Thêm credential mới
   - Nhập API Key
   - Lưu lại

#### 5.3. TheMovieDB API (Đã có sẵn)

API Key đã được cấu hình sẵn trong workflow. Nếu muốn thay đổi:
1. Đăng ký tại [TheMovieDB](https://www.themoviedb.org/)
2. Lấy API Key
3. Cập nhật trong node **HTTP Request**

### Bước 6: Cấu hình Webhook (Tùy chọn)

Nếu sử dụng Ngrok hoặc công cụ tunneling:

1. Chạy ngrok:
```powershell
ngrok http 5678
```

2. Copy URL từ ngrok (ví dụ: `https://abc123.ngrok-free.app`)

3. Cập nhật trong `docker-compose.yml`:
```yaml
environment:
  - WEBHOOK_URL=https://your-ngrok-url.ngrok-free.app
```

4. Khởi động lại Docker:
```powershell
docker-compose down
docker-compose up -d
```

### Bước 7: Kích hoạt Workflow

1. Trong n8n, mở workflow **AI Cinema**
2. Click nút **Active** để bật workflow
3. Workflow sẽ bắt đầu lắng nghe tin nhắn từ Telegram

## 🚀 Sử dụng

### Gửi tin nhắn cho bot:

**Gợi ý phim chung:**
```
Phim gì hay?
Có phim nào đáng xem không?
```

**Tìm phim theo thể loại:**
```
Tìm phim kinh dị
Có phim hài nào không?
Muốn xem phim hành động
Gợi ý phim tình cảm
```

**Hỏi chi tiết về phim:**
```
Review phim Mai
Nói rõ hơn về phim Đất Rừng Phương Nam
Nội dung phim này là gì?
```

## 🔧 Quản lý

### Xem logs

```powershell
docker-compose logs -f
```

### Dừng service

```powershell
docker-compose down
```

### Khởi động lại

```powershell
docker-compose restart
```

### Xóa dữ liệu và khởi động lại

```powershell
docker-compose down -v
docker-compose up -d
```

## 📁 Cấu trúc Project

```
Agent-movie/
├── AI Cinema.json          # n8n workflow file
├── docker-compose.yml      # Docker configuration
└── README.md              # Tài liệu hướng dẫn
```

## 🐛 Troubleshooting

### Bot không phản hồi

1. Kiểm tra workflow đã được **Active** chưa
2. Kiểm tra credentials Telegram đã được cấu hình đúng chưa
3. Xem logs: `docker-compose logs -f n8n`

### Lỗi kết nối API

1. Kiểm tra API Key của TheMovieDB và Groq
2. Kiểm tra kết nối internet
3. Kiểm tra webhook URL nếu sử dụng ngrok

### Docker không khởi động

1. Đảm bảo Docker Desktop đang chạy
2. Kiểm tra port 5678 có bị chiếm dụng không
3. Thử khởi động lại Docker Desktop

## 📝 Ghi chú

- Workflow sử dụng model **LLaMA 3.3 70B** từ Groq (miễn phí)
- Dữ liệu phim được cập nhật real-time từ TheMovieDB
- Bot hỗ trợ tiếng Việt
- Dữ liệu n8n được lưu trong Docker volume `n8n_data`

## 👥 Tác giả

- **Sinh viên**: [Tên của bạn]
- **MSSV**: 3122411218
- **Lớp**: DCT122C4
- **Môn học**: CNL THD

## 📄 License

Project này được tạo cho mục đích học tập.

---

**Chúc bạn thành công! 🎉**
