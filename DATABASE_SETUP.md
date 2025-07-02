# Database Setup Guide

## Overview
This project now uses MongoDB as the database instead of static data. All products, users, and orders are stored in the database.

## Prerequisites
1. MongoDB installed and running locally, OR
2. MongoDB Atlas account (cloud database)

## Setup Instructions

### 1. Install MongoDB (if using local database)
- **Windows**: Download and install from [MongoDB Download Center](https://www.mongodb.com/try/download/community)
- **macOS**: `brew install mongodb-community`
- **Linux**: Follow [MongoDB installation guide](https://docs.mongodb.com/manual/installation/)

### 2. Configure Environment Variables

Create a `.env` file in the `server` directory with the following content:

```env
# Server Configuration
PORT=5000
NODE_ENV=development

# Database Configuration
MONGODB_URI=mongodb://localhost:27017/shopmate

# JWT Configuration
JWT_SECRET=your-super-secret-jwt-key-change-this-in-production
JWT_EXPIRE=7d

# Stripe Configuration (for payments)
STRIPE_SECRET_KEY=your-stripe-secret-key
STRIPE_PUBLISHABLE_KEY=your-stripe-publishable-key

# CORS Configuration
CORS_ORIGIN=http://localhost:3000
```

### 3. Using MongoDB Atlas (Cloud Database)

If you prefer to use MongoDB Atlas:

1. Create an account at [MongoDB Atlas](https://www.mongodb.com/atlas)
2. Create a new cluster
3. Get your connection string
4. Update the `MONGODB_URI` in your `.env` file:
   ```env
   MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/shopmate
   ```

### 4. Populate the Database

Run the database seeder to populate products:

```bash
cd server
npm run seed
```

This will:
- Connect to your MongoDB database
- Clear any existing products
- Insert 24 sample products across all categories

### 5. Start the Application

1. Start the backend server:
   ```bash
   cd server
   npm install
   npm run dev
   ```

2. Start the frontend:
   ```bash
   cd client
   npm install
   npm start
   ```

## Database Schema

### Products Collection
- `_id`: MongoDB ObjectId
- `name`: String (required)
- `description`: String (required)
- `price`: Number (required)
- `category`: String (required)
- `images`: Array of strings (image URLs)
- `stock`: Number (default: 0)
- `averageRating`: Number (calculated from ratings)
- `ratings`: Array of rating objects
- `featured`: Boolean (default: false)
- `specifications`: Object (product specs)
- `createdAt`: Date
- `updatedAt`: Date

### Users Collection
- `_id`: MongoDB ObjectId
- `name`: String (required)
- `email`: String (required, unique)
- `password`: String (hashed, required)
- `role`: String (enum: 'user', 'admin')
- `address`: Object (shipping address)
- `phone`: String
- `orders`: Array of Order ObjectIds
- `createdAt`: Date
- `updatedAt`: Date

### Orders Collection
- `_id`: MongoDB ObjectId
- `user`: ObjectId (ref: User)
- `items`: Array of order items
- `shippingAddress`: Object
- `paymentMethod`: String
- `totalPrice`: Number
- `status`: String (enum: pending, processing, shipped, delivered, cancelled)
- `trackingNumber`: String
- `createdAt`: Date
- `updatedAt`: Date

## API Endpoints

### Products
- `GET /api/products` - Get all products (with filtering, sorting, pagination)
- `GET /api/products/:id` - Get single product
- `POST /api/products` - Create product (admin only)
- `PUT /api/products/:id` - Update product (admin only)
- `DELETE /api/products/:id` - Delete product (admin only)
- `POST /api/products/:id/ratings` - Add product rating

### Authentication
- `POST /api/auth/register` - Register new user
- `POST /api/auth/login` - Login user
- `GET /api/auth/profile` - Get user profile
- `PUT /api/auth/profile` - Update user profile

### Orders
- `POST /api/orders` - Create new order
- `GET /api/orders` - Get user orders
- `GET /api/orders/:id` - Get specific order
- `PUT /api/orders/:id/status` - Update order status (admin only)

## Frontend Changes

The frontend has been updated to:
1. Fetch products from the API instead of using static data
2. Use MongoDB ObjectIds (`_id`) instead of numeric IDs
3. Handle loading and error states
4. Support real-time data updates

## Troubleshooting

### Common Issues

1. **MongoDB Connection Error**
   - Ensure MongoDB is running
   - Check your connection string
   - Verify network connectivity (for Atlas)

2. **CORS Errors**
   - Ensure the frontend is running on the correct port
   - Check CORS_ORIGIN in your .env file

3. **JWT Errors**
   - Ensure JWT_SECRET is set in your .env file
   - Check token expiration settings

4. **Product Images Not Loading**
   - Verify image URLs in the database
   - Check if images are accessible

### Getting Help

If you encounter issues:
1. Check the server console for error messages
2. Verify your environment variables
3. Ensure all dependencies are installed
4. Check MongoDB connection status 

# Terminal 1 - Backend
cd server && npm run dev

# Terminal 2 - Frontend  
cd client && npm start 