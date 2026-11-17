# 🛒 Grocery Management System

A full-stack mobile application developed for the **Year 2, Semester 2 Web and Mobile Technology group project at SLIIT**. Customers can browse stores, order groceries, and track deliveries. Administrators use a separate dashboard to manage stores, products, orders, payments, and support requests.

## Stakeholders

| Stakeholder | Role in the system |
| --- | --- |
| Customers | Browse stores and products, manage their cart, place orders, choose a payment method, track deliveries, and request support. |
| Store administrators | Maintain store information, product listings, and prices. |
| Order and delivery administrators | Review incoming orders and update order and delivery statuses. |
| Payment and support administrators | Review payment records and respond to support tickets. |

The application has two account roles, **Customer** and **Admin**. The administrative responsibilities above are handled through the Admin dashboard.

## Features

| Area | Customer app | Admin dashboard |
| --- | --- | --- |
| Stores and products | Browse stores and view product details and prices. | Manage store records, products, and prices. |
| Cart and orders | Add products to a cart, place orders, and view order history. | Review orders and update their status. |
| Payments | Choose Stripe card payment, bank transfer, or cash on delivery. View payment history. | Review payment records. |
| Delivery tracking | Check delivery progress from the app. | Post tracking updates. |
| Support | Submit support tickets. | Review and respond to tickets. |

Authentication uses **JWT** and **bcrypt** password hashing. Password resets use one-time codes sent by email through Nodemailer.

## How an order moves through the system

1. A customer selects a store and adds products to the cart.
2. The customer places the order and chooses a payment method.
3. An administrator reviews the order and posts status and delivery updates.
4. The customer follows the updates from the order history and can submit a support ticket if needed.

## My contribution

**Dilmi Amarakoon** developed the product-entry and pricing-list functionality, which allows products to be added to the store catalog and their prices displayed.

## Tech stack and architecture

| Layer | Technology |
| --- | --- |
| Mobile app | React Native, Expo, React Navigation, Context API, Axios, AsyncStorage |
| REST API | Node.js and Express |
| Database | MongoDB and Mongoose |
| Integrations | Stripe for card payments, Nodemailer for email OTPs, and Multer for file uploads |

The mobile app sends requests to the Express REST API. The API handles application logic and reads or writes records in MongoDB through Mongoose.

## Repository structure

| Path | Contents |
| --- | --- |
| [`frontend/src/screens/`](frontend/src/screens/) | Authentication, customer, and admin screens |
| [`frontend/src/navigation/`](frontend/src/navigation/) | App navigation |
| [`frontend/src/config/api.js`](frontend/src/config/api.js) | Backend URL configuration |
| [`backend/routes/`](backend/routes/) | Endpoints for authentication, stores, products, orders, payments, tracking, and support |
| [`backend/controllers/`](backend/controllers/) | Request handling and application logic |
| [`backend/models/`](backend/models/) | MongoDB schemas |
| [`backend/server.js`](backend/server.js) | Express server entry point |

## Run locally

### 1. Install and configure the backend

Install Node.js with npm and have a MongoDB connection string ready. Open a terminal in the folder containing both `backend` and `frontend`.

```powershell
cd backend
npm install
```

Create `backend/.env` with your local settings.

```dotenv
PORT=5000
MONGO_URI=your_mongodb_connection_string
JWT_SECRET=your_long_random_secret
JWT_EXPIRE=7d
EMAIL_USER=your_gmail_address
EMAIL_PASS=your_google_app_password
STRIPE_SECRET_KEY=your_stripe_test_secret_key
STRIPE_CURRENCY=lkr
```

The email values configure password reset OTPs. Use Stripe test credentials for local card payment testing. Keep the filled-in `.env` file out of GitHub.

Start the API from the `backend` folder.

```powershell
npm run dev
```

Open [http://localhost:5000](http://localhost:5000) on your computer. The server should return `{"message":"Grocery Management API is running"}`.

### 2. Connect and start the mobile app

In [`frontend/src/config/api.js`](frontend/src/config/api.js), set `SERVER_URL` to your computer’s Wi-Fi IPv4 address and backend port.

```js
export const SERVER_URL = "http://192.168.1.10:5000";
```

Replace the sample IP with your own. On Windows, run `ipconfig` to find it. Connect the phone and computer to the same Wi-Fi network. The app appends `/api` to the server URL automatically.

For card payment testing, set `STRIPE_PUBLISHABLE_KEY` in [`frontend/App.js`](frontend/App.js) to the matching Stripe test publishable key.

Open a second terminal at the project root.

```powershell
cd frontend
npm install
npm start
```

Open the project on an Expo-compatible device or emulator. If Expo Go cannot load the Stripe native module, use an Expo development build.

### 3. Try both roles

- **Admin** · Review [`backend/seed-admin.js`](backend/seed-admin.js), set your own local admin credentials, and run `node seed-admin.js` from `backend` against your local database. Sign in and add a store and a few products.
- **Customer** · Register through the app, open the store, and place a test order. Use cash on delivery to try the order flow without configuring Stripe.

## Academic context

**SLIIT · Web and Mobile Technology · Year 2, Semester 2 · Group project**
 
