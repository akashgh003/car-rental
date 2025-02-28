# RentACarFrontEnd

This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 11.2.4.

## Application Flow
The following flowchart illustrates the complete user journey through our car rental system:

```mermaid
flowchart TD
    Start([User Enters Website]) --> Auth{Is User Authenticated?}
    
    %% Authentication Flow
    Auth -->|No| LandingPage[Landing Page]
    Auth -->|Yes| Dashboard[User Dashboard]
    
    LandingPage --> BrowseCarts[Browse Available Carts]
    LandingPage --> LoginSignup[Login/Signup]
    
    LoginSignup --> Login[Login Form]
    LoginSignup --> Signup[Signup Form]
    Login -->|Submit| ValidateLogin{Validate Credentials}
    Signup -->|Submit| ValidateSignup{Validate Information}
    
    ValidateLogin -->|Invalid| LoginError[Show Error Message]
    ValidateLogin -->|Valid| Dashboard
    
    ValidateSignup -->|Invalid| SignupError[Show Error Message]
    ValidateSignup -->|Valid| Dashboard
    
    %% User Dashboard Flow
    Dashboard --> UserOptions{User Options}
    UserOptions -->|View Profile| Profile[User Profile]
    UserOptions -->|View Rentals| RentalHistory[Rental History]
    UserOptions -->|Browse Carts| BrowseCarts
    UserOptions -->|Logout| Logout[Logout]
    
    Profile --> EditProfile[Edit Profile]
    EditProfile -->|Submit| ValidateProfile{Validate Changes}
    ValidateProfile -->|Invalid| ProfileError[Show Error Message]
    ValidateProfile -->|Valid| Profile
    
    %% Browse and Rent Flow
    BrowseCarts --> FilterCarts[Filter Carts]
    FilterCarts --> CartList[View Cart List]
    CartList --> CartDetails[View Cart Details]
    
    CartDetails --> CartAvailable{Is Cart Available?}
    CartAvailable -->|No| NotificationUnavailable[Show Unavailable Message]
    CartAvailable -->|Yes| UserAuthenticated{Is User Authenticated?}
    
    UserAuthenticated -->|No| RedirectLogin[Redirect to Login]
    UserAuthenticated -->|Yes| RentCart[Rent Cart Form]
    
    RentCart --> SelectDates[Select Rental Dates]
    SelectDates --> ValidateDates{Validate Dates}
    ValidateDates -->|Invalid| DateError[Show Date Error]
    ValidateDates -->|Valid| Checkout[Checkout]
    
    %% Checkout Flow
    Checkout --> PaymentMethod[Select Payment Method]
    PaymentMethod --> ProcessPayment[Process Payment]
    ProcessPayment --> PaymentStatus{Payment Status}
    
    PaymentStatus -->|Failed| PaymentError[Show Payment Error]
    PaymentStatus -->|Success| ConfirmBooking[Confirm Booking]
    
    ConfirmBooking --> SendConfirmation[Send Email Confirmation]
    SendConfirmation --> Dashboard
    
    %% Admin Flow
    Auth -->|Admin| AdminDashboard[Admin Dashboard]
    AdminDashboard --> AdminOptions{Admin Options}
    
    AdminOptions -->|Manage Carts| ManageCarts[Manage Carts]
    AdminOptions -->|Manage Users| ManageUsers[Manage Users]
    AdminOptions -->|View Rentals| ViewRentals[View All Rentals]
    AdminOptions -->|Analytics| ViewAnalytics[View Analytics]
    
    ManageCarts --> CartCRUD[Create/Read/Update/Delete Carts]
    ManageUsers --> UserCRUD[Create/Read/Update/Delete Users]
    ViewRentals --> RentalCRUD[View/Update/Cancel Rentals]
    
    %% Logout Flow
    Logout --> Start
    
    %% Styling
    classDef default fill:#f9f9f9,stroke:#333,stroke-width:1px
    classDef primary fill:#3498db,color:white,stroke:#2980b9,stroke-width:1px
    classDef success fill:#2ecc71,color:white,stroke:#27ae60,stroke-width:1px
    classDef warning fill:#f1c40f,stroke:#f39c12,stroke-width:1px
    classDef danger fill:#e74c3c,color:white,stroke:#c0392b,stroke-width:1px
    classDef info fill:#9b59b6,color:white,stroke:#8e44ad,stroke-width:1px
    classDef secondary fill:#95a5a6,stroke:#7f8c8d,stroke-width:1px
    classDef decision fill:#e67e22,color:white,stroke:#d35400,stroke-width:1px
    
    class Start,Dashboard,AdminDashboard primary
    class Auth,ValidateLogin,ValidateSignup,ValidateProfile,CartAvailable,UserAuthenticated,ValidateDates,PaymentStatus decision
    class LoginError,SignupError,ProfileError,DateError,PaymentError,NotificationUnavailable danger
    class ConfirmBooking,SendConfirmation success
    class FilterCarts,CartList,CartDetails,SelectDates info
    class LandingPage,BrowseCarts,Profile,RentalHistory secondary
    class RentCart,Checkout,ProcessPayment warning
