# Bài 3: Tối ưu tốc độ CI bằng Gradle Dependency Caching

## 1. Mục tiêu

Cấu hình Gradle Dependency Caching để giảm thời gian tải thư viện khi chạy CI trên GitHub Actions.

## 2. Cấu hình

Trong `.github/workflows/ci.yml`, sử dụng `actions/setup-java@v5` với các tham số:

- Java: 17
- Distribution: Temurin
- Cache: `gradle`

## 3. Kết quả lần chạy thứ nhất

- Trạng thái workflow: Success.
- Tổng thời gian Job: 52 giây.
- Trạng thái cache: `gradle cache is not found`.

## 4. Kết quả lần chạy thứ hai

Sẽ cập nhật thời gian thực tế và trạng thái cache sau khi workflow chạy lại.
