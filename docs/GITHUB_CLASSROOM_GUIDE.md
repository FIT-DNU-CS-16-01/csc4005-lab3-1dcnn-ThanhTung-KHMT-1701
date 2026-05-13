# Hướng dẫn GitHub Classroom cho Lab 3

## 1. Nhận assignment

1. Mở link GitHub Classroom do giảng viên cung cấp.
2. Chọn **Accept Assignment**.
3. Chờ hệ thống tạo repository cá nhân.

## 2. Clone repository

```bash
git clone <repo-url>
cd <ten-repo>
```

## 3. Làm bài và chạy kiểm tra

1. Chạy trong môi trường đã yêu cầu của môn học.
2. Không đưa dữ liệu UrbanSound8K (wav/zip) và thư mục cache lên GitHub.
3. Trước khi nộp, chạy kiểm tra local:

```bash
python ci/check_structure.py
python ci/smoke_train.py
```

## 4. Commit và push

```bash
git add .
git commit -m "Complete CSC4005 Lab3"
git push origin main
```

## 5. Checklist trước khi nộp

- Có run baseline MFCC + 1D-CNN.
- Có link W&B run hoặc project.
- Có `curves.png`, `confusion_matrix.png`, `metrics.json`.
- Có báo cáo đầy đủ theo mẫu.
- Cấu trúc repo không thiếu file bắt buộc.
