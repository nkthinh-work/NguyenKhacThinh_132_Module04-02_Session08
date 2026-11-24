# Bài 1: Sửa lỗi cấu hình chia sẻ Docker Socket (DooD)

## 1. Phân tích nguyên nhân gốc rễ (Root Cause)
- Lỗi `Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?` xảy ra vì Self-hosted Runner đang chạy bên trong một Docker container độc lập.
- Container Runner chỉ có Docker CLI (client) nhưng không chạy Docker Daemon riêng bên trong, đồng thời chưa được ánh xạ (mount) file UNIX domain socket `/var/run/docker.sock` từ máy chủ host. Do đó, mọi lệnh `docker build` hay `docker info` đều không thể giao tiếp với Docker Engine của máy host.

## 2. Giải pháp khắc phục (Mô hình DooD - Docker-outside-of-Docker)
- Ánh xạ trực tiếp socket từ host vào container trong `docker-compose.yml`:
  ```yaml
  volumes:
    - /var/run/docker.sock:/var/run/docker.sock
  ```
- Lưu ý trên Linux host: Nếu user chạy runner bên trong container không phải `root`, cần cấp quyền truy cập socket trên host (`sudo chmod 666 /var/run/docker.sock` hoặc thêm user vào nhóm `docker` qua `group_add`).

## 3. Lệnh khởi động lại & kiểm chứng
```bash
docker compose up -d --force-recreate
docker exec -it quickbite-self-hosted-runner docker info
```
