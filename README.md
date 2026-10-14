# Bài 1: Khởi tạo Workflow chạy Unit Test tự động cho Java Spring Boot với Gradle

## 1. Cấu trúc thư mục dự án

```text
Bai01/
├── .github/
│   └── workflows/
│       └── ci.yml               # Workflow GitHub Actions chạy Unit Test
├── gradle/
│   └── wrapper/
│       ├── gradle-wrapper.jar
│       └── gradle-wrapper.properties
├── src/
│   ├── main/
│   │   ├── java/com/example/demo/
│   │   │   ├── DemoApplication.java
│   │   │   └── service/
│   │   │       └── CalculatorService.java
│   │   └── resources/
│   │       └── application.properties
│   └── test/
│       └── java/com/example/demo/
│           ├── DemoApplicationTests.java
│           └── service/
│               └── CalculatorServiceTest.java
├── .gitignore
├── build.gradle
├── gradlew
├── gradlew.bat
└── settings.gradle
```

## 2. Chi tiết cấu hình Workflow (`.github/workflows/ci.yml`)

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

## 3. Các bước thực hiện & Kiểm tra

1. **Khởi tạo Git & Push lên GitHub:**
   ```bash
   git init
   git add .
   git commit -m "feat: setup Java Spring Boot Gradle project with CI workflow"
   git branch -M main
   git remote add origin <URL_REPOSITORY_CUA_BAN>
   git push -u origin main
   ```

2. **Kiểm tra trên GitHub Actions:**
   - Vào repository trên GitHub, chọn tab **Actions**.
   - Quan sát workflow **Java Spring Boot CI (Gradle)** được kích hoạt tự động từ sự kiện push lên nhánh `main`.
   - Kiểm tra Job **Run Unit Tests** hoàn thành thành công với trạng thái tích xanh (**Success**).
