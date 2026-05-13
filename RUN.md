# Nhật ký chạy - CSC4005 Lab 3

## 1) Thông tin chung

- Đường dẫn dữ liệu: `data/UrbanSound8K`
- Môi trường sử dụng: `HocSau` (chạy bằng `conda run -n HocSau ...`)
- Mục tiêu đợt mới: chạy lại các cấu hình đã dùng với `--epochs 30`

## 2) Các lệnh đã chạy lại với 30 epochs

```bash
conda run -n HocSau python -m src.train --config configs/fast_debug.json --data_dir data/UrbanSound8K --epochs 30 --run_name 1771040029_debug_mfcc_1dcnn_e30

conda run -n HocSau python -m src.train --config configs/baseline_mfcc_1dcnn.json --data_dir data/UrbanSound8K --epochs 30 --run_name 1771040029_mfcc_1dcnn_baseline_e30

conda run -n HocSau python -m src.train --config configs/baseline_mfcc_1dcnn.json --feature_type logmel --data_dir data/UrbanSound8K --epochs 30 --run_name 1771040029_logmel_1dcnn_e30

conda run -n HocSau python -m src.train --config configs/extension_raw_waveform.json --data_dir data/UrbanSound8K --epochs 30 --run_name 1771040029_raw_waveform_extension_e30
```

## 3) Thống kê các cấu hình đã chạy

### 3.1 Đợt chạy trước

| Tên run | Cấu hình | feature_type | Epoch đã chạy | Best val acc | Test acc | Thời gian/epoch (s) | Thư mục output |
|---|---|---|---:|---:|---:|---:|---|
| debug_mfcc_1dcnn | fast_debug.json | mfcc | 3 | 0.3533 | 0.3467 | 12.3512 | outputs/debug_mfcc_1dcnn |
| 1771040029_mfcc_1dcnn_baseline | baseline_mfcc_1dcnn.json | mfcc | 8 | 0.5810 | 0.4688 | 7.1276 | outputs/1771040029_mfcc_1dcnn_baseline |
| 1771040029_logmel_1dcnn | baseline_mfcc_1dcnn.json (+feature_type=logmel) | logmel | 12 | 0.6177 | 0.5914 | 4.5464 | outputs/1771040029_logmel_1dcnn |
| 1771040029_raw_waveform_extension | extension_raw_waveform.json | raw | 15 | 0.5400 | 0.5871 | 9.3024 | outputs/1771040029_raw_waveform_extension |

### 3.2 Đợt chạy lại với epochs=30

| Tên run | Cấu hình | feature_type | Epoch yêu cầu | Epoch đã chạy | Best val acc | Test acc | Thời gian/epoch (s) | W&B |
|---|---|---|---:|---:|---:|---:|---:|---|
| 1771040029_debug_mfcc_1dcnn_e30 | fast_debug.json | mfcc | 30 | 8 | 0.4267 | 0.3933 | 0.5349 | https://wandb.ai/thanhtung-contact-official-/csc4005-lab3-urbansound-1dcnn/runs/dx0k7zt7 |
| 1771040029_mfcc_1dcnn_baseline_e30 | baseline_mfcc_1dcnn.json | mfcc | 30 | 8 | 0.5810 | 0.4688 | 1.7950 | https://wandb.ai/thanhtung-contact-official-/csc4005-lab3-urbansound-1dcnn/runs/yk6rb6l1 |
| 1771040029_logmel_1dcnn_e30 | baseline_mfcc_1dcnn.json (+feature_type=logmel) | logmel | 30 | 12 | 0.6177 | 0.5914 | 2.1733 | https://wandb.ai/thanhtung-contact-official-/csc4005-lab3-urbansound-1dcnn/runs/fqhalgyo |
| 1771040029_raw_waveform_extension_e30 | extension_raw_waveform.json | raw | 30 | 19 | 0.5248 | 0.5699 | 6.9136 | https://wandb.ai/thanhtung-contact-official-/csc4005-lab3-urbansound-1dcnn/runs/ao2oo2tn |

## 4) Nhận xét nhanh

- Tất cả cấu hình đã được chạy lại với tham số `--epochs 30` thành công.
- Số epoch thực tế đều nhỏ hơn 30 vì cơ chế early stopping dừng sớm khi không còn cải thiện validation loss.
- Ở đợt e30, run có test acc cao nhất là `1771040029_logmel_1dcnn_e30` (0.5914).
- `1771040029_raw_waveform_extension_e30` có thời gian train/epoch cao hơn đáng kể so với MFCC/log-mel.

## 5) Artefact có sẵn cho mỗi run

Mỗi run trong `outputs/<run_name>/` đều có các file:

- `best_model.pt`
- `history.csv`
- `curves.png`
- `confusion_matrix.png`
- `metrics.json`
- `used_config.json`
