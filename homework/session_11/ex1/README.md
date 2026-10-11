# Báo Cáo Bài Tập 1: Khởi Tạo Workflow Chạy Unit Test Cho Java Spring Boot Với Gradle

## 1. Thông Tin Bài Nộp
- **Bài tập**: Bài 1 - Khởi tạo Workflow chạy Unit Test tự động cho Java Spring Boot với Gradle
- **Thư mục bài nộp**: `homework/session_11/ex1/`
- **Sản phẩm bàn giao**:
  1. Tệp cấu hình workflow: [ci.yml](file:///d:/IT209/Session11_b1/homework/session_11/ex1/ci.yml) (và [.github/workflows/ci.yml](file:///d:/IT209/Session11_b1/.github/workflows/ci.yml))
  2. Ảnh chụp màn hình kết quả chạy thành công: [github_actions_success.png](file:///d:/IT209/Session11_b1/homework/session_11/ex1/github_actions_success.png)

---

## 2. Nội Dung Kịch Bản CI (`ci.yml`)

```yaml
name: Java Spring Boot CI (Gradle)

on:
  push:
    branches: [ "main" ]

jobs:
  test:
    name: Run Unit Tests
    runs-on: ubuntu-latest

    steps:
      - name: Checkout mã nguồn
        uses: actions/checkout@v5

      - name: Thiết lập môi trường Java JDK 17
        uses: actions/setup-java@v5
        with:
          java-version: '17'
          distribution: 'temurin'

      - name: Cấp quyền cho Gradle Wrapper
        run: chmod +x gradlew

      - name: Thực thi JUnit Test với Gradle
        run: ./gradlew test
```

---

## 3. Giải Thích Các Thành Phần Trong Workflow

| Thành phần | Ý nghĩa / Chức năng |
| :--- | :--- |
| `name: Java Spring Boot CI (Gradle)` | Tên hiển thị của GitHub Actions Workflow trên giao diện Repository. |
| `on.push.branches: [ "main" ]` | Kích hoạt tự động pipeline CI mỗi khi có commit mới được push lên nhánh `main`. |
| `runs-on: ubuntu-latest` | Môi trường máy ảo runner thực thi job (Ubuntu phiên bản mới nhất do GitHub cấp). |
| `actions/checkout@v5` | Tải toàn bộ mã nguồn của repository về thư mục làm việc của runner. |
| `actions/setup-java@v5` | Cài đặt và cấu hình Java Development Kit phiên bản 17 với bản phân phối Temurin (Adoptium). |
| `chmod +x gradlew` | Cấp quyền thực thi (`execute`) cho tệp script Gradle Wrapper để runner có thể chạy `./gradlew`. |
| `./gradlew test` | Lệnh biên dịch và chạy toàn bộ các bài kiểm thử đơn vị (JUnit Tests) của dự án Spring Boot. |

---

## 4. Kết Quả Kiểm Thử (GitHub Actions Success)

Job `Run Unit Tests` thực thi hoàn tất với trạng thái tích xanh (**Success ✓**):
- Đã checkout mã nguồn thành công.
- Đã cấu hình môi trường Java JDK 17 (Temurin).
- Cấp quyền thực thi Gradle Wrapper thành công.
- JUnit Test chạy thành công (`BUILD SUCCESSFUL`, `4 actionable tasks: 4 executed`).
