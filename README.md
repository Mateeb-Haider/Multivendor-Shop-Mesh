# The Shop Mesh - Multi-Vendor E-Commerce Platform

![Node.js](https://img.shields.io/badge/Node.js-20.x-green)
![Express](https://img.shields.io/badge/Express-5.1.0-blue)
![React](https://img.shields.io/badge/React-18.x-61dafb)
![MongoDB](https://img.shields.io/badge/MongoDB-8.17.1-green)
![Stripe](https://img.shields.io/badge/Stripe-18.5.0-purple)
![Socket.io](https://img.shields.io/badge/Socket.io-4.x-black)
![JWT](https://img.shields.io/badge/JWT-Authentication-orange)
![Vercel](https://img.shields.io/badge/Vercel-Deployment-black)

## Overview

The Multi-Vendor E-Commerce Platform is a comprehensive marketplace designed to seamlessly connect customers, sellers, and administrators in a unified ecosystem. This production-ready solution provides a complete e-commerce experience with multi-vendor support, real-time communication, secure payment processing, and automated workflows.

The platform enables customers to browse products, participate in promotions, place orders, and communicate directly with sellers. Sellers can create and manage their own shops, maintain product catalogs, process orders, and engage with customers through real-time messaging. Administrators maintain platform integrity by overseeing operations, managing users, and monitoring system performance.

## Project Goals

- Enable multiple independent sellers to operate their own shops within a single marketplace
- Deliver a complete e-commerce experience with product browsing, cart management, and secure checkout
- Facilitate real-time communication between customers and sellers for efficient support
- Provide role-specific dashboards for customers, sellers, and administrators
- Ensure secure authentication and payment processing throughout the platform
- Build a scalable architecture ready for production deployment and future growth

## System Architecture Diagram

<img width="1024" height="559" alt="image" src="https://github.com/user-attachments/assets/3198d5dc-5327-4200-b04e-61f6e2ec974e" />


## Key Features

| Feature Category | Feature | Description |
|------------------|---------|-------------|
| **Multi-Role System** | Customer Interface | Browse products, manage cart, track orders, chat with sellers |
| | Seller Dashboard | Manage products, process orders, track shop analytics and revenue |
| | Admin Panel | Oversee platform operations, manage users and orders |
| **Product Management** | Product Search | Real-time search with dropdown results |
| | Category Navigation | Grid-based browsing with category icons |
| | Shopping Cart | Add to cart with real-time stock validation |
| | Wishlist | Save and manage favorite products |
| **Payment Processing** | Stripe Integration | Secure payment handling with conditional rendering |
| | Order Tracking | End-to-end order status visibility |
| **Real-Time Communication** | Customer-Seller Chat | Direct messaging with image support and live updates |
| **Seller Tools** | Revenue Tracking | Monitor earnings and platform service charges |
| | Order Management | Complete order processing dashboard |
| | Product Analytics | Track performance metrics and inventory |
| | Coupon Management | Create and manage promotional discount codes |

## API Architecture

The platform organizes RESTful endpoints into domain-specific routes under the `/api/v2` base path.

### Authentication & Users

| Endpoint | Method | Description | Authentication |
|----------|--------|-------------|----------------|
| `/api/v2/user/register` | POST | Register new user account | Public |
| `/api/v2/user/login` | POST | Authenticate user and receive JWT | Public |
| `/api/v2/user/profile` | GET | Get current user profile | JWT Required |
| `/api/v2/user/update` | PUT | Update user information | JWT Required |

### Seller Management

| Endpoint | Method | Description | Authentication |
|----------|--------|-------------|----------------|
| `/api/v2/seller/shop` | POST | Create new shop | Seller Only |
| `/api/v2/seller/shop/:id` | GET | Get shop details | Seller Only |
| `/api/v2/seller/analytics` | GET | Get revenue and performance metrics | Seller Only |
| `/api/v2/seller/coupons` | POST | Create discount coupon | Seller Only |

### Product Operations

| Endpoint | Method | Description | Authentication |
|----------|--------|-------------|----------------|
| `/api/v2/product` | GET | List all products with filters | Public |
| `/api/v2/product/search` | GET | Real-time product search | Public |
| `/api/v2/product/:id` | GET | Get single product details | Public |
| `/api/v2/product` | POST | Create new product | Seller Only |
| `/api/v2/product/:id` | PUT | Update product | Seller Only |
| `/api/v2/product/:id` | DELETE | Delete product | Seller Only |

### Order Processing

| Endpoint | Method | Description | Authentication |
|----------|--------|-------------|----------------|
| `/api/v2/order` | POST | Create new order | Customer Only |
| `/api/v2/order/user` | GET | Get user order history | JWT Required |
| `/api/v2/order/seller` | GET | Get seller orders | Seller Only |
| `/api/v2/order/:id/status` | PUT | Update order status | Seller/Admin |

### Payment Integration

| Endpoint | Method | Description | Authentication |
|----------|--------|-------------|----------------|
| `/api/v2/payment/create-intent` | POST | Create Stripe payment intent | Customer Only |
| `/api/v2/payment/webhook` | POST | Stripe webhook handler | Public (Stripe) |
| `/api/v2/payment/confirm` | POST | Confirm payment completion | Customer Only |

### Messaging System

| Endpoint | Method | Description | Authentication |
|----------|--------|-------------|----------------|
| `/api/v2/conversation` | GET | Get user conversations | JWT Required |
| `/api/v2/conversation/start` | POST | Start new conversation | JWT Required |
| `/api/v2/messages/:conversationId` | GET | Get conversation messages | JWT Required |
| `/api/v2/messages/send` | POST | Send new message | JWT Required |

### Request/Response Example

**Product Search Request:**
```json
GET /api/v2/product/search?q=laptop&category=electronics&page=1&limit=10
Authorization: Bearer <JWT_TOKEN>
```

**Product Search Response:**
```json
{
  "success": true,
  "data": [
    {
      "_id": "60d21b4667d0d8992e610c85",
      "name": "Gaming Laptop",
      "price": 1299.99,
      "category": "electronics",
      "shop": {
        "name": "Tech Haven",
        "_id": "60d21b4667d0d8992e610c86"
      },
      "images": ["https://cloudinary.com/image1.jpg"],
      "stock": 15
    }
  ],
  "pagination": {
    "page": 1,
    "limit": 10,
    "total": 45,
    "pages": 5
  }
}
```

**Error Response:**
```json
{
  "success": false,
  "error": "Validation Error",
  "message": "Product stock insufficient",
  "statusCode": 400
}
```

## Brand Value Propositions

- **Unified Marketplace Ecosystem** - Connect customers, sellers, and administrators in one seamless platform
- **Multi-Vendor Empowerment** - Enable independent sellers with dedicated dashboards and tools
- **Real-Time Customer Engagement** - Direct messaging for immediate support and inquiries
- **Secure Transactions** - Enterprise-grade payment processing with Stripe integration
- **Scalable Architecture** - Built for growth with modular design and cloud deployment
- **Complete E-Commerce Experience** - From browsing to delivery tracking, everything included
- **Data-Driven Insights** - Analytics dashboards for sellers to optimize performance

## Tech Stack

| Category | Technology | Version | Purpose |
|----------|------------|---------|---------|
| **Frontend** | React | 18.x | User interface library |
| | Vite | Latest | Build tool and development server |
| | Redux Toolkit | Latest | Global state management |
| **Backend** | Node.js | 20.x | JavaScript runtime |
| | Express.js | 5.1.0 | REST API framework |
| | Socket.io | 4.x | Real-time bidirectional communication |
| **Database** | MongoDB | Latest | NoSQL database |
| | Mongoose | 8.17.1 | MongoDB object modeling |
| **Authentication** | JWT | Latest | Token-based authentication |
| | bcrypt | Latest | Password hashing |
| **Payments** | Stripe | 18.5.0 | Payment processing integration |
| **File Storage** | Cloudinary | Latest | Cloud image storage and management |
| | Multer | Latest | File upload handling |
| **Email** | Nodemailer | 7.0.5 | Transactional email service |
| **Deployment** | Vercel | Latest | Hosting and production deployment |
| **Development** | Nodemon | Latest | Auto-restart during development |
| | dotenv | Latest | Environment variable management |


## Folder Structure

```
the-shop-mesh/
├── backend/
│   ├── controllers/
│   │   ├── conversation.js        # Chat conversation logic
│   │   ├── coupounCode.js         # Discount coupon management
│   │   ├── event.js                # Product events/promotions
│   │   ├── messages.js             # Message handling
│   │   ├── order.js                # Order processing
│   │   ├── payment.js              # Payment integration
│   │   ├── product.js              # Product CRUD operations
│   │   ├── shop.js                 # Shop management
│   │   └── user.js                 # User authentication and profile
│   ├── db/
│   │   └── Database.js             # MongoDB connection setup
│   ├── middleware/
│   │   ├── auth.js                  # JWT verification for users
│   │   ├── catchAsyncErrors.js      # Async error wrapper
│   │   └── error.js                 # Error handling middleware
│   ├── models/
│   │   ├── conversation.js          # Chat conversation schema
│   │   ├── coupounCode.js           # Coupon schema
│   │   ├── event.js                  # Event/promotion schema
│   │   ├── messages.js               # Message schema
│   │   ├── order.js                  # Order schema
│   │   ├── product.js                # Product schema
│   │   ├── shop.js                   # Shop schema
│   │   └── user.js                   # User schema
│   ├── routes/
│   │   └── shop.js                   # Shop-related routes
│   ├── utils/
│   │   ├── ErrorHandler.js           # Custom error class
│   │   ├── cloudinary.js             # Cloudinary configuration
│   │   ├── jwtToken.js                # User JWT token generation
│   │   ├── sendMail.js                # Email sending utility
│   │   └── shopToken.js               # Shop JWT token generation
│   ├── app.js                         # Express app configuration
│   ├── multer.js                      # File upload configuration
│   ├── server.js                       # Entry point
│   ├── vercel.json                     # Vercel deployment config
│   ├── package.json
│   └── package-lock.json
│
├── frontend/
│   ├── public/
│   │   └── src/
│   │       ├── ProductDetails/
│   │       │   └── ProductDetailsPage.jsx
│   │       ├── assets/
│   │       │   ├── animations/
│   │       │   │   ├── 107043-success.json
│   │       │   │   └── 24151-ecommerce-animation.json
│   │       │   ├── logo.ico
│   │       │   ├── logo.png
│   │       │   ├── logo1.png
│   │       │   ├── logo12.png
│   │       │   └── logo123.png
│   │       ├── components/
│   │       │   ├── Activation/
│   │       │   │   └── Activation.jsx
│   │       │   ├── Checkout/
│   │       │   ├── Layout/
│   │       │   ├── Login/
│   │       │   ├── Payment/
│   │       │   ├── Products/
│   │       │   ├── Profile/
│   │       │   ├── Route/
│   │       │   ├── Signup/
│   │       │   ├── cart/
│   │       │   ├── shop/
│   │       │   └── Layout/
│   │       │       ├── DashboardHeader.jsx
│   │       │       ├── DashboardSideBar.jsx
│   │       │       ├── AllCoupounsCodes.jsx
│   │       │       ├── AllEvents.jsx
│   │       │       ├── AllOrders.jsx
│   │       │       ├── AllProducts.jsx
│   │       │       ├── AllRefundOrders.jsx
│   │       │       ├── CreateEvent.jsx
│   │       │       ├── CreateProduct.jsx
│   │       │       ├── DashboardHero.jsx
│   │       │       ├── DashboardMessages.jsx
│   │       │       ├── OrderDetails.jsx
│   │       │       ├── ShopCreate.jsx
│   │       │       ├── ShopInfo.jsx
│   │       │       ├── ShopLogin.jsx
│   │       │       ├── ShopProfileData.jsx
│   │       │       ├── ShopSettings.jsx
│   │       │       ├── WithdrawMoney/
│   │       │       │   └── WithdrawMoney.jsx
│   │       │       └── wishlist/
│   │       │           └── Wishlist.jsx
│   │       ├── pages/
│   │       │   ├── Shop/
│   │       │   │   ├── ShopAllCoupouns.jsx
│   │       │   │   ├── ShopAllEvents.jsx
│   │       │   │   ├── ShopAllOrders.jsx
│   │       │   │   ├── ShopAllProduct.jsx
│   │       │   │   ├── ShopAllRefunds.jsx
│   │       │   │   ├── ShopCreateEvent.jsx
│   │       │   │   ├── ShopCreateProduct.jsx
│   │       │   │   ├── ShopDashboardPage.jsx
│   │       │   │   ├── ShopHomePage.jsx
│   │       │   │   ├── ShopInboxPage.jsx
│   │       │   │   ├── ShopOrderDetails.jsx
│   │       │   │   ├── ShopPreviewPage.jsx
│   │       │   │   ├── ShopSettingsPages.jsx
│   │       │   │   └── ShopWithdrawMoneyPage.jsx
│   │       │   ├── ActivationPage.jsx
│   │       │   ├── BestSellingPage.jsx
│   │       │   ├── CheckoutPage.jsx
│   │       │   ├── EvetsPage.jsx
│   │       │   ├── FAQPage.jsx
│   │       │   ├── HomePage.jsx
│   │       │   ├── LoginPage.jsx
│   │       │   ├── OrderDetailsPage.jsx
│   │       │   ├── OrderSuccessPage.jsx
│   │       │   ├── PaymentPage.jsx
│   │       │   ├── ProductsPage.jsx
│   │       │   ├── ProfilePage.jsx
│   │       │   ├── ShopCreatePage.jsx
│   │       │   ├── ShopLoginPage.jsx
│   │       │   ├── SignupPage.jsx
│   │       │   ├── TrackOrderPage.jsx
│   │       │   └── UserOrderDeails.jsx
│   │       ├── protectedRoutes/
│   │       │   ├── ProtectedRoute.jsx
│   │       │   └── SellerProtectedRoute.jsx
│   │       ├── redux/
│   │       │   ├── actions/
│   │       │   │   ├── cart.js
│   │       │   │   ├── event.js
│   │       │   │   ├── order.js
│   │       │   │   ├── product.js
│   │       │   │   ├── seller.js
│   │       │   │   ├── user.js
│   │       │   │   └── wishlist.js
│   │       │   ├── reducers/
│   │       │   │   ├── cart.js
│   │       │   │   ├── event.js
│   │       │   │   ├── order.js
│   │       │   │   ├── product.js
│   │       │   │   ├── seller.js
│   │       │   │   ├── user.js
│   │       │   │   └── wishlist.js
│   │       │   └── store.js
│   │       ├── routes/
│   │       │   ├── Routes.js
│   │       │   └── ShopRoutes.js
│   │       ├── static/
│   │       │   └── data.js
│   │       ├── styles/
│   │       │   └── styles.js
│   │       ├── App.css
│   │       ├── App.jsx
│   │       ├── SellerActivationPage.jsx
│   │       ├── index.css
│   │       └── main.jsx
│   ├── README.md
│   ├── eslint.config.js
│   ├── index.html
│   ├── package-lock.json
│   ├── package.json
│   ├── postcss.config.js
│   ├── server.js
│   ├── tailwind.config.js
│   ├── vercel.json
│   └── vite.config.js
│
├── socket/
│   └── index.js                      # Socket.io server configuration
│
├── .gitignore
└── README.md
```
## Challenges & Solutions

| Challenge | Solution |
|-----------|----------|
| Token expiration during sign-up | Adjusted React Strict Mode to prevent token re-render issues |
| Database schema validation errors | Reviewed and corrected Mongoose schemas with proper validation rules |
| Redux state not updating consistently | Implemented async actions with proper state slices and reducers |
| Stripe payment integration failures | Used Stripe sandbox environment for comprehensive testing before production deployment |
| Image upload handling at scale | Migrated from local storage to Cloudinary for better scalability and performance |
| Vercel deployment configuration issues | Properly configured environment variables and server reload management |
| LocalStorage session management problems | Implemented robust JSON parsing with error handling for session data |
| Data fetching and display inconsistencies | Established consistent API call patterns with React hooks and error boundaries |
| Express middleware configuration | Correctly configured authentication, validation, and error handling middleware chain |
| Real-time connection stability | Implemented Socket.io with reconnection logic and fallback mechanisms |

## Application Flow

### Customer Journey

1. **Discovery Phase**
   - User visits platform and browses product categories
   - Searches for specific products using real-time search
   - Views product details, images, and seller information

2. **Engagement Phase**
   - Adds products to cart or wishlist
   - Initiates chat with seller for product inquiries
   - Receives real-time responses via Socket.io

3. **Transaction Phase**
   - Proceeds to checkout
   - Completes payment via Stripe integration
   - Receives order confirmation email

4. **Post-Purchase Phase**
   - Tracks order status in dashboard
   - Receives updates on order processing
   - Continues communication with seller if needed

### Seller Journey

1. **Onboarding**
   - Registers as seller and creates shop profile
   - Sets up product catalog with images via Cloudinary

2. **Daily Operations**
   - Monitors dashboard for new orders and revenue
   - Processes orders and updates status
   - Manages inventory and creates promotions

3. **Customer Engagement**
   - Responds to customer inquiries via chat
   - Provides support and builds relationships

4. **Analytics Review**
   - Reviews sales performance metrics
   - Analyzes product popularity and adjusts strategy

### Admin Journey

1. **Platform Monitoring**
   - Reviews user registrations and activity
   - Monitors overall order volume and revenue

2. **Management Tasks**
   - Handles user disputes or issues
   - Manages platform policies and configurations

3. **System Oversight**
   - Reviews performance metrics
   - Ensures platform stability and security

## Error Handling & UX

### Error Types and Responses

| Error Type | User Experience | Technical Handling |
|------------|-----------------|-------------------|
| **Authentication Errors** | Clear message about invalid credentials with option to reset password | 401 responses with specific error codes |
| **Validation Errors** | Field-level highlighting with descriptive error messages | 422 status with validation details |
| **Payment Failures** | Friendly message with troubleshooting steps and retry option | Stripe error mapping to user-friendly messages |
| **Network Issues** | Offline indicator with auto-reconnect on connection restoration | Exponential backoff retry with max attempts |
| **Server Errors** | Apologetic message with request ID for support reference | 500 error logging with detailed context |
| **Stock Validation** | Real-time stock checking with unavailable item indicators | Prevents checkout of out-of-stock items |

### UX Principles

- **Progressive Disclosure** - Complex features revealed as needed
- **Real-Time Feedback** - All actions trigger immediate visual response
- **Persistent State** - Cart and wishlist survive page refreshes via localStorage
- **Skeleton Loading** - Content placeholders prevent layout shift
- **Error Recovery** - One-click form reset and retry options
- **Accessibility** - ARIA labels and keyboard navigation support
- **Responsive Design** - Optimized for all device sizes
- **Toast Notifications** - Non-intrusive success/error messages

## Conclusion

The Shop Mesh Multi-Vendor E-Commerce Platform delivers a production-ready solution that unites customers, sellers, and administrators in one comprehensive ecosystem. Built with modern technologies and following industry best practices, the platform provides:

- **Scalable Architecture** - Modular design supporting growth from dozens to thousands of sellers
- **Secure Transactions** - Enterprise-grade payment processing with Stripe integration
- **Real-Time Engagement** - Instant communication between customers and sellers
- **Role-Specific Experiences** - Tailored interfaces for each user type
- **Production Readiness** - Deployed on Vercel with proper environment configuration

### Next Steps

- Implement advanced analytics and reporting dashboards
- Add mobile applications for iOS and Android
- Integrate additional payment gateways
- Enhance recommendation engine with AI/ML
- Expand multi-language and multi-currency support
- Implement PWA capabilities for offline access

The platform is ready for real-world deployment and future growth, providing both technical excellence and tangible business value.
