# Bài 3: Quy trình Build và Push Image lên GitHub Container Registry (GHCR)

## Bước 1: Tạo Personal Access Token (PAT Classic) trên GitHub
- Truy cập: **GitHub -> Settings -> Developer settings -> Personal access tokens -> Tokens (classic) -> Generate new token (classic)**.
- Chọn tối thiểu các quyền (scopes):
  - `write:packages` (tự động bao gồm `read:packages` và `repo` nếu repo private)
  - `delete:packages` (tùy chọn để quản lý phiên bản)

## Bước 2: Đăng nhập GHCR qua Docker CLI (an toàn qua stdin)
```bash
export CR_PAT=<YOUR_GITHUB_PAT>
echo $CR_PAT | docker login ghcr.io -u ThinhBanTo --password-stdin
```

## Bước 3: Build và gắn tag chuẩn namespace GHCR (chữ thường)
```bash
# Build trực tiếp với tag chuẩn
docker build -t ghcr.io/thinhbanto/payment-service:1.0.0 .

# Hoặc gắn tag từ image có sẵn
docker tag payment-service:latest ghcr.io/thinhbanto/payment-service:1.0.0
```

## Bước 4: Push image lên GHCR
```bash
docker push ghcr.io/thinhbanto/payment-service:1.0.0
```
- Kiểm tra kết quả tại: `https://github.com/ThinhBanTo?tab=packages`
