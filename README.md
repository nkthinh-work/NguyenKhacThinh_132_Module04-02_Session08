# Rikkei Education - Bài tập thực hành Docker & CI/CD

Cấu trúc thư mục tương ứng từng bài trong bộ PDF:
- `bai-1-dood/`: File `docker-compose.yml` mount `/var/run/docker.sock` và giải thích lỗi DooD.
- `bai-2-multistage-dockerfile/`: `Dockerfile` Multi-stage hoàn chỉnh cho `cart-service` (`eclipse-temurin:17-jdk-alpine` -> `17-jre-alpine`).
- `bai-3-ghcr-push/`: Các lệnh CLI tạo PAT, `docker login ghcr.io`, `docker tag` và `docker push` `payment-service:1.0.0`.
- `bai-4-ghcr-pull-ci/`: Workflow `.github/workflows/ci.yml` tự động login bằng `GITHUB_TOKEN`, chuyển lowercase owner và pull/verify image.
- `bai-5-cache-analysis/`: Báo cáo phân tích nguyên nhân mất Gradle cache (`.docx` và `.txt`) dùng để nộp trực tiếp lên Portal.
- `bai-6-delivery-service-repo/`: Dự án Spring Boot (`delivery-service`) đầy đủ mã nguồn + `Dockerfile` + `.github/workflows/main.yml`. Bạn có thể push riêng thư mục này lên 1 repo GitHub mới để Actions chạy xanh 100% và lấy link nộp bài 6.
- `bai-tong-hop-gitlab-cicd/`: `Dockerfile` (`gradle:8.5-jdk17-alpine` -> `eclipse-temurin:17-jre-alpine`) và `.gitlab-ci.yml` (3 stages: `test` kèm service `postgres:15-alpine`, `build_image`, `deploy`).
