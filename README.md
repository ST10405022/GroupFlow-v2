# GroupFlow App

GroupFlow is an Android application developed using **Clean Architecture** principles and **role-based access control** to serve both **Patients** and **Employees** in a clinical environment. The system enables users to manage appointments, view ultrasound scans, submit reviews, and access clinic information.

---

# Previous Sprint
## Sprint 4: Project Structure and Initial Implementation
**Duration:** 26th June – 8th July  
**Goal:**  
Set up the core infrastructure of the application, initialize the GitHub repository and CI/CD pipeline, and scaffold all necessary classes and layout files to support modular development of GroupFlow.

### ✅ Objectives Achieved
- 📁 Defined and implemented a **Clean Architecture structure**:
    - Separation into **domain**, **data**, and **UI** layers.
    - Defined entities, repositories, services, and UI screens per role.
- ⚙️ CI/CD Pipeline:
    - Initialized GitHub repository.
    - GitHub Actions configured for basic linting and build checks (to be expanded).
- 🧱 Initial Implementation:
    - Designed layouts for all core activities (login, register, dashboard, etc.).
    - Created mock repositories using in-memory data classes.
    - Implemented navigation between screens based on user role.

---

## 📦 Project Structure (Sprint 4)

```plaintext
com.example.groupflow
│
├── core
│   ├── domain              // Entities & Value Objects
│   │   ├── User.kt
│   │   ├── Appointment.kt
│   │   ├── DoctorInfo.kt
│   │   ├── Employee.kt
│   │   ├── Notification.kt
│   │   ├── Patient.kt
│   │   ├── UltrascanImage.kt
│   │   └── Review.kt
│   ├── service             // Port Interfaces
│   │   ├── AuthenticationService.kt
│   │   ├── AppointmentService.kt
│   │   ├── ImagingService.kt
│   │   └── ReviewService.kt
│   └── util                // Constants, Mappers, Exceptions
│
├── data                    // Adapter Implementations (Repositories)
│   ├── auth
│   │   └── InMemoryAuthAdapter.kt
│   ├── appointment
│   │   └── InMemoryAppointmentRepo.kt
│   ├── scan
│   │   └── InMemoryScanRepo.kt
│   ├── review
│   │   └── InMemoryReviewRepo.kt
│   ├── notification
│   │   └── InMemoryNotificationRepo.kt
│   └── AppDatabase.kt      // Singleton for accessing in-memory repos
│
├── ui                      // Activities and UI Layer
│   ├── auth
│   │   ├── LoginActivity.kt
│   │   └── RegisterActivity.kt
│   ├── appointments
│   │   ├── AppointmentsActivity.kt
│   │   └── RequestAppointmentActivity.kt
│   ├── ultrascans
│   │   ├── UltrascansActivity.kt
│   │   └── UploadUltrascanActivity.kt
│   ├── reviews
│   │   ├── ReviewsActivity.kt
│   │   └── LeaveReviewActivity.kt
│   ├── profile
│   │   └── UserProfileActivity.kt
│   ├── hubs
│   │   └── EmployeeHubActivity.kt
│   ├── ClinicInfoActivity.kt
│   └── NotificationsActivity.kt
│
├── GroupFlowApplication.kt   //  base Application class for global initialisation 
└── MainActivity.kt           // Acts as Patient Dashboard
```

---

## 🧪 Sprint 4 Functionality Summary

| Feature                    | Patient Access   | Employee Access        |
|----------------------------|------------------|------------------------|
| Login / Register           | ✅              | ✅                     |
| View Appointments          | ✅              | 🔜                     |
| Request Appointment        | ✅              | ❌                     |
| Upload Ultrascans          | ❌              | ✅                     |
| View Ultrascans            | ✅              | 🔜                     |
| Submit & View Reviews      | ✅              | ✅                     |
| Access Clinic Info         | ✅              | ✅                     |
| Receive Notifications      | ✅              | ✅                     |
| Dynamic Dashboards         | ✅ MainActivity | ✅ EmployeeHubActivity |

---

## 🔐 Access Control

| User Role   | Dashboard Entry          | Access Restrictions                      |
|-------------|--------------------------|------------------------------------------|
| Patient     | `MainActivity.kt`        | Cannot upload scans                      |
| Employee    | `EmployeeHubActivity.kt` | Cannot request appointments              |

---

## ⚙️ CI/CD

- ✅ GitHub Actions configured for:
  - Build verification
  - Linting & formatting
  - Testing workflows (to be completed in Sprint 6)
- ✅ Branch protection enabled on `main`
- ✅ Modular build scripts for future Gradle improvements


---
# Current Sprint
## Sprint 5: Core Feature Implementation ( Deadline: 25th August)

**Goal:**
- Replace in-memory stubs with **Firebase Firestore / Firebase Auth** services
- Implement service logic in `core.service` to connect data and UI
- Build ViewModels to support state-based UI updates
- Add **role-based dashboard behavior**:
  - Patients → `MainActivity`
  - Employees → `EmployeeHubActivity`

### ✅ Objectives Achieved
- 🔐 Authentication: Implemented FirebaseAuthAdapter with email/password registration, login, logout, and session persistence.
- 👥 Role-Based Access: Patients → MainActivity; Employees → EmployeeHubActivity.

- 🗄 Firebase Repositories:
  - `FirebaseAppointmentRepo`
  - `FirebaseScanRepo`
  - `FirebaseReviewRepo`
  - `FirebaseNotificationRepo`

- 🕒 Date Handling: Added Converters for LocalDateTime ↔ Long storage.

- 🌐 Lifecycle + Coroutines:
  - Used `lifecycleScope.launch {}` in Activities to safely call Firebase suspend functions.
  - Ensured data fetching and updates respect Activity lifecycle.
- 💾 SessionManager:
  - Stores userId, role, and persists across app restarts.
  - Enforces access restrictions before navigating to Activities.
---

## 🔜 Sprint 6: Integration and Testing (Deadline: 18th August)

### 🎯 Goals
- Full **Firebase integration** (Auth, Firestore, Storage)
- Connect all screens to real data
- Comprehensive **UI & unit testing**
- Finalize bottom navigation and toolbar behavior across roles

### 🔨 Planned Tasks

- [ ] Write unit tests for core services.
- [ ] Finalize navigation flows and validate all role-based access.
- [ ] Expand Firebase rules for notifications and clinic info.
- [ ] Add UI Tests (Espresso) for login, register, and navigation flows.
- [ ] CI/CD: Expand GitHub Actions to run tests automatically.

---

## 💡 Summaries
- Sprint 4 established a clean, modular structure with mock repos.
- Sprint 5 integrated Firebase, role-based navigation, and lifecycle-aware coroutines.
- Sprint 6 will finalize integration, strengthen testing, and deliver production readiness.

---

🧱 *Built using Android, Kotlin, Material 3, and Clean Architecture.*

---

## 👥 Contributors

- **Scrum-Master & Lead Front-End Developer:** *[Javier Pena Gonzalez]*
- **Lead Back-End Developer (Database & Infrastructure):** *[Fungho Baloyi / GitHub Handle]*
- **Architecture & Design Lead:** *[Lefa Matunda]*
- **Lead Back-End Developer (API & Integration):** *[Karabo Latakgomo]*
- **Requirements, Testing & QA:** *[Sandile Ndukula]*

---

_© 2025 GroupFlow Team — Built with passion and purpose._
