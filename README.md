
# 🤖 MTAT STUDIO BASIC

<p align="center">
  <img src="https://img.shields.io/badge/version-1.0.0-blue?style=for-the-badge" />
  <img src="https://img.shields.io/badge/node-%3E%3D18.x-green?style=for-the-badge&logo=node.js" />
  <img src="https://img.shields.io/badge/license-MIT-yellow?style=for-the-badge" />
  <img src="https://img.shields.io/badge/status-active-brightgreen?style=for-the-badge" />
</p>

> Bot tự động hỗ trợ vận hành, quản lý và tương tác cho hệ thống **MTAT STUDIO** — nhanh chóng, ổn định, dễ triển khai.

---

## 📋 Mục lục

- [Yêu cầu hệ thống](#-yêu-cầu-hệ-thống)
- [Cài đặt](#-cài-đặt)
- [Cấu hình](#-cấu-hình)
- [Chạy bot](#-chạy-bot)
- [Cấu trúc thư mục](#-cấu-trúc-thư-mục)
- [Các lệnh hỗ trợ](#-các-lệnh-hỗ-trợ)
- [Cập nhật bot](#-cập-nhật-bot)
- [Xử lý lỗi thường gặp](#-xử-lý-lỗi-thường-gặp)
- [Đóng góp & Liên hệ](#-đóng-góp--liên-hệ)

---

## 💻 Yêu cầu hệ thống

| Thành phần | Phiên bản tối thiểu |
|---|---|
| Node.js | `>= 18.x` |
| npm | `>= 9.x` |
| Git | `>= 2.x` |
| Hệ điều hành | Windows 10 / Ubuntu 20.04 / macOS 12+ |
| RAM | 512 MB trở lên |

> ⚠️ **Lưu ý:** Khuyến nghị sử dụng **Node.js LTS** để đảm bảo ổn định nhất.

---

## 🚀 Cài đặt

### Bước 1 — Clone repository

```bash
git clone https://github.com/mtat-studio/mtat-studio-bot.git
cd mtat-studio-bot
```

### Bước 2 — Cài đặt dependencies

```bash
npm install
```

### Bước 3 — Sao chép file cấu hình mẫu

```bash
cp .env.example .env
```

### Bước 4 — Điền thông tin cấu hình vào `.env`

```bash
# Mở file .env bằng trình soạn thảo bất kỳ
nano .env       # Linux / macOS
notepad .env    # Windows
```

---

## ⚙️ Cấu hình

Chỉnh sửa file `.env` với các thông số sau:

```env
# ========================
# MTAT STUDIO BOT — CONFIG
# ========================

# Token bot (bắt buộc)
BOT_TOKEN=your_bot_token_here

# ID chủ sở hữu bot
OWNER_ID=your_owner_id_here

# Prefix lệnh (mặc định: !)
PREFIX=!

# Môi trường chạy: development | production
NODE_ENV=production

# Cổng server (nếu có webhook)
PORT=3000

# Cơ sở dữ liệu (tuỳ chọn)
DATABASE_URL=your_database_url_here

# Log level: error | warn | info | debug
LOG_LEVEL=info
```

> 🔒 **Bảo mật:** Tuyệt đối **không** chia sẻ file `.env` hoặc đưa lên GitHub. File này đã được thêm vào `.gitignore`.

---

## ▶️ Chạy bot

### Chế độ thông thường

```bash
npm start
```

### Chế độ phát triển (tự reload khi có thay đổi)

```bash
npm run dev
```

### Chạy nền với PM2 (khuyến nghị cho production)

```bash
# Cài PM2 toàn cục (chỉ cần làm 1 lần)
npm install -g pm2

# Khởi động bot
pm2 start npm --name "mtat-studio-bot" -- start

# Tự khởi động lại khi server reboot
pm2 startup
pm2 save
```

### Kiểm tra trạng thái bot (PM2)

```bash
pm2 status
pm2 logs mtat-studio-bot
```

---

## 📁 Cấu trúc thư mục

```
mtat-studio-bot/
├── src/
│   ├── commands/       # Các lệnh của bot
│   ├── events/         # Xử lý sự kiện
│   ├── handlers/       # Handler chính
│   ├── utils/          # Tiện ích & helper
│   └── index.js        # Điểm khởi chạy
├── config/
│   └── config.js       # Cấu hình mở rộng
├── logs/               # File log hệ thống
├── .env.example        # Mẫu cấu hình
├── .gitignore
├── package.json
└── README.md
```

---

## 📌 Các lệnh hỗ trợ

| Lệnh | Mô tả |
|---|---|
| `!help` | Hiển thị danh sách lệnh |
| `!ping` | Kiểm tra độ trễ của bot |
| `!info` | Thông tin phiên bản bot |
| `!reload` | Tải lại cấu hình (chỉ owner) |
| `!stop` | Tắt bot (chỉ owner) |

> 📝 Danh sách đầy đủ các lệnh có thể xem bằng `!help` sau khi bot đã chạy.

---

## 🔄 Cập nhật bot

```bash
# Kéo phiên bản mới nhất
git pull origin main

# Cài đặt lại dependencies (nếu có thay đổi)
npm install

# Khởi động lại bot (nếu dùng PM2)
pm2 restart mtat-studio-bot
```

---

## 🛠️ Xử lý lỗi thường gặp

**❌ Lỗi: `Cannot find module '...'`**
```bash
# Xoá node_modules và cài lại
rm -rf node_modules package-lock.json
npm install
```

**❌ Lỗi: `Invalid token` hoặc bot không kết nối được**
- Kiểm tra lại `BOT_TOKEN` trong file `.env`
- Đảm bảo token chưa bị thu hồi hoặc hết hạn

**❌ Lỗi: `Port already in use`**
```bash
# Tìm và kill process đang chiếm cổng (ví dụ cổng 3000)
lsof -ti:3000 | xargs kill -9    # Linux / macOS
netstat -ano | findstr :3000      # Windows
```

**❌ Bot chạy nhưng không phản hồi lệnh**
- Kiểm tra `PREFIX` trong `.env` có khớp với lệnh bạn gõ không
- Xem log lỗi: `pm2 logs mtat-studio-bot` hoặc `npm start`

---

## 🤝 Đóng góp & Liên hệ

Mọi đóng góp, báo lỗi hoặc góp ý xin vui lòng liên hệ:
- 📧 Email: `choao054@gmail.com`
- 💬 Discord: [MTAT STUDIO Server](MinhTri)
- 🐛 Facebook: [FACEBOOK ADMIN](https://www.facebook.com/ng.minh.tri.768741/)

---

<p align="center">
  Made with ❤️ by <strong>MTAT STUDIO</strong> &nbsp;•&nbsp; © 2025 All rights reserved.
</p>
