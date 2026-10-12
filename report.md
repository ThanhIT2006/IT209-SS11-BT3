# Bài 3: Tối ưu tốc độ CI bằng Gradle Dependency Caching

## 1. Mục tiêu

Cấu hình GitHub Actions sử dụng Gradle Dependency Caching nhằm giảm thời gian chạy CI cho dự án Java Spring Boot sử dụng Gradle.

## 2. Cấu hình workflow

Workflow được đặt tại `.github/workflows/ci.yml`, sử dụng:

- `actions/checkout@v4`: tải mã nguồn.
- `actions/setup-java@v5`: thiết lập JDK 17 Temurin.
- `cache: 'gradle'`: bật cơ chế lưu và khôi phục Gradle cache.
- `./gradlew test`: thực thi kiểm thử tự động.

## 3. Kết quả thực nghiệm

| Lần chạy | Commit | Thời gian chạy test | Kết quả |
|---|---|---:|---|
| #1 | `b21d6c0` | 38 giây | Thành công |
| #2 | `e14a920` | 16 giây | Thành công |
| #3 | `c8c2fee` | 17 giây | Thành công |

Ở lần chạy đầu tiên, Gradle Wrapper phải tải Gradle 9.7.1. Ở lần chạy mới nhất, Gradle cache đã được khôi phục thành công.

## 4. Đánh giá

So với lần chạy đầu tiên, lần chạy thứ ba giảm từ 38 giây xuống 17 giây, tiết kiệm 21 giây, tương đương khoảng 55,3%.

Kết quả cho thấy thời gian chạy Gradle giảm ở các lần chạy sau. Tuy nhiên, mức cải thiện không chỉ đến từ Dependency Caching mà còn có thể liên quan đến việc không phải tải lại Gradle Wrapper và quá trình khởi tạo Gradle.

