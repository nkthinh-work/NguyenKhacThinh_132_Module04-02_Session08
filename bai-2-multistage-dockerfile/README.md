# Bài 2: Hoàn thiện Dockerfile Multi-stage Build (`cart-service`)

## Các phần đã hoàn thiện
1. `COPY . .`: Sao chép toàn bộ mã nguồn dự án và Gradle Wrapper vào thư mục `/app` của Stage 1.
2. `FROM eclipse-temurin:17-jre-alpine`: Sử dụng base image chỉ chứa JRE trên nền Alpine Linux siêu nhẹ thay vì cả bộ công cụ biên dịch JDK.
3. `COPY --from=builder /app/build/libs/*.jar app.jar`: Chỉ trích xuất file `.jar` thành phẩm từ Stage `builder` sang Stage runtime, loại bỏ hoàn toàn mã nguồn thô, Gradle cache và JDK.

## Lệnh build & so sánh dung lượng
```bash
# Build Multi-stage image
docker build -t cart-service:multistage .

# So sánh kích thước với base image JDK (eclipse-temurin:17-jdk-alpine ~ 326MB)
docker images
```
- **Kết quả kỳ vọng:** Image `cart-service:multistage` chỉ khoảng **115MB - 140MB** (giảm > 60% so với bản build trên JDK > 350MB).
