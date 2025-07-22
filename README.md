# 📅 iBook

## 📌 Real-World Problem
Many individual service providers — such as private tutors, doctors, barbers, consultants, or local repairmen — currently manage appointments manually through phone calls or messages. This manual system is:

Time-consuming, requiring back-and-forth communication
Error-prone, often leading to double bookings or forgotten appointments
Lacks visibility, as customers don't know when the provider is available
Has no history tracking, making it hard to analyze peak hours or plan availability
Causes stress and poor customer experience when scheduling conflicts arise
For example, a barber may unknowingly give the same time slot to two different customers, resulting in delays and dissatisfaction.

## 🎯 Project Motivation
This project was built to digitize the appointment scheduling process for individual service providers by offering a simple, self-managed, cloud-based system where:

Providers can publish their availability dynamically
Customers can view and book available time slots online
Booked slots are automatically marked as unavailable
Canceled slots are reopened for booking
Providers can track their daily, weekly, and monthly appointments

## 🧩 Key Problems Solved
Eliminates manual scheduling by phone or message
Prevents double bookings through real-time availability management
Saves time for both providers and customers
Brings professional-level scheduling tools to independent service providers

## 🚀 Why It Matters
By giving individuals the ability to control their own schedule, publish availability, and let customers book transparently, this system:

Increases efficiency and professionalism
Builds customer trust through reliability
Can be extended to multiple service domains easily
Enables providers to focus more on their service and less on logistics

## 📌 Context Diagram
![Context Diagram.jpg](Context%20Diagram.jpg)

## 📌 Use Case Diagram
![Use case diagram.jpg](Use%20case%20diagram.jpg)

## 📘 User Stories

### 🧑‍💼 As a Service Provider, I want to:
1. ✅ Create my availability timetable
   
   So that I can specify when I’m open for appointments
2. ✅ Dynamically add or update available time slots
   
   So that I can adjust my schedule anytime without external help
3. ✅ View all upcoming appointments
   
   So that I can prepare and avoid overlapping bookings
4. ✅ Cancel appointments or mark no-shows

   So that I can free up time and avoid lost productivity
5. ✅ Be notified of new bookings
   
   So that I don’t miss important appointments
6. ✅ Track appointment history

   So that I can analyze busy periods and customer frequency

### 🧑‍💻 As a Customer, I want to:
1. ✅ View a provider’s available time slots

   So that I can book without calling or waiting
2. ✅ Book an appointment online easily

   So that I can schedule services at my convenience
3. ✅ Cancel or reschedule a booking

   So that I can manage my time flexibly
4. ✅ Get confirmation and reminders

   So that I don’t forget my scheduled appointments
5. ✅ Avoid double bookings

   So that I can trust the service provider’s system

### 🔧 As a System, I want to:
1. ✅ Prevent double booking

   So that only one user can book a time slot
2. ✅ Reopen canceled slots

   So that others can book freed-up time
3. ✅ Support real-time updates

   So that both customers and providers see up-to-date information
4. ✅ Run on serverless cloud infrastructure

   So that the system is scalable and cost-effective (using AWS Lambda)




## ✅ Essential Features and Functionalities

### 👤 For Service Providers:
1. Timetable Creation
   * Define working days and available hours.
   * Mark holidays or unavailable periods.
2. Dynamic Time Slot Management
   * Add, update, or delete available time slots in real-time.
   * Prevent overlapping time slots.
3. Appointment Dashboard
   * View upcoming, past, and canceled appointments.
   * Filter by date, status, or customer.
4. Appointment Cancellation
   * Cancel scheduled appointments.
   * Automatically release the slot for rebooking.
5. Notifications
   * Receive alerts when new appointments are booked or canceled.
6. History Tracking
   * View detailed logs of past appointments and customer interactions.

### 👥 For Customers:
1. Service Provider Discovery
   * Search or access a specific provider’s page.
2. Available Time Slot View
   * Browse real-time available slots from selected providers.
3. Appointment Booking
   * Book a time slot and provide necessary details.
4. Appointment Rescheduling
   * Modify existing appointment to another available time.
5. Confirmation and Reminder Notifications
   * Receive confirmation instantly.
   * Get reminders via email/SMS before the appointment.
6. Cancel Appointment
   * Cancel with confirmation and free up the slot for others.

### ⚙️ System-Level Functionalities:
1. Double Booking Prevention
   * Ensure only one appointment per time slot per provider.
2. Authentication & Authorization
   * Secure login for both customers and providers.
3. Audit Logging
   * Track system activity and appointment changes.
4. REST API / Cloud Function Interface
   * Backend logic via Spring Cloud Function & AWS Lambda for scalability.
5. MongoDB Data Storage
   * Use MongoDB to store user, provider, time slot, and appointment data.
6. Stateless, Event-Driven Backend
   * Designed for serverless deployment (e.g., AWS Lambda with API Gateway).


## 🔒Non-Functional Requirements

#### ✅ 1. Usability
The system must provide an intuitive and responsive user interface.
Users (both customers and service providers) should be able to book, manage, and cancel appointments with minimal effort.
All actions should require minimal clicks and input, with real-time feedback.
#### ✅ 2. Security
All user data must be securely stored using encryption where necessary (e.g., passwords, personal information).
Authentication and authorization mechanisms must protect access to data (e.g., JWT, OAuth2).
Only authorized users can access and modify their respective data.
#### ✅ 3. Reliability
The system should be available 99.9% of the time, with proper failover support.
In case of system or function failure (e.g., AWS Lambda timeout), proper error handling must be in place.
#### ✅ 4. Performance
Backend operations (booking, canceling, updating appointments) must complete within 1 second.
The system must respond to UI/API calls within 300 ms under normal load.
#### ✅ 5. Scalability
The system must be horizontally scalable using cloud-native services (e.g., AWS Lambda, API Gateway, MongoDB Atlas).
It should be capable of supporting an increasing number of users and appointments without degradation in performance.
#### ✅ 6. Maintainability
The codebase must follow clean coding principles, be well-documented, and modular (e.g., use of Spring Cloud Function).
Test coverage must be maintained with unit and integration tests.
#### ✅ 7. Portability
The backend should be deployable on multiple environments (local, AWS Lambda, or Docker-based environments).
It must support CI/CD pipelines for deployment automation.
#### ✅ 8. Auditability
All user actions (booking, canceling, modifying) must be logged and time-stamped for traceability.
Logs should be queryable for debugging and analytics.


## 📐 Architecture

Our system follows a layered client-server architecture, with a Flutter frontend communicating via HTTP to a serverless Spring Cloud Function backend, backed by MongoDB. This architecture ensures modularity, scalability, and clear separation of concerns.

### 🎨 1. Presentation Layer (Client UI – Flutter)
* Technology: Flutter (Dart)
* Purpose: Acts as the user interface for both service providers and customers.
* Key Responsibilities:
  * Allow users to view available time slots.
  * Enable booking, canceling, or modifying appointments.
  * Display feedback (confirmation, errors, history).
  * Communicate with backend via HTTP (using REST-like payloads).
  * Maintain client-side state and routing.

### 🌐 2. API Layer (Routing Layer – Spring Cloud Function)
* Technology: Spring Cloud Function with @Bean Function<Map<String, Object>, Object>
* Purpose: Receives incoming JSON requests and routes them to the appropriate handler based on the action field.
* Key Responsibilities:
  * Parse request JSON.
  * Validate input at a high level.
  * Dispatch logic to appropriate function (e.g., createUser, createAppointment).

### 🧠 3. Business Logic Layer (Function Layer)
* Technology: Java Functional Interfaces (Function, Supplier, Consumer)
* Purpose: Contains the core logic for appointment creation, status change, user registration, etc.
* Key Responsibilities:
  * Prevent double bookings.
  * Reopen canceled slots.
  * Link users, providers, and services appropriately.
  * Enforce domain rules (like valid time ranges).

### 🛠️ 4. Service Layer
* Technology: Spring @Service components (optional but used for separation of concern)
* Purpose: Implements reusable business logic for scheduling, slot validation, etc.
* Key Responsibilities:
  * Modularize domain logic.
  * Shared methods used across multiple functions.

### 🗃️ 5. Persistence Layer
* Technology: Spring Data MongoDB (MongoRepository)
* Purpose: Handles CRUD operations with MongoDB collections.
* Key Responsibilities:
  * Store and retrieve users, appointments, time slots, and services.
  * Enforce constraints such as unique phone numbers.

### 📦 6. Domain Model Layer
* Technology: Java POJOs (or records)
* Purpose: Represents the system’s core data structures.
* Key Responsibilities:
  * Encapsulate business entities like User, Appointment, ServiceProvider.
  * Enable strong typing and validation rules.

### ☁️ 7. Deployment Layer (Cloud Infrastructure)
* Technology: AWS Lambda, API Gateway
* Purpose: Provide a serverless runtime for executing backend logic on demand.
* Key Responsibilities:
  * Auto-scale functions.
  * Expose HTTP endpoints securely.
  * Integrate with other cloud services (e.g., monitoring, logging, CI/CD).

![Architect](https://github.com/user-attachments/assets/4ef25fc7-1d93-4a0b-811f-e2c72a554448)

## 🚀 Class Diagram
![Class](https://github.com/user-attachments/assets/5b8e38bf-2ea9-4685-aaec-1a73c4507555)

This API allows you to manage appointments and users via JSON-based HTTP POST requests.


## 🚀 Sequence Diagram
![Sequence](https://github.com/user-attachments/assets/1cf5f116-6428-4fdb-a5ec-ed30d038bf0a)

## 🛠️ Technologies Used

The system leverages a modern, scalable technology stack tailored for cross-platform access, serverless deployment, and NoSQL flexibility:

### 🧑‍💻 Backend (Serverless)
* Java 21 – Main backend programming language
* Spring Cloud Function – To build function-based microservices for serverless execution
* Spring Data MongoDB – For seamless integration with MongoDB database
* AWS Lambda – Serverless runtime for deploying backend logic
* AWS API Gateway – To expose the functions as HTTP endpoints
* Maven – Build and dependency management

### 🧩 Frontend
* Flutter (Dart) – Cross-platform mobile UI framework for Android and iOS
* HTTP client in Flutter for API requests
* Bloc – State management solution in Flutter

### 🗃️ Database
* MongoDB Atlas – Cloud-based NoSQL database for flexible document storage

### ✅ Testing
* SpringBootTest – Unit testing for Java backend

### ⚙️ DevOps / Tools
* Postman – For manual API testing
* Git & GitHub – Version control and collaboration
* IntelliJ IDEA / VS Code – IDEs for backend and Flutter development respectively


## Use Case Descriptions

### Use Case Name: Book Appointment
Primary Actor(s): User (Customer), System

Preconditions:

* The user is registered and logged into the system.
* Service provider has published available time slots.

Postconditions:

* An appointment is created and linked to the user and service provider.
* Time slot is marked as unavailable.

Main Success Scenario:

1. User navigates to the list of available services.
2. User selects a service provider.
3. System displays available time slots.
4. User selects a preferred time slot.
5. User confirms the booking.
6. System creates an appointment.
7. System sends a confirmation notification to the user and the provider.

### Use Case Name: Cancel Appointment
Primary Actor(s): User (Customer), System

Preconditions:

* The user has an existing upcoming appointment.
* The cancellation is within allowed cancellation window.

Postconditions:

* The appointment status is set to "Cancelled".
* The time slot becomes available again.

Main Success Scenario:

1. User views their upcoming appointments.
2. User selects an appointment to cancel.
3. System confirms the cancellation request.
4. User confirms cancellation.
5. System updates the appointment status to "Cancelled".
6. System notifies the provider and user of the cancellation.
7. System reopens the time slot for booking.

### Use Case Name: Create Time Slot
Primary Actor(s): Service Provider, System

Preconditions:

* Service provider is authenticated.
* No conflicting time slots exist.
Postconditions:

* New time slot is added to provider’s availability.

Main Success Scenario:

1. Provider logs in and navigates to availability settings.
2. Provider selects a date and time range.
3. Provider defines slot duration (e.g., 30 mins).
4. System validates against existing slots.
5. System saves and displays the new time slots.


## Installation & Deployment
### ✅ 1. Cloning the Repository

Requirements:

* Git installed (git --version)

### Steps:
#### Navigate to the directory where you want the project
    cd ~/projects

#### Clone the repository
    git clone https://github.com/your-org/your-repo.git

#### Move into the project directory
    cd your-repo
### ✅ 2. Setting Up Dependencies and Environment

Requirements:
* Java 21+
* Maven 3.9+
* IntelliJ IDEA or VS Code (optional but recommended)

### Steps:

#### 🔧 Install Java:

#### Check Java version
    java -version

#### If not installed, install Java 21 using SDKMAN (Linux/Mac)
    curl -s "https://get.sdkman.io" | bash
    source "$HOME/.sdkman/bin/sdkman-init.sh"
    sdk install java 21-tem

#### On Windows, install via [https://adoptium.net/](https://adoptium.net/)
#### 🔧 Install Maven:

#### Check Maven
    mvn -v

#### If not installed, install via Homebrew (Mac)
    brew install maven
🔧 Set environment variables (Optional):

    export JAVA_HOME=/path/to/java21
    export MONGO_URI=mongodb://localhost:27017/yourdb
### ✅ 3. Database Setup (MongoDB)

Requirements:
MongoDB installed and running (mongod)

### Steps:
### 📦 Install MongoDB (if not installed):

    Mac: brew tap mongodb/brew && brew install mongodb-community@7.0
### Ubuntu: Follow 
https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-ubuntu/
### Windows: Use the MongoDB MSI installer

🚀 Start MongoDB:

### macOS
    brew services start mongodb-community

#### or manually
    mongod --dbpath /your/data/path
📁 Create initial collections (Optional):

You can use a script like mongo-init.js:

    // mongo-init.js
    db = db.getSiblingDB('yourdb');
    db.users.insertMany([
        { name: 'Admin', phone: '1234567890', role: 'admin' }
    ]);
Run it:

    mongo < mongo-init.js

### ✅ 4. Running the Application

CLI:
#### Clean and build the project
    mvn clean install

#### Run the Spring Boot application
    mvn spring-boot:run
GUI (IntelliJ IDEA or VS Code):
Open the project folder.
Import it as a Maven project.
Locate the main class (usually in src/main/java/.../Application.java).
Right-click → Run Application.main()


## 🚀 Endpoints

**Base URL:**  
`https://thbhrvap0d.execute-api.us-east-1.amazonaws.com/prod`

---
### ✅ `/appointment` — Appointment Operations
### ✅ `/user` — User Operations

All actions must be submitted as a POST request with a JSON body containing an `"action"` field.

---

## 📍 `/appointment` Actions

### ➕ Create Appointment

```json
{
  "action": "createAppointment",
  "serviceProviderId": "provider123",
  "userId": "user456",
  "serviceId": "service789",
  "startTime": "2025-07-16T14:30:00",
  "endTime": "2025-07-16T15:30:00",
  "status": "AVAILABLE",
  "notes": "First appointment slot"
}
```

---

### 🔎 Get Appointments

#### By User ID
```json
{
  "action": "getAppointmentByUserId",
  "userId": "user456"
}
```

#### By Service Provider ID
```json
{
  "action": "getAppointmentByServiceProviderId",
  "serviceProviderId": "provider123"
}
```

#### By Service ID
```json
{
  "action": "getAppointmentByServiceId",
  "serviceId": "687810331ef13a0afd0b7646"
}
```

##### ✅ Sample Response:
```json
[
    {
        "id": "6877d023fcb9715820640970",
        "serviceProviderId": "provider123",
        "userId": "6875a3fb9d8c2a85a2c84496",
        "serviceId": "687810331ef13a0afd0b7646",
        "startTime": "2025-07-16T14:30:00",
        "endTime": "2025-07-16T15:30:00",
        "status": "CANCELED",
        "notes": "First appointment slot",
        "createdDate": null,
        "lastModifiedDate": "2025-07-16T17:24:42.278",
        "duration": "PT1H"
    },
    {
        "id": "68780192a997a05b07a6c1f0",
        "serviceProviderId": "6877c947187f2b55b4258bcf",
        "userId": "6875a3fb9d8c2a85a2c84496",
        "serviceId": "687810331ef13a0afd0b7646",
        "startTime": "2025-07-16T14:30:00",
        "endTime": "2025-07-16T15:30:00",
        "status": "CANCELED",
        "notes": "First appointment slot",
        "createdDate": null,
        "lastModifiedDate": null,
        "duration": "PT1H"
    }
]
````


#### By Service Name
```json
{
  "action": "getAppointmentByServiceName",
  "serviceNames": ["car wash", "dentist"]
}
```

##### ✅ Sample Response:

```json
[
    {
        "serviceProviderName": "Kshitij",
        "serviceName": "Dentist",
        "serviceId": "687825b72f12e846aeb1171b",
        "appointments": [
            {
            "id": "6878019aa997a05b07a6c1f1",
            "serviceProviderId": "6877c947187f2b55b4258bcf",
            "userId": "6875a3fb9d8c2a85a2c84496",
            "serviceId": "687825b72f12e846aeb1171b",
            "startTime": "2025-07-16T14:30:00",
            "endTime": "2025-07-16T15:30:00",
            "status": "AVAILABLE",
            "notes": "First appointment slot",
            "createdDate": null,
            "lastModifiedDate": null,
            "duration": "PT1H"
            }
          ],
        "serviceProviderId": "6875c78d8a828d2e3b8fbea4"
    },
    {
        "serviceProviderName": "Kshitij",
        "serviceName": "car wash",
        "serviceId": "687810331ef13a0afd0b7646",
        "appointments": [
                {
                    "id": "6877d023fcb9715820640970",
                    "serviceProviderId": "provider123",
                    "userId": "6875a3fb9d8c2a85a2c84496",
                    "serviceId": "687810331ef13a0afd0b7646",
                    "startTime": "2025-07-16T14:30:00",
                    "endTime": "2025-07-16T15:30:00",
                    "status": "CANCELED",
                    "notes": "First appointment slot",
                    "createdDate": null,
                    "lastModifiedDate": "2025-07-16T17:24:42.278",
                    "duration": "PT1H"
                },
                {
                    "id": "68780192a997a05b07a6c1f0",
                    "serviceProviderId": "6877c947187f2b55b4258bcf",
                    "userId": "6875a3fb9d8c2a85a2c84496",
                    "serviceId": "687810331ef13a0afd0b7646",
                    "startTime": "2025-07-16T14:30:00",
                    "endTime": "2025-07-16T15:30:00",
                    "status": "CANCELED",
                    "notes": "First appointment slot",
                    "createdDate": null,
                    "lastModifiedDate": null,
                    "duration": "PT1H"
                }
            ],
        "serviceProviderId": "6875c78d8a828d2e3b8fbea4"
    }
]
```

#### Get All Appointments
```json
{
  "action": "getAllAppointments"
}
```

##### ✅ Sample Response:

```json
[
  {
    "id": "6877d023fcb9715820640970",
    "serviceProviderId": "provider123",
    "userId": "6875c78d8a828d2e3b8fbea4",
    "serviceId": "service789",
    "startTime": "2025-07-16T14:30:00",
    "endTime": "2025-07-16T15:30:00",
    "status": "BOOKED",
    "notes": "First appointment slot",
    "createdDate": null,
    "lastModifiedDate": null,
    "duration": "PT1H"
  }
]
```

---

### 🔄 Change Appointment Status

#### Cancel Appointment
```json
{
  "action": "changeAppointmentStatus",
  "id": "6877d023fcb9715820640970",
  "status": "CANCELED"
}
```

#### Book Appointment
```json
{
  "action": "changeAppointmentStatus",
  "id": "6877d023fcb9715820640970",
  "userId": "6875a3fb9d8c2a85a2c84496",
  "status": "BOOKED"
}
```

---

### 📘 Appointment Status Options

| Status     | Description                          |
|------------|--------------------------------------|
| AVAILABLE  | Slot created but not yet booked      |
| BOOKED     | Appointment is booked by a user      |
| CANCELED   | Appointment was canceled             |
| COMPLETED  | Appointment was completed            |
| NO_SHOW    | User did not attend the appointment  |

---

## 👤 `/user` Actions

### 🔎 Get User by Phone

```json
{
  "action": "getUserByPhone",
  "phone": "+198765432101"
}
```

---

### 📋 Get All Users

```json
{
  "action": "getAllUsers"
}
```

##### ✅ Sample Response:

```json
[
  {
    "id": "6875a3fb9d8c2a85a2c84496",
    "phone": "+19876543210",
    "nickname": null
  },
  {
    "id": "6875c78d8a828d2e3b8fbea4",
    "phone": "+1234567890",
    "nickname": null
  }
]
```

---

### ➕ Create User

#### Without Nickname
```json
{
  "action": "createUser",
  "phone": "+198765432103"
}
```

#### With Nickname
```json
{
  "action": "createUser",
  "phone": "+16412330771",
  "nickname": "Orgil"
}
```

---

## 📌 Notes

- All requests must use the `POST` method and include the `action` field.
- Timestamps must follow the ISO 8601 format, e.g. `"2025-07-16T14:30:00"`.
- Status values are case-sensitive.
- Duration is expressed in [ISO 8601 duration format](https://en.wikipedia.org/wiki/ISO_8601#Durations), e.g., `"PT1H"` for 1 hour.

---

## 📫 Contact

If you have questions or need support, please contact the development team.
