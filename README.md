 # 🛒 Grocery Management System

A full-stack grocery shopping app built for the **Year 2, Semester 2 Web and Mobile Technology group project at SLIIT**. Customers can browse stores, order groceries, and track deliveries. Administrators manage the catalog, orders, payments, and support requests from a separate dashboard.

## Features

| Customer app | Admin dashboard |
| --- | --- |
| Browse stores and products, and view product details | Manage stores and product listings |
| Add products to a cart and place orders | View orders and update their status |
| Pay by Stripe card, online transfer, or cash on delivery | Review payment records |
| View order and payment history, and track deliveries | Manage delivery tracking updates |
| Submit support requests | Review and respond to support tickets |

The app uses JWT-based authentication, bcrypt password hashing, and email OTPs for password resets.

## Tech stack

| Layer | Technologies |
| --- | --- |
| Mobile app | React Native, Expo SDK 54, React Navigation, Context API, Axios, AsyncStorage |
| REST API | Node.js, Express |
| Database | MongoDB, Mongoose |
| Integrations | Stripe, Nodemailer, Multer |

## Run locally

You’ll need Node.js with npm and a MongoDB connection string. Extract the ZIP and open the folder that contains both `backend` and `frontend`.

### 1. Start the backend

In your first terminal, run:

```bash
cd backend
npm install
```

Create a `backend/.env` file with your own values:

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

The email settings are used for password reset OTPs. Use Stripe test credentials for local card payment testing. Keep your filled-in `.env` out of GitHub.

With the terminal still in `backend`, start the API:

```bash
npm run dev
```

Open [http://localhost:5000](http://localhost:5000) on your computer. The API should return `{"message":"Grocery Management API is running"}`.

### 2. Connect and start the mobile app

The checked-in [API configuration](frontend/src/config/api.js) points to a Render backend. To use your local backend from a phone, change `SERVER_URL` to your computer’s Wi-Fi IPv4 address and port. Use `ipconfig` on Windows to find the address, and connect both devices to the same Wi-Fi network.

```js
export const SERVER_URL = "http://192.168.1.10:5000";
```

Replace `192.168.1.10` with your own address. The app adds `/api` automatically. For card payment testing, set `STRIPE_PUBLISHABLE_KEY` in [frontend/App.js](frontend/App.js) to the publishable test key from the same Stripe account as your backend test secret.

In a second terminal opened at the project root, run:

```bash
cd frontend
npm install
npm start
```

Open the app on an Expo-compatible device or emulator. Use an Expo development build if Expo Go cannot load the project’s Stripe native module.

### 3. Try the two roles

- **Customer:** Register in the app, then browse stores and products. For an empty local database, create a store and products through the admin dashboard first.
- **Admin:** Review the starter account in [backend/seed-admin.js](backend/seed-admin.js) and set your own credentials before running `node seed-admin.js` from the `backend` folder against your local database.

## Repository structure

| Location | Contents |
| --- | --- |
| [frontend/src/screens](frontend/src/screens/) | Authentication, customer, and administrator screens |
| [frontend/src/navigation](frontend/src/navigation/) | App navigation |
| [backend/routes](backend/routes/) | REST endpoints for authentication, products, stores, orders, payments, tracking, and support |
| [backend/controllers](backend/controllers/) | Request handling and business logic |
| [backend/models](backend/models/) | MongoDB schemas |
| [backend/server.js](backend/server.js) | Express server entry point |
