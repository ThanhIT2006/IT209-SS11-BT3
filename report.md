# Bài 3: Tối ưu tốc độ CI bằng Gradle Dependency Caching

## 1. Mục tiêu

Cấu hình Gradle Dependency Caching bằng `cache: 'gradle'` trong `actions/setup-java@v5` để giảm thời gian tải thư viện khi chạy CI.

## 2. Cấu hình

- Java: 17
- Distribution: Temurin
- Cache: `gradle`
- Lệnh kiểm thử: `./gradlew test`

## 3. Kết quả thực nghiệm

| Thông tin | Lần chạy 1 | Lần chạy 2 |
|---|---|---|
| Tổng thời gian Job | 52 giây | Chưa ghi nhận riêng |
| Trạng thái cache đầu Job | Cache chưa được tìm thấy | Cache chưa được tìm thấy |
| Trạng thái cuối Job | Chưa ghi nhận | Cache đã lưu thành công |
| Gradle test | Chưa ghi nhận | Khoảng 40 giây theo log Job |

## 4. Kết luận

Workflow chạy thành công. Ở lần chạy thứ hai, GitHub Actions đã lưu thành công Gradle Wrapper cache và Gradle Dependencies cache. Cần xác minh việc khôi phục cache ở lần chạy tiếp theo để đánh giá hiệu quả tối ưu thời gian.