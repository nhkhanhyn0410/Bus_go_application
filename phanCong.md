### Phase 1: Foundation & Setup

#### Backend Setup
- [X] Tạo cấu trúc project Spring Boot
- [KH] Cấu hình database (MySQL + Flyway migrations)
- [KH] Setup Redis cache
- [KH] Setup RabbitMQ
- [KH] Cấu hình Spring Security + JWT
- [KH] Setup Swagger/OpenAPI documentation
- [KH] Tạo base entities (BaseEntity, Auditable)
- [KH] Global exception handling
- [KH] Response wrapper standardization

#### Android App Setup
- [KH] Tạo cấu trúc project Android
- [ ] Setup Hilt dependency injection
- [ ] Cấu hình Retrofit + OkHttp
- [ ] Setup Room database
- [ ] Base classes (BaseActivity, BaseFragment, BaseViewModel)
- [TR/TH] Navigation component setup
- [TR] Material Design theme configuration
- [ ] Utility classes (DateUtils, CurrencyUtils, etc.)

#### Infrastructure
- [ ] Development environment documentation

**Deliverables:**
- Project structure hoàn chỉnh
- Base setup cho cả Backend và Android
- Sample API endpoint + Android screen kết nối thành công

---

### Phase 2: Authentication & User Management

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

### Phase 3: Core Business Logic - Trip & Booking

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

### Phase 4: Payment Integration

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

### Phase 5: Real-time Tracking & Notifications

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