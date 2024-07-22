# Project Phases

## Phase 1: Planning and Requirements (Objective)
1. **Requirements Gathering**: 
    - Identify user needs, business goals, 
    - Compile a list of must-have features and optional functionalities.
  
2. **Overall Model**: 
    - Formulate a high-level problem statement.
    - Identify key stakeholders and define their roles and responsibilities.
	
## Phase 2: Design (Methodology)
1. **UX Design**: 
    - Outline the range of actions available to users.
    - Detail the user journey and interaction flow within the application.

2. **UI Design**: 
    - Create wireframes or mockups to visualize key user interfaces.
  
3. **System Architecture**: 
    - Develop a high-level architecture diagram.
    - Describe software and hardware components, and how they interact.
    - Include a database schema if applicable.

## Phase 3: Development Planning (Methodology)
1. **Feature Planning**: 
    - Provide detailed specifications for each feature.
	
## Phase 4: Coding and Unit Testing (Implementation)
1. **Coding**: 
    - Develop source code for both frontend and backend components.
    - Include documentation for critical functions and modules.

2. **Unit Testing**: 
    - Design test cases for individual units of code.
    - Document test results and flag any issues for resolution.
	
## Phase 5: Testing and Quality Assurance (Validation)
1. **Ongoing Testing**: 
    - Develop a comprehensive test plan specifying types of tests to be conducted.
    - Continuously update test results and issues identified.

2. **Integration and User Acceptance Tests**: 
    - Create test cases for integration points between system components.
    - Define user acceptance criteria and document test outcomes.
	
## Phase 6: Deployment (Implementation)
1. **System Delivery**: 
    - Prepare the final build of the application for deployment.
    - Include step-by-step deployment instructions.

2. **Deployment**: 
    - Specify the deployment environment requirements.
    - Develop a rollback plan to mitigate potential deployment failures.

## Goal
- Have an ai with minimal direction and human effort make an software, be it app , website or wathever.
- A map for a developer be it ai or human to make a software

## Communication with AI
The AI should understand the user's intent. The user should not need to be overly specific.
The human should prompts shoudl contain certain information. the ai should ask for clarification if needed but up to a point. 

### Workflow
1. The user provides the AI with a description or concept of the desired software or system.
2. the ai replies with clarification if neeeded. ai cannot code much in a single step. hende a map is needed. i imagine a the proces should be like a set of modules. they are nested. their basic structure should be output / input . problems should be divided in large problems and those in smaller . once cut into a simple enough size it codes. having in consideration the expected output and input. the ai can give recomendations make asumptions but asks the uses and gives him options. 

### Development Stages

1. **Ideation and Market Research**
   - Initial concept, target audience, and potential features.
   ```dsl
   Ideation {
     Concept "On-demand delivery service for urban areas"
     MarketResearch {
       TargetAudience "Urban residents"
       Competitors ["Uber", "DoorDash"]
       Features ["Real-time tracking", "Quick delivery", "Multiple payment options"]
     }
   }
   ```

2. **Technical Requirements**
   - Business goals, user stories
   ```dsl
   Technical {
     UserStories ["As a user, I want to track my delivery in real-time"]
   }
   ```

3. **Design and Prototyping**
   - Design phase details, including wireframes, mockups, prototypes, and target platforms.
   
4. **Architecture Planning**
   - Technical architecture and system design.
   ```dsl
   Architecture {
     TechStack {
       Backend "Node.js"
       Frontend "React Native"
       Database "MongoDB"
     }
     SystemDesign ["Microservices", "RESTful API"]
   }
   ```

5. **Development Sprints**
   - Development tasks and sprints.
   ```dsl
   Development {
     Sprint 1 {
       Tasks ["Implement Login", "Set up database"]
       CodeReview true
     }
     Sprint 2 {
       Tasks ["Implement Payment Gateway", "User Testing"]
       CodeReview true
     }
   }
   ```


7. **Deployment and Monitoring**
   - Deployment environment and monitoring tools.
   ```dsl
   Deployment {
     Environment "Production"
     MonitoringTools ["Prometheus", "Grafana"]
   }
   ```


## Examples of DSL for this. 

```
// Define reusable components
Component "Header" {
  Display "AppName" as Title
  Icon "Notifications" {
    onClick: FetchNotifications, Show NotificationsPopup
  }
  Icon "Messages" {
    onClick: GoTo Messages
  }
}

// Landing Page Screen
Screen "LandingPage" {
  BeforeScreenLoads: If UserType is NULL, Set UserType to Guest
  
  Use Header
  Display "Welcome" as Title
  
  Button "Login" {
    onClick: GoTo Login
  }
  
  Button "SignUp" {
    onClick: GoTo SignUp
  }
  
  Button "Guest" {
    onClick: GoTo GuestRegistration
  }
}

// Login Screen
Screen "Login" {
  BeforeScreenLoads: CheckSession
  
  Use Header
  Display "Login" as Title
  
  Input "PhoneNumber"
  Input "Password"
  
  Button "Login" {
    onClick: LoginUser, Set UserType to User
  }
  
  Link "ForgotPassword" {
    onClick: GoTo ForgotPassword
  }
}

// SignUp Screen
Screen "SignUp" {
  Use Header
  Display "SignUp" as Title
  
  Input "Name"
  Dropdown "Gender"
  Input "PhoneNumber"
  Input "Password"
  Input "ConfirmPassword"
  
  Button "SignUp" {
    onClick: RegisterUser, Set UserType to User
  }
}

// Guest Registration Screen
Screen "GuestRegistration" {
  Use Header
  Display "GuestRegistration" as Title
  
  Input "PhoneNumber"
  
  Button "Continue" {
    onClick: RegisterGuest, Set UserType to Visitor
  }
}

// Home Screen
Screen "Home" {
  BeforeScreenLoads: FetchHomeData, Set HomeData
  
  Use Header
  Display "Home" as Title
  
  Button "NewRequest" {
    onClick: GoTo NewRequest
  }
  
  Button "MyRequests" {
    onClick: If UserType is User, GoTo MyRequests
  }
  
  Button "BecomeAUser" {
    onClick: If UserType is Visitor, GoTo SignUp
  }
}

// ... (continue for other screens like NewRequest, MyRequests, ProfileAndSettings, etc.)

```

## +1 Level of Abstraction
```
// Define reusable components
HeaderComponent with Title "AppName", Notifications, Messages

// Landing Page Screen
LandingPage {
  Use HeaderComponent
  Title "Welcome"
  Buttons "Login", "SignUp", "Guest"
  OnLoad: SetGuestIfNoUser
}

// Login Screen
LoginScreen {
  Use HeaderComponent
  Title "Login"
  Inputs "PhoneNumber", "Password"
  Button "Login"
  Link "ForgotPassword"
  OnLoad: CheckSession
}

// SignUp Screen
SignUpScreen {
  Use HeaderComponent
  Title "SignUp"
  Inputs "Name", "PhoneNumber", "Password", "ConfirmPassword"
  Dropdown "Gender"
  Button "SignUp"
}

// Guest Registration Screen
GuestRegistration {
  Use HeaderComponent
  Title "GuestRegistration"
  Input "PhoneNumber"
  Button "Continue"
}

// Home Screen
HomeScreen {
  Use HeaderComponent
  Title "Home"
  Buttons "NewRequest", "MyRequests", "BecomeAUser"
  OnLoad: FetchHomeData
}

// ... (continue for other screens)

```

## 2 Level Of Abstraction
```
// Define reusable components
HeaderComponent with Title "AppName", Notifications, Messages

// Landing Page Screen
LandingPage {
  Use HeaderComponent
  Title "Welcome"
  Buttons "Login", "SignUp", "Guest"
  OnLoad: SetGuestIfNoUser
}

// Login Screen
LoginScreen {
  Use HeaderComponent
  Title "Login"
  Inputs "PhoneNumber", "Password"
  Button "Login"
  Link "ForgotPassword"
  OnLoad: CheckSession
}

// SignUp Screen
SignUpScreen {
  Use HeaderComponent
  Title "SignUp"
  Inputs "Name", "PhoneNumber", "Password", "ConfirmPassword"
  Dropdown "Gender"
  Button "SignUp"
}

// Guest Registration Screen
GuestRegistration {
  Use HeaderComponent
  Title "GuestRegistration"
  Input "PhoneNumber"
  Button "Continue"
}

// Home Screen
HomeScreen {
  Use HeaderComponent
  Title "Home"
  Buttons "NewRequest", "MyRequests", "BecomeAUser"
  OnLoad: FetchHomeData
}

// ... (continue for other screens)

```

## 3 Level of Abstraction 

```
// Define Application Type and Features
ApplicationType "MobileApp" with Features "Authentication", "Notifications", "UserProfiles"

// Define User Roles
UserRoles "Guest", "User", "Admin"

// Define Application Flow
AppFlow {
  LandingPage -> LoginOrSignUp
  Login -> Home
  SignUp -> Home
  Home -> [NewRequest, MyRequests]
}

// Define Data Models
DataModels {
  UserProfile: "Name", "PhoneNumber", "Gender"
  Request: "PickupLocation", "DropOffLocation", "ItemDescription", "EstimatedWeight"
}

// Define APIs
APIs {
  FetchNotifications: "/api/notifications"
  LoginUser: "/api/login"
  RegisterUser: "/api/signup"
  FetchHomeData: "/api/getHomeData"
}

// Define Conditional Logic
Conditions {
  UserTypeIsNull: "UserType is NULL"
  UserTypeIsUser: "UserType is User"
  UserTypeIsVisitor: "UserType is Visitor"
}

// Define Custom Actions
CustomActions {
  SetGuestIfNoUser: "If UserTypeIsNull, Set UserType to Guest"
  NavigateBasedOnUser: "If UserTypeIsUser, GoTo MyRequests else GoTo SignUp"
}
```

## 4 Level


```
// Define Core Purpose
Purpose "ServiceRequestPlatform"

// Define Target Audience
Audience "GeneralPublic"

// Define Key Interactions
Interactions {
  UserRequestsService
  UserManagesProfile
  UserReceivesNotifications
}

// Define Data Needs
DataNeeds {
  UserProfileData
  ServiceRequestData
}

// Define Security Level
Security "Medium"

// Define Custom Logic
CustomLogic {
  GuestAccess
  UserTypeBasedNavigation
}

// Define Platform
Platform "Mobile"
```

## 5 Level of abstraction

```
// Define Business Goal
BusinessGoal "Improve Urban Logistics"

// Define Market Need
MarketNeed "Efficient, On-Demand Delivery Services"

// Define User Outcome
UserOutcome "Quick and Reliable Service Requests"

// Define Competitive Edge
CompetitiveEdge "AI-Optimized Routing"

// Define Monetization Strategy
Monetization "Freemium with In-App Purchases"

// Define Regulatory Compliance
RegulatoryCompliance "GDPR, HIPAA"
```

## 6 Level of abstracction

```
AppConcept "On-demand delivery service for urban areas."
```
### 1. Low-Level Abstraction (Initial JSON-like DSL)

**Example:**
```json
{
  "Components": {
    "Header": {
      "UI": {
        "Logo": {},
        "Navigation": {
          "Home": {"Action": ["Navigate:Home"]},
          "Profile": {"Action": ["Navigate:Profile"]}
        }
      }
    }
  },
  "Screen": "Home",
  "UI": {
    "Header": {"UseComponent": "Header"},
    "Title": "Home",
    "ExpandableSection": {
      "Label": "More Info",
      "Action": ["Expand"],
      "Nested": {
        "Text": "Detailed Information",
        "Button": {
          "LearnMore": {"Action": ["Navigate:LearnMore"]}
        }
      }
    }
  },
  "Preload": ["API:GET /api/loadHomeData"]
}
```

**Description:**
- Focuses on the nitty-gritty details of UI elements, actions, and data models.
- Requires the developer to specify each screen, component, and action individually.
- Offers the most control but is also the most verbose.

---

### 2. Mid-Level Abstraction (First Simplified DSL)

**Example:**
```mabl
LandingPage {
  Use HeaderComponent
  Title "Welcome"
  Buttons "Login", "SignUp", "Guest"
  OnLoad: SetGuestIfNoUser
}
```

**Description:**
- Introduces higher-level constructs like reusable components and simplified screen definitions.
- Allows for quicker development by reducing boilerplate code.
- Balances control and simplicity.

---

### 3. High-Level Abstraction (Second Simplified DSL)

**Example:**
```mabl
ApplicationType "MobileApp" with Features "Authentication", "Notifications", "UserProfiles"
UserRoles "Guest", "User", "Admin"
AppFlow {
  LandingPage -> LoginOrSignUp
  Login -> Home
  SignUp -> Home
  Home -> [NewRequest, MyRequests]
}
```

**Description:**
- Focuses on the application's overall architecture, flow, and main features.
- Automatically generates much of the underlying code based on best practices.
- Offers less control but is much quicker for prototyping and development.

---

### 4. Ultra-High-Level Abstraction (Core Purpose and Interactions)

**Example:**
```mabl
Purpose "ServiceRequestPlatform"
Audience "GeneralPublic"
Interactions {
  UserRequestsService
  UserManagesProfile
  UserReceivesNotifications
}
```

**Description:**
- Focuses on the application's core purpose, target audience, and key interactions.
- Leaves the implementation details to the system, which generates an appropriate architecture and feature set.
- Offers the least control but is the quickest for getting a project off the ground.

Each level of abstraction serves different needs and is suitable for different stages of development or types of projects.

***
## High-Level Language Domain-Specific Language (HHL-DSL) Documentation

### Overview
HHL-DSL is a domain-specific language designed to facilitate AI-assisted programming. It serves as a blueprint for AI to generate software modules based on minimally structured prompts. This document outlines the basic syntax and provides examples for using HHL-DSL.

### Syntax Requirements for Minimally Structured Prompts
1. `Objective`: Clearly state the primary goal.
2. `Domain`: Specify the domain or industry.
3. `UserRoles`: Define user roles.
4. `CoreFeatures`: List key functionalities.
5. `Platform`: Indicate target platform.
6. `Constraints`: Mention any limitations.
7. `ComparativeExample`: Provide comparative examples for context.

### HHL-DSL Example 1
```
Objective: Develop a mobile application
Domain: Transportation
UserRoles: [Customers, TruckServiceProviders]
CoreFeatures: [RealTimeTracking, Scheduling, PaymentProcessing]
Platform: MobileApp
Constraints: None
ComparativeExample: Uber for trucks
```

## Stage 1: Project Specification and Scope Definition in HHL-DSL

### Objective
To collect all project specifications, from user stories to feature lists, and outline the project scope and features in a language-agnostic manner.

### HHL-DSL Syntax Extensions for Stage 1
1. `ProjectSpecifications`: A collection of all project requirements.
2. `ProjectScope`: A high-level outline of the project's boundaries.
3. `UserStories`: Narratives that describe how different user roles interact with the system.
4. `FeaturesList`: A detailed list of functionalities.

### HHL-DSL Example for Stage 1
```
Objective: Develop a mobile application
Domain: Transportation
UserRoles: [Customers, TruckServiceProviders]
CoreFeatures: [RealTimeTracking, Scheduling, PaymentProcessing]
Platform: MobileApp
Constraints: None
ComparativeExample: Uber for trucks
ProjectScope: Connect individual customers with truck service providers for moving and pick-up services.
ProjectGoal: To connect individual customers with truck service providers for services such as moving furniture or item pick-up.
UserStories: [
  "As a Customer, I want to schedule a pick-up so that I can move my furniture.",
  "As a TruckServiceProvider, I want to accept or decline jobs based on my availability.",
  "As a Customer, I want to track the truck in real-time during the service."
]
FeaturesList: [UserAuthentication, RealTimeTracking, SchedulingSystem, PaymentGateway, RatingsAndReviews]
TargetDevicesOrPlatforms: [Mobile(Android, iOS), Web, AdminPortal]
SelectedFrameworks: [ReactNative, React.js, ReactAdmin]
ArchitecturalParadigms: [MVVM, SPA, CRUD]
Backend: [Node.jsWithExpress]
Database: [PostgreSQL]
Hosting: [AWS]
Security: [OAuth2.0]
```

### Stage 1 Output: Language-Agnostic Project Map
The AI will interpret the HHL-DSL prompt and generate a language-agnostic project map that includes:

1. **Project Specifications**: User Authentication, Real-Time Tracking, Scheduling, Payment Processing, Ratings and Reviews.
  
2. **Project Scope**: The application aims to connect individual customers with truck service providers for services such as moving furniture or item pick-up.

3. **User Stories**: 
   - Customer: Schedule pick-ups for moving furniture.
   - Truck Service Provider: Accept or decline jobs based on availability.
   - Customer: Real-time tracking of the truck during the service.

4. **Features List**: 
   - User Authentication
   - Real-Time Tracking
   - Scheduling System
   - Payment Gateway
   - Ratings and Reviews

This language-agnostic project map serves as the foundation for the next stages of development.

***
```
ServerSide: {
  Component: UserAuth
    Responsibility: User_Validation, Session_Management
    Interaction: Database_Read, Notification_Trigger

  Component: Scheduling
    Responsibility: Pickup_Scheduling, Delivery_Scheduling
    Interaction: UserAuth_Validation, RealTimeTracking_Update, Notification_Trigger

  Component: Payment
    Responsibility: Transaction_Processing, Payment_Authentication
    Interaction: UserAuth_Validation, Database_Update

  Component: RatingsReviews
    Responsibility: Review_Collection, Rating_Calculation
    Interaction: Database_ReadWrite, Notification_Trigger

  Component: Backend
    Responsibility: Server_Side_Logic
    Interaction: AllComponents_Communication, AWS_Hosting

  Component: Database
    Responsibility: Data_Storage, Data_Management
    Interaction: AllComponents_ReadWrite
}

ClientSide: {
  Component: RealTimeTracking
    Responsibility: Location_Monitoring, Location_Display
    Interaction: Client_Fetch, Database_Read

  Component: Notifications
    Responsibility: RealTime_Alerts
    Interaction: TriggeredBy_UserAuth, TriggeredBy_Scheduling, TriggeredBy_RatingsReviews

  Component: AdminPortal
    Responsibility: System_Management, Role_Management, Analytics
    Interaction: AllComponents_Monitoring
}

```

***

```
ClientType: User
  StateManagement: Redux
  Component: UserDashboard
    Responsibility: Display_Services, Account_Management
    Interaction: RealTimeTracking_View, Scheduling_View

  Component: Notifications
    Responsibility: RealTime_Alerts
    Interaction: TriggeredBy_Scheduling, TriggeredBy_Payment

ClientType: Admin
  StateManagement: Redux
  Component: AdminDashboard
    Responsibility: User_Management, Analytics
    Interaction: AllComponents_Monitoring
    Security: Firewall

  Component: Notifications
    Responsibility: System_Alerts
    Interaction: TriggeredBy_UserActivity, TriggeredBy_SystemEvents

ClientType: Trucker
  StateManagement: Redux
  Component: TruckerDashboard
    Responsibility: Job_Management, Account_Management
    Interaction: RealTimeTracking_Update, Scheduling_View

  Component: Notifications
    Responsibility: Job_Alerts
    Interaction: TriggeredBy_Scheduling, TriggeredBy_Payment
```
 ***
## Stage 6a: Development Task Identification and Dependency Analysis DSL (DevPlan-DSL)

### Objective
To create a DSL that identifies individual development tasks for each component and outlines their dependencies. This DevPlan-DSL aims to provide a structured approach to breaking down the project into actionable tasks.

### DevPlan-DSL Syntax
1. `Task`: Specifies an individual development task.
2. `Component`: Identifies the component to which the task belongs.
3. `Dependency`: Lists the tasks that must be completed before the current task can begin.

### DevPlan-DSL Example

```
Component: UserAuth
  Task: Implement_User_Validation
    Dependency: Setup_Database

  Task: Implement_Session_Management
    Dependency: Implement_User_Validation

Component: Scheduling
  Task: Implement_Pickup_Scheduling
    Dependency: Implement_User_Validation

  Task: Implement_Delivery_Scheduling
    Dependency: Implement_Pickup_Scheduling

Component: Payment
  Task: Implement_Transaction_Processing
    Dependency: Implement_User_Validation

  Task: Implement_Payment_Authentication
    Dependency: Implement_Transaction_Processing

Component: UserDashboard (ClientType: User)
  Task: Implement_UI_for_User_Dashboard
    Dependency: Setup_Frontend_Environment

  Task: Integrate_RealTimeTracking_API
    Dependency: Implement_UI_for_User_Dashboard

Component: AdminDashboard (ClientType: Admin)
  Task: Implement_UI_for_Admin_Dashboard
    Dependency: Setup_Frontend_Environment

  Task: Implement_User_Management
    Dependency: Implement_UI_for_Admin_Dashboard

Component: TruckerDashboard (ClientType: Trucker)
  Task: Implement_UI_for_Trucker_Dashboard
    Dependency: Setup_Frontend_Environment

  Task: Implement_Job_Management
    Dependency: Implement_UI_for_Trucker_Dashboard
```

### How to Use DevPlan-DSL
1. The AI interprets the SysArch-DSL, ClientArch-DSL, and ProjectMap-DSL to generate the DevPlan-DSL.
2. This DevPlan-DSL serves as a structured guide for development planning, providing a detailed list of tasks and their dependencies for each component.

By using this DevPlan-DSL, the development team gains a clear and structured task breakdown, allowing for a more organized and efficient development process.
**