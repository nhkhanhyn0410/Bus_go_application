# CLAUDE.md - Dự án Bus_Go (Java Backend + Android App - Monorepo)

## Tổng quan dự án

**Bus_Go** (VeXeNhanh) là nền tảng đặt vé xe khách trực tuyến toàn diện. Hiện đang trong giai đoạn lập kế hoạch kiến trúc với thiết kế hệ thống và cơ sở dữ liệu đã hoàn thành.

**Cấu trúc dự án**: Monorepo - Backend và Android App trong cùng 1 repository

## Chiến lược phát triển theo độ ưu tiên

### Giai đoạn 1: Customer App (Ưu tiên cao nhất) 
- **Platform:** Android App
- **Mục tiêu:** Cho phép khách hàng tìm kiếm, đặt vé và quản lý chuyến đi
- **Timeline:** Phase 1-7 (Core MVP)

### Giai đoạn 2: Driver App (Ưu tiên thứ hai) 
- **Platform:** Android App
- **Mục tiêu:** Hỗ trợ tài xế cập nhật vị trí, quản lý chuyến đi, check-in hành khách
- **Timeline:** Phase 8 (Song song với Operator Dashboard)

### Giai đoạn 3: Operator & Admin Dashboard (Ưu tiên thứ ba) 
- **Platform:** Web Dashboard (React/Vue hoặc Spring MVC + Thymeleaf)
- **Mục tiêu:** Quản lý hệ thống cho nhà xe và admin
- **Timeline:** Phase 9-10

## Công nghệ sử dụng

### Backend (Java)
- **Framework:** Spring Boot 3.2.x
- **Java Version:** Java 17 LTS
- **Build Tool:** Maven 3.9.x
- **Cơ sở dữ liệu:** MySQL 8.0 / PostgreSQL 15.x
- **ORM:** Spring Data JPA (Hibernate)
- **Cache/Session:** Redis 7.x (Spring Data Redis)
- **Message Queue:** RabbitMQ 3.x / Kafka 3.x
- **Security:** Spring Security 6.x + JWT
- **API Documentation:** SpringDoc OpenAPI 3.x (Swagger)
- **Real-time:** WebSocket (Spring WebSocket + STOMP)

### Mobile (Android)
- **Language:** Java 11+
- **Min SDK:** Android 8.0 (API 26)
- **Target SDK:** Android 14 (API 34)
- **Architecture:** MVVM (Model-View-ViewModel)
- **DI:** Dagger 2 / Hilt
- **Network:** Retrofit 2.x + OkHttp
- **Async:** RxJava 3.x
- **Local DB:** Room Database
- **Image Loading:** Glide 4.x
- **Navigation:** Navigation Component
- **UI:** Material Design 3

### Dịch vụ bên thứ ba
- Firebase Auth (OAuth), FCM (Push Notifications)
- Thanh toán: VNPay, MoMo, ZaloPay
- SMS: Twilio/ESMS, Email: SendGrid/AWS SES
- Bản đồ: Google Maps Android API
- CDN: Cloudinary / AWS S3

---

## Cấu trúc Monorepo (Backend + Android trong 1 project)

```
Bus_go_app_java/                           # Root project
├── backend/                               # Backend module (Spring Boot)
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/
│   │   │   │   └── com/
│   │   │   │       └── busgo/
│   │   │   │           ├── BusGoApplication.java          # Main class
│   │   │   │           │
│   │   │   │           ├── config/                        # Configuration
│   │   │   │           │   ├── SecurityConfig.java
│   │   │   │           │   ├── WebConfig.java
│   │   │   │           │   ├── RedisConfig.java
│   │   │   │           │   ├── WebSocketConfig.java
│   │   │   │           │   ├── OpenApiConfig.java         # Swagger config
│   │   │   │           │   └── AsyncConfig.java
│   │   │   │           │
│   │   │   │           ├── entity/                        # JPA Entities
│   │   │   │           │   ├── User.java
│   │   │   │           │   ├── BusOperator.java
│   │   │   │           │   ├── Bus.java
│   │   │   │           │   ├── Route.java
│   │   │   │           │   ├── Trip.java
│   │   │   │           │   ├── Booking.java
│   │   │   │           │   ├── Payment.java
│   │   │   │           │   ├── Ticket.java
│   │   │   │           │   └── ...
│   │   │   │           │
│   │   │   │           ├── repository/                    # Spring Data JPA Repositories
│   │   │   │           │   ├── UserRepository.java
│   │   │   │           │   ├── TripRepository.java
│   │   │   │           │   ├── BookingRepository.java
│   │   │   │           │   └── ...
│   │   │   │           │
│   │   │   │           ├── dto/                           # Data Transfer Objects
│   │   │   │           │   ├── request/
│   │   │   │           │   │   ├── LoginRequest.java
│   │   │   │           │   │   ├── RegisterRequest.java
│   │   │   │           │   │   ├── BookingRequest.java
│   │   │   │           │   │   └── ...
│   │   │   │           │   └── response/
│   │   │   │           │       ├── UserResponse.java
│   │   │   │           │       ├── TripResponse.java
│   │   │   │           │       ├── BookingResponse.java
│   │   │   │           │       └── ApiResponse.java       # Generic wrapper
│   │   │   │           │
│   │   │   │           ├── service/                       # Business Logic Layer
│   │   │   │           │   ├── AuthService.java
│   │   │   │           │   ├── UserService.java
│   │   │   │           │   ├── TripService.java
│   │   │   │           │   ├── BookingService.java
│   │   │   │           │   ├── PaymentService.java
│   │   │   │           │   ├── NotificationService.java
│   │   │   │           │   └── ...
│   │   │   │           │
│   │   │   │           ├── serviceimpl/                   # Service Implementations
│   │   │   │           │   ├── AuthServiceImpl.java
│   │   │   │           │   ├── UserServiceImpl.java
│   │   │   │           │   ├── TripServiceImpl.java
│   │   │   │           │   └── ...
│   │   │   │           │
│   │   │   │           ├── controller/                    # REST Controllers
│   │   │   │           │   ├── AuthController.java
│   │   │   │           │   ├── UserController.java
│   │   │   │           │   ├── TripController.java
│   │   │   │           │   ├── BookingController.java
│   │   │   │           │   ├── PaymentController.java
│   │   │   │           │   └── ...
│   │   │   │           │
│   │   │   │           ├── security/                      # Security Components
│   │   │   │           │   ├── JwtTokenProvider.java
│   │   │   │           │   ├── JwtAuthenticationFilter.java
│   │   │   │           │   ├── UserDetailsServiceImpl.java
│   │   │   │           │   └── UserPrincipal.java
│   │   │   │           │
│   │   │   │           ├── validation/                    # Custom Validators
│   │   │   │           │   ├── PhoneValidator.java
│   │   │   │           │   ├── BookingValidator.java
│   │   │   │           │   └── ...
│   │   │   │           │
│   │   │   │           ├── exception/                     # Exception Handling
│   │   │   │           │   ├── GlobalExceptionHandler.java
│   │   │   │           │   ├── BusinessException.java
│   │   │   │           │   ├── ResourceNotFoundException.java
│   │   │   │           │   ├── ValidationException.java
│   │   │   │           │   └── ErrorCode.java             # Error codes enum
│   │   │   │           │
│   │   │   │           ├── util/                          # Utility Classes
│   │   │   │           │   ├── DateUtils.java
│   │   │   │           │   ├── StringUtils.java
│   │   │   │           │   ├── QRCodeGenerator.java
│   │   │   │           │   ├── SeatMapGenerator.java
│   │   │   │           │   └── ...
│   │   │   │           │
│   │   │   │           ├── websocket/                     # WebSocket Handlers
│   │   │   │           │   ├── TripTrackingHandler.java
│   │   │   │           │   ├── NotificationHandler.java
│   │   │   │           │   └── ...
│   │   │   │           │
│   │   │   │           ├── scheduler/                     # Scheduled Jobs
│   │   │   │           │   ├── BookingExpirationScheduler.java
│   │   │   │           │   ├── TripReminderScheduler.java
│   │   │   │           │   └── SeatReleaseScheduler.java
│   │   │   │           │
│   │   │   │           └── integration/                   # External Service Integration
│   │   │   │               ├── payment/
│   │   │   │               │   ├── VNPayService.java
│   │   │   │               │   ├── MoMoService.java
│   │   │   │               │   └── ZaloPayService.java
│   │   │   │               ├── sms/
│   │   │   │               │   └── TwilioService.java
│   │   │   │               ├── email/
│   │   │   │               │   └── SendGridService.java
│   │   │   │               └── firebase/
│   │   │   │                   └── FirebaseMessagingService.java
│   │   │   │
│   │   │   └── resources/
│   │   │       ├── application.yml                        # Main config
│   │   │       ├── application-dev.yml                    # Dev profile
│   │   │       ├── application-prod.yml                   # Production profile
│   │   │       ├── application-test.yml                   # Test profile
│   │   │       ├── db/
│   │   │       │   └── migration/                         # Flyway/Liquibase migrations
│   │   │       │       ├── V1__create_users_table.sql
│   │   │       │       ├── V2__create_trips_table.sql
│   │   │       │       └── ...
│   │   │       ├── static/
│   │   │       └── templates/
│   │   │
│   │   └── test/
│   │       └── java/
│   │           └── com/
│   │               └── busgo/
│   │                   ├── service/
│   │                   │   ├── AuthServiceTest.java
│   │                   │   └── ...
│   │                   ├── controller/
│   │                   │   ├── AuthControllerTest.java
│   │                   │   └── ...
│   │                   └── integration/
│   │                       └── BookingFlowIntegrationTest.java
│   │
│   ├── pom.xml                                            # Backend Maven config
│   ├── Dockerfile                                         # Backend Docker
│   └── README.md
│
├── android-customer-app/                                  # Customer Android App (Priority 1)
│   ├── app/
│   │   ├── src/
│   │   │   ├── main/
│   │   │   │   ├── java/
│   │   │   │   │   └── com/
│   │   │   │   │       └── busgo/
│   │   │   │   │           ├── BusGoApplication.java      # Application class
│   │   │   │   │           │
│   │   │   │   │           ├── ui/                        # Activity / Fragment
│   │   │   │   │           │   ├── auth/
│   │   │   │   │           │   │   ├── LoginActivity.java
│   │   │   │   │           │   │   ├── RegisterActivity.java
│   │   │   │   │           │   │   └── OTPActivity.java
│   │   │   │   │           │   ├── main/
│   │   │   │   │           │   │   ├── MainActivity.java
│   │   │   │   │           │   │   └── MainFragment.java
│   │   │   │   │           │   ├── home/
│   │   │   │   │           │   │   └── HomeFragment.java
│   │   │   │   │           │   ├── search/
│   │   │   │   │           │   │   ├── SearchResultActivity.java
│   │   │   │   │           │   │   └── FilterBottomSheet.java
│   │   │   │   │           │   ├── trip/
│   │   │   │   │           │   │   ├── TripDetailActivity.java
│   │   │   │   │           │   │   └── SeatSelectionActivity.java
│   │   │   │   │           │   ├── booking/
│   │   │   │   │           │   │   ├── BookingActivity.java
│   │   │   │   │           │   │   ├── PassengerInfoActivity.java
│   │   │   │   │           │   │   └── BookingSummaryActivity.java
│   │   │   │   │           │   ├── payment/
│   │   │   │   │           │   │   ├── PaymentActivity.java
│   │   │   │   │           │   │   └── PaymentResultActivity.java
│   │   │   │   │           │   ├── ticket/
│   │   │   │   │           │   │   ├── MyTicketsFragment.java
│   │   │   │   │           │   │   ├── TicketDetailActivity.java
│   │   │   │   │           │   │   └── QRCodeDialogFragment.java
│   │   │   │   │           │   ├── tracking/
│   │   │   │   │           │   │   └── TripTrackingActivity.java
│   │   │   │   │           │   ├── profile/
│   │   │   │   │           │   │   ├── ProfileFragment.java
│   │   │   │   │           │   │   └── EditProfileActivity.java
│   │   │   │   │           │   ├── wallet/
│   │   │   │   │           │   │   ├── WalletActivity.java
│   │   │   │   │           │   │   └── TopUpActivity.java
│   │   │   │   │           │   └── notification/
│   │   │   │   │           │       └── NotificationsFragment.java
│   │   │   │   │           │
│   │   │   │   │           ├── viewmodel/                 # ViewModels
│   │   │   │   │           │   ├── AuthViewModel.java
│   │   │   │   │           │   ├── TripViewModel.java
│   │   │   │   │           │   ├── BookingViewModel.java
│   │   │   │   │           │   ├── PaymentViewModel.java
│   │   │   │   │           │   ├── TicketViewModel.java
│   │   │   │   │           │   └── ...
│   │   │   │   │           │
│   │   │   │   │           ├── model/                     # Data Models (DTOs)
│   │   │   │   │           │   ├── User.java
│   │   │   │   │           │   ├── Trip.java
│   │   │   │   │           │   ├── Booking.java
│   │   │   │   │           │   ├── Ticket.java
│   │   │   │   │           │   ├── ApiResponse.java
│   │   │   │   │           │   └── ...
│   │   │   │   │           │
│   │   │   │   │           ├── network/                   # Network Layer
│   │   │   │   │           │   ├── ApiService.java        # Retrofit interface
│   │   │   │   │           │   ├── ApiClient.java         # Retrofit builder
│   │   │   │   │           │   ├── AuthInterceptor.java   # JWT interceptor
│   │   │   │   │           │   └── NetworkHelper.java
│   │   │   │   │           │
│   │   │   │   │           ├── repository/                # Data Repository Layer
│   │   │   │   │           │   ├── AuthRepository.java
│   │   │   │   │           │   ├── TripRepository.java
│   │   │   │   │           │   ├── BookingRepository.java
│   │   │   │   │           │   └── ...
│   │   │   │   │           │
│   │   │   │   │           ├── database/                  # Room Database
│   │   │   │   │           │   ├── AppDatabase.java
│   │   │   │   │           │   ├── dao/
│   │   │   │   │           │   │   ├── UserDao.java
│   │   │   │   │           │   │   ├── TicketDao.java
│   │   │   │   │           │   │   └── ...
│   │   │   │   │           │   └── entity/
│   │   │   │   │           │       ├── UserEntity.java
│   │   │   │   │           │       ├── TicketEntity.java
│   │   │   │   │           │       └── ...
│   │   │   │   │           │
│   │   │   │   │           ├── adapter/                   # RecyclerView Adapters
│   │   │   │   │           │   ├── TripAdapter.java
│   │   │   │   │           │   ├── TicketAdapter.java
│   │   │   │   │           │   ├── SeatAdapter.java
│   │   │   │   │           │   └── ...
│   │   │   │   │           │
│   │   │   │   │           ├── util/                      # Utility Classes
│   │   │   │   │           │   ├── DateUtils.java
│   │   │   │   │           │   ├── CurrencyUtils.java
│   │   │   │   │           │   ├── ValidationUtils.java
│   │   │   │   │           │   ├── PermissionUtils.java
│   │   │   │   │           │   └── Constants.java
│   │   │   │   │           │
│   │   │   │   │           ├── widget/                    # Custom Views
│   │   │   │   │           │   ├── SeatMapView.java
│   │   │   │   │           │   ├── CustomSearchView.java
│   │   │   │   │           │   └── ...
│   │   │   │   │           │
│   │   │   │   │           ├── service/                   # Background Services
│   │   │   │   │           │   ├── LocationTrackingService.java
│   │   │   │   │           │   └── FCMService.java        # Firebase Messaging
│   │   │   │   │           │
│   │   │   │   │           └── di/                        # Dependency Injection (Hilt)
│   │   │   │   │               ├── AppModule.java
│   │   │   │   │               ├── NetworkModule.java
│   │   │   │   │               └── DatabaseModule.java
│   │   │   │   │
│   │   │   │   ├── res/
│   │   │   │   │   ├── layout/                            # XML layouts
│   │   │   │   │   ├── drawable/                          # Images, icons
│   │   │   │   │   ├── values/
│   │   │   │   │   │   ├── strings.xml
│   │   │   │   │   │   ├── colors.xml
│   │   │   │   │   │   ├── styles.xml
│   │   │   │   │   │   └── dimens.xml
│   │   │   │   │   ├── navigation/                        # Navigation graphs
│   │   │   │   │   └── menu/                              # Menu resources
│   │   │   │   │
│   │   │   │   └── AndroidManifest.xml
│   │   │   │
│   │   │   └── test/
│   │   │       └── java/
│   │   │
│   │   ├── build.gradle                                   # App-level Gradle
│   │   └── proguard-rules.pro
│   │
│   ├── build.gradle                                       # Project-level Gradle
│   ├── settings.gradle
│   └── gradle.properties
│
├── android-driver-app/                                   # Driver Android App (Priority 2)
│   ├── app/
│   │   ├── src/
│   │   │   ├── main/
│   │   │   │   ├── java/
│   │   │   │   │   └── com/
│   │   │   │   │       └── busgo/
│   │   │   │   │           └── driver/
│   │   │   │   │               ├── BusGoDriverApplication.java
│   │   │   │   │               │
│   │   │   │   │               ├── ui/                        # Activities & Fragments
│   │   │   │   │               │   ├── auth/
│   │   │   │   │               │   │   ├── LoginActivity.java
│   │   │   │   │               │   │   └── DriverVerificationActivity.java
│   │   │   │   │               │   ├── main/
│   │   │   │   │               │   │   ├── MainActivity.java
│   │   │   │   │               │   │   ├── DashboardFragment.java
│   │   │   │   │               │   │   ├── TripListFragment.java
│   │   │   │   │               │   │   └── ProfileFragment.java
│   │   │   │   │               │   ├── trip/
│   │   │   │   │               │   │   ├── TripDetailActivity.java
│   │   │   │   │               │   │   ├── StartTripActivity.java
│   │   │   │   │               │   │   ├── NavigationActivity.java
│   │   │   │   │               │   │   └── PassengerListActivity.java
│   │   │   │   │               │   ├── checkin/
│   │   │   │   │               │   │   ├── QRScannerActivity.java
│   │   │   │   │               │   │   └── ManualCheckinActivity.java
│   │   │   │   │               │   └── earnings/
│   │   │   │   │               │       ├── EarningsActivity.java
│   │   │   │   │               │       └── TripHistoryActivity.java
│   │   │   │   │               │
│   │   │   │   │               ├── viewmodel/
│   │   │   │   │               │   ├── TripViewModel.java
│   │   │   │   │               │   ├── NavigationViewModel.java
│   │   │   │   │               │   └── CheckinViewModel.java
│   │   │   │   │               │
│   │   │   │   │               ├── service/
│   │   │   │   │               │   ├── LocationTrackingService.java
│   │   │   │   │               │   └── FCMService.java
│   │   │   │   │               │
│   │   │   │   │               ├── model/
│   │   │   │   │               ├── network/
│   │   │   │   │               ├── repository/
│   │   │   │   │               ├── database/
│   │   │   │   │               ├── util/
│   │   │   │   │               └── di/
│   │   │   │   │
│   │   │   │   ├── res/
│   │   │   │   └── AndroidManifest.xml
│   │   │   │
│   │   │   └── test/
│   │   │
│   │   ├── build.gradle
│   │   └── proguard-rules.pro
│   │
│   ├── build.gradle
│   ├── settings.gradle
│   └── gradle.properties
│
├── web-dashboard/                                        # Web Dashboard (Priority 3)
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/
│   │   │   │   └── com/
│   │   │   │       └── busgo/
│   │   │   │           └── dashboard/
│   │   │   │               ├── controller/
│   │   │   │               │   ├── DashboardController.java
│   │   │   │               │   ├── OperatorController.java
│   │   │   │               │   ├── AdminController.java
│   │   │   │               │   └── ReportController.java
│   │   │   │               ├── service/
│   │   │   │               └── dto/
│   │   │   │
│   │   │   ├── resources/
│   │   │   │   ├── static/
│   │   │   │   │   ├── css/
│   │   │   │   │   ├── js/
│   │   │   │   │   └── images/
│   │   │   │   └── templates/                          # Thymeleaf templates
│   │   │   │       ├── operator/
│   │   │   │       │   ├── dashboard.html
│   │   │   │       │   ├── trips.html
│   │   │   │       │   ├── buses.html
│   │   │   │       │   └── bookings.html
│   │   │   │       └── admin/
│   │   │   │           ├── dashboard.html
│   │   │   │           ├── operators.html
│   │   │   │           ├── users.html
│   │   │   │           └── reports.html
│   │   │   │
│   │   │   └── application.yml
│   │   │
│   │   └── test/
│   │
│   └── pom.xml
│
├── shared/                                                # Shared DTOs (Optional)
│   └── src/
│       └── main/
│           └── java/
│               └── com/
│                   └── busgo/
│                       └── dto/                            # DTOs dùng chung
│                           ├── UserDto.java
│                           ├── TripDto.java
│                           ├── BookingDto.java
│                           └── ...
│
├── docker-compose.yml                                     # Docker services (MySQL, Redis, RabbitMQ)
├── .gitignore                                             # Git ignore cho cả backend và android
├── README.md                                              # Root README
└── CLAUDE.md                                              # File này
```

---

## Ưu điểm của cấu trúc Monorepo

### Advantages

1. **Quản lý dễ dàng hơn**
   - Chỉ 1 repository duy nhất
   - Git history đồng bộ giữa backend và frontend
   - Dễ dàng track changes liên quan đến cả 2 phía

2. **Chia sẻ code**
   - DTOs có thể share giữa backend và android (trong thư mục `shared/`)
   - Constants, enums, error codes có thể tái sử dụng

3. **Development thuận tiện**
   - Mở 1 project trong IDE có thể code cả backend và android
   - Dễ dàng test end-to-end
   - API contract changes được sync ngay

4. **CI/CD đơn giản**
   - Chỉ cần setup 1 pipeline duy nhất
   - Build cả backend và android trong 1 workflow

5. **Versioning thống nhất**
   - Backend và Android app có cùng version
   - Dễ quản lý releases

### Lưu ý

- Project size sẽ lớn hơn
- Clone time lâu hơn
- IDE có thể lag nếu máy yếu
- Cần cấu hình Git ignore cẩn thận

---

## Cấu hình Backend
---

## Workflow Development

### 1. Setup Project

```bash
# Clone repository
git https://github.com/nhkhanhyn0410/Bus_go_application.git
cd Bus_go_application

# Start database services
docker-compose up -d mysql redis rabbitmq

# Start backend
cd backend
mvn spring-boot:run

# Open Android app in Android Studio
# File -> Open -> Bus_go_app_java/android-app
```

### 2. Development Workflow

**Backend Development:**
```bash
cd backend
mvn spring-boot:run -Dspring-boot.run.profiles=dev
```

**Android Development:**
```bash
cd android-app
./gradlew assembleDebug
./gradlew installDebug
```

**Both together:**
- Terminal 1: Run backend
- Android Studio: Open android-app và run

### 3. Testing

**Backend Tests:**
```bash
cd backend
mvn test
```

**Android Tests:**
```bash
cd android-app
./gradlew test
./gradlew connectedAndroidTest
```

### 4. Build for Production

**Backend:**
```bash
cd backend
mvn clean package
docker build -t busgo-backend:1.0.0 .
```

**Android:**
```bash
cd android-app
./gradlew bundleRelease
```

---

---

## Danh sách màn hình theo ứng dụng

---

## A. Customer Android App (Ưu tiên 1) 

### 1. Authentication Flow (Auth)
- **SplashActivity** - Màn hình chào
- **LoginActivity** - Đăng nhập
- **RegisterActivity** - Đăng ký tài khoản
- **OTPActivity** - Xác thực OTP
- **ForgotPasswordActivity** - Quên mật khẩu
- **ResetPasswordActivity** - Đặt lại mật khẩu

### 2. Main Navigation
- **MainActivity** - Activity chính với Bottom Navigation
  - **HomeFragment** - Trang chủ
  - **MyTicketsFragment** - Vé của tôi
  - **NotificationsFragment** - Thông báo
  - **ProfileFragment** - Tài khoản

### 3. Home & Search Flow
- **HomeFragment** - Trang chủ với tìm kiếm nhanh
- **SearchActivity** - Tìm kiếm chi tiết
- **SearchResultActivity** - Kết quả tìm kiếm
- **FilterBottomSheet** - Bộ lọc tìm kiếm
- **SortBottomSheet** - Sắp xếp kết quả

### 4. Trip & Booking Flow
- **TripListActivity** - Danh sách chuyến xe
- **TripDetailActivity** - Chi tiết chuyến xe
- **SeatSelectionActivity** - Chọn ghế
- **PickupDropoffActivity** - Chọn điểm đón/trả
- **PassengerInfoActivity** - Thông tin hành khách
- **BookingSummaryActivity** - Tóm tắt đặt vé
- **ContactInfoActivity** - Thông tin liên hệ

### 5. Payment Flow
- **PaymentMethodActivity** - Chọn phương thức thanh toán
- **PaymentActivity** - Thanh toán
- **PaymentProcessingActivity** - Xử lý thanh toán
- **PaymentResultActivity** - Kết quả thanh toán
- **PaymentHistoryActivity** - Lịch sử thanh toán

### 6. Ticket Management
- **MyTicketsFragment** - Danh sách vé của tôi
- **TicketDetailActivity** - Chi tiết vé
- **QRCodeDialogFragment** - Mã QR vé
- **TicketCancellationActivity** - Hủy vé
- **RefundActivity** - Hoàn tiền
- **RescheduleActivity** - Đổi lịch

### 7. Trip Tracking
- **TripTrackingActivity** - Theo dõi chuyến xe realtime
- **BusLocationMapActivity** - Bản đồ vị trí xe
- **TripTimelineActivity** - Lịch trình chuyến đi

### 8. User Profile & Settings
- **ProfileFragment** - Trang cá nhân
- **EditProfileActivity** - Chỉnh sửa thông tin
- **ChangePasswordActivity** - Đổi mật khẩu
- **VerifyPhoneActivity** - Xác thực số điện thoại
- **VerifyEmailActivity** - Xác thực email
- **SettingsActivity** - Cài đặt
- **NotificationSettingsActivity** - Cài đặt thông báo
- **LanguageSettingsActivity** - Ngôn ngữ
- **BiometricSettingsActivity** - Sinh trắc học

### 9. Wallet & Promotions
- **WalletActivity** - Ví điện tử
- **TopUpActivity** - Nạp tiền
- **WithdrawActivity** - Rút tiền
- **TransactionHistoryActivity** - Lịch sử giao dịch
- **PromotionsActivity** - Khuyến mãi
- **VoucherActivity** - Mã giảm giá
- **LoyaltyPointsActivity** - Điểm thưởng
- **RewardsActivity** - Phần thưởng

### 10. Reviews & Support
- **WriteReviewActivity** - Viết đánh giá
- **ReviewsListActivity** - Danh sách đánh giá
- **HelpCenterActivity** - Trung tâm trợ giúp
- **FAQActivity** - Câu hỏi thường gặp
- **ContactSupportActivity** - Liên hệ hỗ trợ
- **ChatSupportActivity** - Chat với hỗ trợ
- **ReportIssueActivity** - Báo cáo sự cố

### 11. Additional Features
- **SavedRoutesActivity** - Tuyến đường yêu thích
- **PassengerManagementActivity** - Quản lý hành khách thường đi
- **TravelHistoryActivity** - Lịch sử đi lại
- **AboutActivity** - Về chúng tôi
- **TermsActivity** - Điều khoản sử dụng
- **PrivacyPolicyActivity** - Chính sách bảo mật

---

## B. Driver Android App (Ưu tiên 2) 

### 1. Authentication & Profile
- **SplashActivity** - Màn hình chào
- **LoginActivity** - Đăng nhập tài xế
- **DriverVerificationActivity** - Xác thực tài xế (Giấy phép lái xe, CMND)
- **ProfileActivity** - Thông tin tài xế
- **EditProfileActivity** - Chỉnh sửa thông tin
- **DocumentsActivity** - Quản lý giấy tờ
- **ChangePasswordActivity** - Đổi mật khẩu

### 2. Main Dashboard
- **MainActivity** - Activity chính với Bottom Navigation
  - **DashboardFragment** - Tổng quan (Thu nhập hôm nay, chuyến tiếp theo)
  - **TripListFragment** - Danh sách chuyến được phân công
  - **EarningsFragment** - Thu nhập
  - **ProfileFragment** - Tài khoản tài xế

### 3. Trip Management
- **TripDetailActivity** - Chi tiết chuyến xe được phân công
- **StartTripActivity** - Bắt đầu chuyến đi (Checklist trước khởi hành)
- **OngoingTripActivity** - Chuyến đang di chuyển
- **NavigationActivity** - Dẫn đường GPS
- **PassengerListActivity** - Danh sách hành khách
- **TripCompletionActivity** - Hoàn thành chuyến
- **TripHistoryActivity** - Lịch sử chuyến đã hoàn thành

### 4. Passenger Check-in
- **QRScannerActivity** - Quét mã QR vé
- **ManualCheckinActivity** - Check-in thủ công (bằng mã vé)
- **PassengerSearchActivity** - Tìm kiếm hành khách
- **NoShowReportActivity** - Báo cáo hành khách không lên xe

### 5. Location & Navigation
- **LiveTrackingActivity** - Theo dõi vị trí realtime
- **RouteMapActivity** - Bản đồ lộ trình
- **NextStopActivity** - Điểm dừng tiếp theo
- **TrafficAlertsActivity** - Cảnh báo giao thông

### 6. Earnings & Reports
- **EarningsActivity** - Tổng thu nhập
- **DailyEarningsActivity** - Thu nhập theo ngày
- **WeeklyEarningsActivity** - Thu nhập theo tuần
- **MonthlyEarningsActivity** - Thu nhập theo tháng
- **WithdrawalActivity** - Rút tiền
- **BonusActivity** - Thưởng & khuyến khích

### 7. Communication
- **ChatWithOperatorActivity** - Chat với nhà xe
- **CallOperatorActivity** - Gọi điện thoại nhà xe
- **EmergencyContactActivity** - Liên hệ khẩn cấp
- **AnnouncementsActivity** - Thông báo từ nhà xe

### 8. Vehicle & Maintenance
- **VehicleInfoActivity** - Thông tin xe được phân công
- **VehicleInspectionActivity** - Kiểm tra xe (Checklist)
- **MaintenanceHistoryActivity** - Lịch sử bảo dưỡng
- **ReportIssueActivity** - Báo cáo sự cố xe

### 9. Help & Support
- **HelpCenterActivity** - Trung tâm trợ giúp
- **FAQActivity** - Câu hỏi thường gặp
- **ContactSupportActivity** - Liên hệ hỗ trợ
- **GuidelinesActivity** - Hướng dẫn tài xế
- **SafetyProtocolsActivity** - Quy định an toàn

### 10. Settings
- **SettingsActivity** - Cài đặt
- **NotificationSettingsActivity** - Cài đặt thông báo
- **LocationSettingsActivity** - Cài đặt định vị
- **LanguageSettingsActivity** - Ngôn ngữ
- **PrivacySettingsActivity** - Quyền riêng tư

---

## C. Web Dashboard (Operator & Admin) (Ưu tiên 3) 💻

### Operator Dashboard Pages

#### 1. Dashboard & Overview
- **Dashboard** - Tổng quan (Thống kê hôm nay, biểu đồ)
- **Quick Actions** - Hành động nhanh (Tạo chuyến, xem đặt vé)

#### 2. Trip Management
- **Trips List** - Danh sách tất cả chuyến xe
- **Create Trip** - Tạo chuyến xe mới
- **Edit Trip** - Chỉnh sửa chuyến xe
- **Trip Schedule** - Lịch trình chuyến xe (Calendar view)
- **Recurring Trips** - Chuyến định kỳ
- **Cancel Trip** - Hủy chuyến

#### 3. Bus Management
- **Buses List** - Danh sách xe
- **Add Bus** - Thêm xe mới
- **Edit Bus** - Chỉnh sửa thông tin xe
- **Seat Layout** - Thiết lập sơ đồ ghế
- **Bus Status** - Trạng thái xe (Available, In Use, Maintenance)
- **Maintenance Schedule** - Lịch bảo dưỡng

#### 4. Route Management
- **Routes List** - Danh sách tuyến đường
- **Create Route** - Tạo tuyến mới
- **Edit Route** - Chỉnh sửa tuyến
- **Stops Management** - Quản lý điểm dừng
- **Pricing** - Thiết lập giá theo quãng đường

#### 5. Driver Management
- **Drivers List** - Danh sách tài xế
- **Add Driver** - Thêm tài xế mới
- **Edit Driver** - Chỉnh sửa thông tin tài xế
- **Assign Driver** - Phân công tài xế cho chuyến
- **Driver Performance** - Đánh giá tài xế
- **Documents Verification** - Xác minh giấy tờ

#### 6. Booking Management
- **Bookings List** - Danh sách đặt vé (Realtime)
- **Booking Details** - Chi tiết đặt vé
- **Confirm/Reject Booking** - Xác nhận/Từ chối
- **Passenger List** - Danh sách hành khách theo chuyến
- **Check-in Status** - Trạng thái check-in
- **Refund Management** - Quản lý hoàn tiền

#### 7. Revenue & Reports
- **Revenue Dashboard** - Tổng quan doanh thu
- **Daily Revenue** - Doanh thu theo ngày
- **Monthly Revenue** - Doanh thu theo tháng
- **Trip Performance** - Hiệu suất chuyến xe
- **Seat Occupancy** - Tỷ lệ lấp đầy ghế
- **Export Reports** - Xuất báo cáo (Excel/PDF)

#### 8. Promotions & Discounts
- **Promotions List** - Danh sách khuyến mãi
- **Create Promotion** - Tạo khuyến mãi
- **Vouchers** - Quản lý mã giảm giá
- **Seasonal Offers** - Ưu đãi theo mùa

#### 9. Reviews & Ratings
- **Reviews List** - Danh sách đánh giá
- **Respond to Reviews** - Phản hồi đánh giá
- **Rating Analytics** - Phân tích đánh giá
- **Reported Issues** - Vấn đề được báo cáo

#### 10. Settings
- **Operator Profile** - Thông tin nhà xe
- **Business Information** - Thông tin kinh doanh
- **Policies** - Chính sách (Hủy vé, Hoàn tiền)
- **Payment Settings** - Cài đặt thanh toán
- **Notification Settings** - Cài đặt thông báo

---

### Admin Dashboard Pages

#### 1. System Dashboard
- **Overview** - Tổng quan hệ thống
- **System Health** - Tình trạng hệ thống
- **Active Users** - Người dùng đang hoạt động
- **Real-time Statistics** - Thống kê realtime

#### 2. Operator Management
- **Operators List** - Danh sách nhà xe
- **Pending Approvals** - Chờ duyệt
- **Verify Operator** - Xác minh nhà xe
- **Operator Details** - Chi tiết nhà xe
- **Commission Settings** - Cài đặt hoa hồng
- **Suspend/Activate** - Tạm ngưng/Kích hoạt

#### 3. User Management
- **All Users** - Tất cả người dùng
- **Customers** - Khách hàng
- **Drivers** - Tài xế
- **User Details** - Chi tiết người dùng
- **Activity Logs** - Nhật ký hoạt động
- **Block/Unblock User** - Khóa/Mở khóa

#### 4. System Configuration
- **General Settings** - Cài đặt chung
- **Payment Gateways** - Cổng thanh toán
- **Email Templates** - Mẫu email
- **SMS Templates** - Mẫu SMS
- **Push Notification Templates** - Mẫu thông báo
- **Fee Configuration** - Cấu hình phí

#### 5. Content Management
- **FAQ Management** - Quản lý FAQ
- **Terms & Conditions** - Điều khoản
- **Privacy Policy** - Chính sách bảo mật
- **Help Center Content** - Nội dung trợ giúp
- **Announcements** - Thông báo hệ thống

#### 6. System Reports
- **Revenue Reports** - Báo cáo doanh thu
- **Transaction Reports** - Báo cáo giao dịch
- **User Growth** - Tăng trưởng người dùng
- **Booking Statistics** - Thống kê đặt vé
- **Top Operators** - Nhà xe hàng đầu
- **Top Routes** - Tuyến phổ biến

#### 7. System Promotions
- **System-wide Promotions** - Khuyến mãi toàn hệ thống
- **Flash Sales** - Flash sale
- **Loyalty Programs** - Chương trình khách hàng thân thiết
- **Referral Management** - Quản lý giới thiệu

#### 8. Monitoring & Logs
- **Error Logs** - Nhật ký lỗi
- **API Logs** - Nhật ký API
- **Payment Logs** - Nhật ký thanh toán
- **User Activity** - Hoạt động người dùng
- **System Performance** - Hiệu suất hệ thống

#### 9. Backup & Security
- **Database Backup** - Sao lưu database
- **System Backup** - Sao lưu hệ thống
- **Restore** - Khôi phục
- **Security Settings** - Cài đặt bảo mật
- **Audit Trail** - Kiểm toán

#### 10. Admin Settings
- **Admin Users** - Người dùng admin
- **Role Management** - Quản lý vai trò
- **Permissions** - Phân quyền
- **Two-Factor Authentication** - Xác thực 2 lớp

---

## Chức năng chính của hệ thống

### A. Chức năng Khách hàng (Customer Features)

#### 1. Xác thực & Tài khoản
- Đăng ký/Đăng nhập (Email, SĐT, Google, Facebook)
- Xác thực OTP qua SMS/Email
- Quên mật khẩu & đặt lại
- Đăng nhập sinh trắc học (FaceID/Fingerprint)
- Quản lý profile (Avatar, thông tin cá nhân)
- Xác thực 2 lớp (2FA)

#### 2. Tìm kiếm & Đặt vé
- Tìm kiếm chuyến xe theo tuyến, ngày giờ
- Lọc theo giá, loại xe, nhà xe, tiện nghi
- Sắp xếp kết quả (giá, giờ, đánh giá)
- Xem chi tiết chuyến xe (lịch trình, tiện nghi, chính sách)
- Chọn ghế/giường trực quan (Sơ đồ ghế tương tác)
- Chọn điểm đón/trả tùy chỉnh
- Nhập thông tin hành khách
- Áp dụng mã giảm giá/voucher
- Lưu hành khách thường đi
- Đặt vé cho nhiều người

#### 3. Thanh toán
- Thanh toán VNPay, MoMo, ZaloPay
- Thanh toán bằng ví BusGo
- Thanh toán tại văn phòng
- Lưu phương thức thanh toán
- Thanh toán tự động cho vé thường xuyên
- Lịch sử thanh toán
- Hóa đơn điện tử

#### 4. Quản lý vé
- Danh sách vé (Upcoming, Completed, Cancelled)
- Chi tiết vé với QR Code
- Tải vé về điện thoại
- Chia sẻ vé qua Email/SMS
- Hủy vé & hoàn tiền
- Đổi lịch chuyến
- Chuyển vé cho người khác
- In vé điện tử

#### 5. Theo dõi chuyến xe
- Theo dõi vị trí xe realtime trên bản đồ
- Ước tính thời gian đến
- Nhận thông báo khi xe sắp đến
- Xem lịch trình chi tiết
- Thông tin tài xế & xe
- Gọi điện cho tài xế/nhà xe

#### 6. Ví điện tử & Khuyến mãi
- Ví BusGo (Nạp/Rút tiền)
- Tích điểm thưởng
- Đổi điểm lấy voucher
- Nhận khuyến mãi theo độ thân thiết
- Flash sale & ưu đãi đặc biệt
- Giới thiệu bạn bè nhận thưởng
- Cashback

#### 7. Đánh giá & Hỗ trợ
- Đánh giá chuyến xe (Sao, bình luận)
- Đánh giá tài xế
- Xem đánh giá của người khác
- Báo cáo sự cố
- Chat với support
- FAQ & Help Center
- Gọi hotline

#### 8. Tính năng tiện ích
- Lưu tuyến đường yêu thích
- Lịch sử đi lại
- Thông báo push (Khuyến mãi, nhắc nhở, cập nhật)
- Dark mode
- Đa ngôn ngữ (VI/EN)
- Offline mode (Xem vé đã tải)

### B. Chức năng Nhà xe (Bus Operator Features)

#### 1. Quản lý chuyến xe
- Tạo/Sửa/Xóa chuyến xe
- Thiết lập lịch trình tự động
- Quản lý giá vé theo mùa
- Thiết lập chính sách hủy vé
- Tạo khuyến mãi cho chuyến cụ thể
- Dừng bán vé tạm thời

#### 2. Quản lý xe & tài xế
- Thêm/Sửa thông tin xe (biển số, loại xe, sơ đồ ghế)
- Quản lý tài xế (thông tin, giấy phép)
- Phân công tài xế cho chuyến
- Theo dõi trạng thái xe
- Lịch bảo dưỡng xe

#### 3. Quản lý đặt vé
- Xem danh sách đặt vé realtime
- Xác nhận/Từ chối đặt vé
- Hoàn vé cho khách
- Check-in hành khách (Quét QR)
- Danh sách hành khách theo chuyến

#### 4. Báo cáo & Thống kê
- Doanh thu theo ngày/tháng/năm
- Tỷ lệ lấp đầy ghế
- Top chuyến xe bán chạy
- Đánh giá từ khách hàng
- Xuất báo cáo Excel/PDF

#### 5. Quản lý tuyến đường
- Tạo/Sửa tuyến đường
- Thiết lập điểm dừng
- Cập nhật giá theo quãng đường

### C. Chức năng Tài xế (Driver Features)

#### 1. Xác thực & Tài khoản
- Đăng nhập tài xế (Email/SĐT + Password)
- Xác thực giấy tờ (Giấy phép lái xe, CMND, Bằng lái)
- Quản lý profile tài xế
- Cập nhật thông tin cá nhân
- Quản lý giấy tờ (Upload, gia hạn)
- Đổi mật khẩu

#### 2. Quản lý chuyến xe
- Xem danh sách chuyến được phân công
- Chi tiết chuyến xe (Thời gian, tuyến đường, xe)
- Bắt đầu chuyến đi
- Kết thúc chuyến đi
- Lịch sử chuyến đã hoàn thành
- Danh sách hành khách
- Checklist trước khởi hành

#### 3. Check-in hành khách
- Quét mã QR vé
- Check-in thủ công (nhập mã vé)
- Tìm kiếm hành khách
- Xác nhận đón khách
- Báo cáo hành khách không lên xe (No-show)
- Trạng thái check-in realtime

#### 4. Định vị & Dẫn đường
- GPS tracking realtime
- Cập nhật vị trí tự động
- Dẫn đường theo route
- Điểm dừng tiếp theo
- ETA (Estimated Time of Arrival)
- Cảnh báo giao thông

#### 5. Thu nhập & Thống kê
- Xem thu nhập hôm nay
- Thu nhập theo tuần/tháng
- Lịch sử thu nhập
- Thưởng & khuyến khích
- Rút tiền
- Chi tiết thanh toán

#### 6. Quản lý xe
- Xem thông tin xe được phân công
- Checklist kiểm tra xe
- Báo cáo sự cố xe
- Lịch sử bảo dưỡng
- Yêu cầu bảo trì

#### 7. Giao tiếp
- Chat với nhà xe
- Gọi điện cho dispatcher
- Liên hệ khẩn cấp
- Nhận thông báo từ nhà xe
- Thông báo về chuyến mới

#### 8. Hỗ trợ
- Trung tâm trợ giúp
- FAQ
- Hướng dẫn tài xế
- Quy định an toàn
- Báo cáo sự cố

---

### D. Chức năng Admin (System Admin Features)

#### 1. Quản lý người dùng
- Danh sách người dùng (Customer, Operator, Admin)
- Khóa/Mở khóa tài khoản
- Phân quyền
- Xem lịch sử hoạt động

#### 2. Quản lý nhà xe
- Duyệt/Từ chối đăng ký nhà xe
- Xác minh tài liệu
- Quản lý hoa hồng
- Theo dõi doanh thu hệ thống

#### 3. Quản lý hệ thống
- Cấu hình hệ thống
- Quản lý phương thức thanh toán
- Quản lý khuyến mãi toàn hệ thống
- Quản lý nội dung (FAQ, Điều khoản)
- Monitor logs & errors
- Backup & restore

#### 4. Báo cáo tổng hợp
- Tổng doanh thu hệ thống
- Số lượng vé bán ra
- Thống kê người dùng
- Tỷ lệ hủy vé
- Top nhà xe

---

## Lộ trình xây dựng hệ thống (Development Roadmap)

### Phase 1: Foundation & Setup (2-3 tuần)

#### Backend Setup
- [ ] Tạo cấu trúc project Spring Boot
- [ ] Cấu hình database (MySQL + Flyway migrations)
- [ ] Setup Redis cache
- [ ] Setup RabbitMQ
- [ ] Cấu hình Spring Security + JWT
- [ ] Setup Swagger/OpenAPI documentation
- [ ] Tạo base entities (BaseEntity, Auditable)
- [ ] Global exception handling
- [ ] Response wrapper standardization

#### Android App Setup
- [ ] Tạo cấu trúc project Android
- [ ] Setup Hilt dependency injection
- [ ] Cấu hình Retrofit + OkHttp
- [ ] Setup Room database
- [ ] Base classes (BaseActivity, BaseFragment, BaseViewModel)
- [ ] Navigation component setup
- [ ] Material Design theme configuration
- [ ] Utility classes (DateUtils, CurrencyUtils, etc.)

#### Infrastructure
- [ ] Development environment documentation

**Deliverables:**
- Project structure hoàn chỉnh
- Base setup cho cả Backend và Android
- Sample API endpoint + Android screen kết nối thành công

---

### Phase 2: Authentication & User Management (2 tuần)

#### Backend
- [ ] User entity & repository
- [ ] Role & Permission entities
- [ ] JWT token generation & validation
- [ ] Login API (Email/Phone + Password)
- [ ] Register API with OTP verification
- [ ] Forgot password flow
- [ ] Refresh token mechanism
- [ ] Firebase Authentication integration
- [ ] Social login (Google, Facebook)
- [ ] Profile management APIs

#### Android
- [ ] Splash screen
- [ ] Onboarding screens
- [ ] Login screen
- [ ] Register screen
- [ ] OTP verification screen
- [ ] Forgot password flow
- [ ] Token storage (SharedPreferences/DataStore)
- [ ] Auth interceptor for API calls
- [ ] Profile screen
- [ ] Edit profile screen
- [ ] Change password screen

#### Testing
- [ ] Unit tests cho auth services
- [ ] Integration tests cho auth flow
- [ ] Android UI tests cho login/register

**Deliverables:**
- Complete authentication system
- User có thể đăng ký, đăng nhập, quản lý profile
- Token-based authorization working end-to-end

---

### Phase 3: Core Business Logic - Trip & Booking (3-4 tuần)

#### Backend Entities & Repositories
- [ ] BusOperator entity & repository
- [ ] Bus entity (với sơ đồ ghế)
- [ ] Route entity (tuyến đường)
- [ ] Trip entity (chuyến xe)
- [ ] Seat entity
- [ ] Booking entity
- [ ] Ticket entity
- [ ] Passenger entity

#### Backend APIs
- [ ] Trip search API (filters, sorting, pagination)
- [ ] Trip detail API
- [ ] Available seats API
- [ ] Seat hold/lock mechanism (Redis)
- [ ] Create booking API
- [ ] Booking validation
- [ ] Cancel booking API
- [ ] Get booking list/detail APIs
- [ ] Trip schedule management APIs (for operators)

#### Android
- [ ] Home screen với search widget
- [ ] Search screen
- [ ] Search results with filters
- [ ] Trip detail screen
- [ ] Seat selection screen (Interactive seat map)
- [ ] Pickup/dropoff selection
- [ ] Passenger info form
- [ ] Booking summary screen
- [ ] My tickets screen
- [ ] Ticket detail screen với QR code
- [ ] Custom SeatMapView widget

#### Business Logic
- [ ] Seat availability checking
- [ ] Seat hold timeout (15 phút)
- [ ] Price calculation
- [ ] Booking validation rules
- [ ] Cancellation policy enforcement

**Deliverables:**
- Customers có thể tìm chuyến xe, chọn ghế, tạo booking
- Interactive seat map hoạt động mượt mà
- Booking được lưu vào database
- Xem danh sách và chi tiết booking

---

### Phase 4: Payment Integration (2 tuần)

#### Backend
- [ ] Payment entity & repository
- [ ] VNPay integration
- [ ] MoMo integration
- [ ] ZaloPay integration
- [ ] Payment webhook handlers
- [ ] Payment verification
- [ ] Refund processing
- [ ] Wallet entity & APIs
- [ ] Transaction history APIs

#### Android
- [ ] Payment method selection screen
- [ ] Payment processing screen
- [ ] WebView for payment gateways
- [ ] Payment result screen
- [ ] Wallet screen
- [ ] Top-up screen
- [ ] Transaction history screen
- [ ] Payment retry mechanism

#### Testing
- [ ] Payment gateway sandbox testing
- [ ] Refund flow testing
- [ ] Transaction consistency tests

**Deliverables:**
- Complete payment integration với 3 payment gateways
- Thanh toán thành công → ticket được issue
- Hoàn tiền working properly
- Ví điện tử functional

---

### Phase 5: Real-time Tracking & Notifications (2 tuần)

#### Backend
- [ ] WebSocket configuration
- [ ] Trip location tracking service
- [ ] Location update API (từ driver app)
- [ ] ETA calculation
- [ ] Firebase Cloud Messaging setup
- [ ] Notification entity & repository
- [ ] Notification service (Email, SMS, Push)
- [ ] Notification templates
- [ ] Scheduled notifications (nhắc nhở trước chuyến)

#### Android
- [ ] Trip tracking screen với Google Maps
- [ ] Real-time location updates via WebSocket
- [ ] FCM integration
- [ ] Notification handler
- [ ] Notification settings screen
- [ ] In-app notification list
- [ ] Deep linking từ notifications

#### Scheduled Jobs
- [ ] Booking expiration scheduler
- [ ] Trip reminder scheduler (2h trước chuyến)
- [ ] Seat release scheduler
- [ ] Payment timeout scheduler

**Deliverables:**
- Real-time tracking hoạt động trên bản đồ
- Push notifications cho các events quan trọng
- Email/SMS notifications
- Scheduled jobs running correctly

---

### Phase 6: Promotions & Loyalty Program (2 tuần)

#### Backend
- [ ] Promotion entity & repository
- [ ] Voucher entity
- [ ] LoyaltyPoints entity
- [ ] Promotion service
- [ ] Apply voucher logic
- [ ] Loyalty points calculation
- [ ] Referral program
- [ ] Cashback mechanism
- [ ] Flash sale support

#### Android
- [ ] Promotions screen
- [ ] Voucher list screen
- [ ] Apply voucher in booking flow
- [ ] Loyalty points screen
- [ ] Rewards screen
- [ ] Referral screen
- [ ] Promotion banners in home screen

**Deliverables:**
- Voucher system working
- Loyalty points accumulation
- Referral program functional
- Flash sales can be created and applied

---

### Phase 7: Reviews & Support (1-2 tuần)

#### Backend
- [ ] Review entity & repository
- [ ] Rating system
- [ ] Review moderation APIs
- [ ] Support ticket entity
- [ ] Help center content APIs
- [ ] FAQ management

#### Android
- [ ] Write review screen
- [ ] Reviews list screen
- [ ] Help center screen
- [ ] FAQ screen
- [ ] Contact support screen
- [ ] Chat support (basic)
- [ ] Report issue screen

**Deliverables:**
- Review system hoạt động
- Help center & FAQ accessible
- Support ticketing system

---

### Phase 8: Driver App Development (2-3 tuần)

#### Backend APIs for Driver
- [ ] Driver entity & repository
- [ ] Driver authentication APIs
- [ ] Driver verification APIs (Documents)
- [ ] Assigned trips APIs (Get trips for driver)
- [ ] Start/End trip APIs
- [ ] Location update API (Realtime GPS)
- [ ] Check-in passenger API (QR scan, Manual)
- [ ] Trip status update APIs
- [ ] Driver earnings APIs
- [ ] Driver notification APIs

#### Driver Android App
- [ ] Authentication flow (Login, Verification)
- [ ] Dashboard fragment (Today's earnings, Next trip)
- [ ] Trip list fragment
- [ ] Trip detail screen
- [ ] Start trip screen (Checklist)
- [ ] Navigation screen với Google Maps
- [ ] QR scanner for check-in
- [ ] Manual check-in screen
- [ ] Passenger list screen
- [ ] Earnings screen
- [ ] Trip completion screen
- [ ] Profile & documents screen

#### Location Tracking
- [ ] Background location service
- [ ] Auto location updates to server
- [ ] Route navigation
- [ ] Next stop notifications

**Deliverables:**
- Driver có thể login và verify documents
- Xem chuyến được phân công
- Start/End trip functionality
- QR check-in hành khách working
- Realtime GPS tracking
- Xem thu nhập

---

### Phase 9: Web Dashboard (Operator & Admin) (3-4 tuần)

#### Backend APIs for Dashboard
- [ ] Operator management APIs
- [ ] Trip management APIs (CRUD)
- [ ] Bus management APIs (CRUD)
- [ ] Route management APIs (CRUD)
- [ ] Driver management APIs (CRUD)
- [ ] Revenue report APIs
- [ ] Booking management APIs
- [ ] System configuration APIs
- [ ] Admin management APIs
- [ ] System-wide reports APIs
- [ ] Content management APIs (FAQ, Terms)

#### Web Dashboard (Spring MVC + Thymeleaf)
**Operator Features:**
- [ ] Operator login & dashboard
- [ ] Trips management (Create, Edit, Delete, Schedule)
- [ ] Buses management (Add, Edit, Seat layout)
- [ ] Routes management (Create, Edit, Stops)
- [ ] Drivers management (Add, Assign, Performance)
- [ ] Bookings list & management (Realtime)
- [ ] Revenue dashboard & reports
- [ ] Promotions & vouchers
- [ ] Reviews & ratings
- [ ] Settings & policies

**Admin Features:**
- [ ] Admin login & dashboard
- [ ] System overview (Statistics, Health)
- [ ] Operator management (Approve, Verify, Commission)
- [ ] User management (Customers, Drivers, Block/Unblock)
- [ ] System configuration (Payment gateways, Fees)
- [ ] Content management (FAQ, Terms, Help center)
- [ ] System reports (Revenue, Users, Bookings)
- [ ] System promotions & loyalty programs
- [ ] Monitoring & logs (Errors, API, Payments)
- [ ] Backup & security

#### Frontend (Thymeleaf + Bootstrap)
- [ ] Responsive layout
- [ ] Dashboard charts (Chart.js)
- [ ] Data tables với pagination & search
- [ ] Forms validation
- [ ] Modal dialogs
- [ ] Toast notifications
- [ ] Date pickers
- [ ] File upload components

**Deliverables:**
- Operator có thể quản lý toàn bộ operations
- Admin có thể quản lý hệ thống
- Web dashboard responsive và user-friendly
- Reports & analytics functional

---

### Phase 10: Testing, Optimization & Launch Prep (2-3 tuần)

#### Testing
- [ ] Comprehensive unit tests (Backend)
- [ ] Integration tests (Backend)
- [ ] API contract tests
- [ ] Android unit tests
- [ ] Android UI tests
- [ ] End-to-end testing
- [ ] Performance testing
- [ ] Load testing
- [ ] Security testing (OWASP)

#### Optimization
- [ ] Database indexing
- [ ] Query optimization
- [ ] Redis caching optimization
- [ ] API response time optimization
- [ ] Android app size optimization
- [ ] Image optimization
- [ ] ProGuard/R8 configuration

#### Documentation
- [ ] API documentation (Swagger)
- [ ] User manual
- [ ] Operator manual
- [ ] Admin manual
- [ ] Deployment guide
- [ ] Troubleshooting guide

#### DevOps
- [ ] Production environment setup
- [ ] CI/CD pipeline completion
- [ ] Monitoring setup (Prometheus/Grafana)
- [ ] Logging setup (ELK Stack)
- [ ] Backup strategy
- [ ] Disaster recovery plan

#### Launch Preparation
- [ ] Beta testing với real users
- [ ] Bug fixes from beta
- [ ] Performance tuning
- [ ] Security audit
- [ ] Play Store submission preparation
- [ ] Marketing materials

**Deliverables:**
- Production-ready application
- Comprehensive test coverage
- Documentation complete
- App submitted to Play Store
- Backend deployed to production

---

### Phase 11: Post-Launch & Maintenance

#### Monitoring & Support
- [ ] Monitor server health
- [ ] Monitor app crashes
- [ ] User feedback collection
- [ ] Bug tracking & fixes
- [ ] Performance monitoring

#### Enhancements
- [ ] Feature improvements based on feedback
- [ ] A/B testing for key features
- [ ] New payment methods
- [ ] Additional languages
- [ ] Advanced analytics

#### Marketing Features
- [ ] Push notification campaigns
- [ ] In-app messaging
- [ ] Seasonal promotions
- [ ] Partnership integrations

**Deliverables:**
- Stable production system
- Continuous improvement based on metrics
- Growing user base

---

## Ước tính thời gian tổng thể

| Phase | Duration | Team Size | Priority |
|-------|----------|-----------|----------|
| Phase 1: Foundation | 2-3 tuần | 2-3 devs |  |
| Phase 2: Authentication | 2 tuần | 2 devs |  |
| Phase 3: Core Business Logic | 3-4 tuần | 3-4 devs |  |
| Phase 4: Payment | 2 tuần | 2 devs |  |
| Phase 5: Real-time & Notifications | 2 tuần | 2 devs |  |
| Phase 6: Promotions & Loyalty | 2 tuần | 1-2 devs |  |
| Phase 7: Reviews & Support | 1-2 tuần | 1-2 devs |  |
| **CUSTOMER APP MVP** | **16-20 tuần** | | **DONE** |
| Phase 8: Driver App | 2-3 tuần | 2 devs |  |
| Phase 9: Web Dashboard | 3-4 tuần | 2-3 devs |  |
| Phase 10: Testing & Launch Prep | 2-3 tuần | Full team |  |
| **TOTAL** | **23-30 tuần** | **~6-7 months** | |

**Lưu ý:** Thời gian có thể thay đổi tùy theo:
- Kích thước team
- Kinh nghiệm của team
- Độ phức tạp thực tế
- Thay đổi requirements
- Issues không lường trước

---

## Tech Stack Summary

### Backend
```
Spring Boot 3.2.x + Java 17
MySQL 8.0 + Redis 7.x + RabbitMQ 3.x
Spring Security 6 + JWT
Spring Data JPA (Hibernate)
WebSocket (STOMP)
Swagger/OpenAPI 3
Docker & Docker Compose
```

### Android
```
Java 11+ (Android SDK 26-34)
MVVM Architecture
Hilt (DI)
Retrofit 2 + OkHttp
RxJava 3
Room Database
Glide
Navigation Component
Material Design 3
Firebase (Auth, FCM)
Google Maps
```

### Third-party Services
```
Payment: VNPay, MoMo, ZaloPay
SMS: Twilio/ESMS
Email: SendGrid/AWS SES
Push: Firebase Cloud Messaging
Maps: Google Maps Android API
Storage: Cloudinary/AWS S3
```

---

## Chiến lược phát triển theo độ ưu tiên & MVP

### Phase 1: Customer App MVP (Phase 1-7) - Ưu tiên cao nhất 

**Must-Have Features (16-20 tuần):**
1. Authentication (Login/Register/OTP)
2. Search trips (Filters, sorting)
3. View trip details
4. Interactive seat selection
5. Create booking
6. Payment integration (VNPay hoặc MoMo)
7. View tickets với QR code
8. Basic push notifications
9. Real-time trip tracking
10. User profile management

**Nice-to-Have (Có thể làm sau):**
- Promotions & vouchers (Phase 6)
- Wallet (Phase 6)
- Reviews & ratings (Phase 7)
- Help center (Phase 7)

**Milestone: Customer App MVP Ready for Launch**

---

### Phase 2: Driver App (Phase 8) - Ưu tiên thứ hai 

**Core Features (2-3 tuần):**
1. Driver authentication & verification
2. View assigned trips
3. Start/End trip
4. QR check-in passengers
5. Realtime GPS tracking
6. View earnings
7. Basic navigation

**Milestone: Driver App Functional**

---

### Phase 3: Web Dashboard (Phase 9) - Ưu tiên thứ ba 

**Operator Features (3-4 tuần):**
1. Manage trips (CRUD)
2. Manage buses & routes
3. Manage drivers
4. View bookings & revenue
5. Basic reports

**Admin Features:**
1. Operator management & verification
2. System configuration
3. User management
4. System reports

**Milestone: Complete Platform Ready**

---

### MVP Success Criteria

**Customer App:**
- Users có thể tìm kiếm và đặt vé successfully
- Payment flow hoạt động end-to-end
- QR tickets được generate và hiển thị
- App stable với < 2% crash rate

**Driver App:**
- Drivers có thể check-in passengers
- GPS tracking update realtime
- Earnings được tính toán chính xác

**Web Dashboard:**
- Operators có thể tạo trips và quản lý buses
- Revenue reports accurate
- Admin có thể approve operators

---

###  Launch Strategy

**Soft Launch (After Phase 7):**
- Customer App only
- Limited to 1-2 bus operators
- Beta testing với real users
- Collect feedback

**Full Launch (After Phase 10):**
- All 3 platforms (Customer, Driver, Web)
- Open to all operators
- Marketing campaign
- Full support team ready

---

---

## Các lệnh thường dùng

### Root Level

```bash
# Start all services
docker-compose up -d

# Stop all services
docker-compose down

# View logs
docker-compose logs -f backend

# Clean everything
docker-compose down -v
rm -rf backend/target
rm -rf android-app/.gradle
```

### Backend

```bash
cd backend

# Build
mvn clean install

# Run
mvn spring-boot:run

# Test
mvn test

# Package
mvn clean package
```

### Android

```bash
cd android-app

# Build debug
./gradlew assembleDebug

# Install on device
./gradlew installDebug

# Run tests
./gradlew test

# Clean
./gradlew clean
```

---

## Kết luận

Cấu trúc Monorepo này cho phép bạn:

**Quản lý dễ dàng**: Cả backend và Android trong 1 repository
**Sync API**: Thay đổi API được reflect ngay lập tức
**Share code**: DTOs và constants có thể dùng chung
**CI/CD đơn giản**: 1 pipeline build cả 2
**Versioning thống nhất**: Backend và Android cùng version


