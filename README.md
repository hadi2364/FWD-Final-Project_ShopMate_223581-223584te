# ShopMate - E-Commerce Platform

A modern, full-stack e-commerce platform built with the MERN stack (MongoDB, Express.js, React.js, Node.js) inspired by Shopify.

## Features

- 🔐 Secure user authentication with JWT
- 🛍️ Product management system with database storage
- 🛒 Shopping cart functionality with localStorage persistence
- 💳 Secure payment processing (Stripe/PayPal integration)
- 📦 Order tracking and management
- 🔍 Advanced search and filtering
- 📱 Responsive design for all devices
- ⭐ Product ratings and reviews
- 👤 User profile management
- 🏷️ Category-based product organization

## Tech Stack

- **Frontend**: React.js, Material-UI, React Router, Axios
- **Backend**: Node.js, Express.js, Mongoose
- **Database**: MongoDB
- **Authentication**: JWT with bcrypt password hashing
- **Payment**: Stripe integration
- **State Management**: React Context API
- **Styling**: Material-UI with custom theme

## Project Structure

```
shopmate/
├── client/                 # Frontend React application
│   ├── src/
│   │   ├── components/     # Reusable UI components
│   │   ├── pages/         # Page components
│   │   ├── context/       # React Context providers
│   │   ├── services/      # API services
│   │   └── utils/         # Utility functions
├── server/                 # Backend Node.js/Express application
│   ├── src/
│   │   ├── models/        # MongoDB schemas
│   │   ├── routes/        # API routes
│   │   ├── middleware/    # Custom middleware
│   │   ├── controllers/   # Route controllers
│   │   ├── config/        # Configuration files
│   │   └── seeders/       # Database seeders
├── DATABASE_SETUP.md      # Database setup guide
└── README.md
```

## Getting Started

### Prerequisites

- Node.js (v14 or higher)
- MongoDB (local installation or MongoDB Atlas)
- npm or yarn

### Installation

1. **Clone the repository**
```bash
git clone [repository-url]
cd shopmate
```

2. **Install backend dependencies**
```bash
cd server
npm install
```

3. **Install frontend dependencies**
```bash
cd client
npm install
```

4. **Set up environment variables**

Create a `.env` file in the `server` directory:
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

5. **Set up the database**

For detailed database setup instructions, see [DATABASE_SETUP.md](./DATABASE_SETUP.md)

Quick setup:
```bash
# Start MongoDB (if using local installation)
mongod

# Populate the database with sample products
cd server
npm run seed
```

6. **Start the development servers**

Backend:
```bash
cd server
npm run dev
```

Frontend:
```bash
cd client
npm start
```

The application will be available at:
- Frontend: http://localhost:3000
- Backend API: http://localhost:5000

## Database Integration

This project now uses MongoDB as the primary database instead of static data. Key features:

- **Real-time data**: All products, users, and orders are stored in MongoDB
- **Scalable**: Database can handle large product catalogs and user bases
- **Secure**: User passwords are hashed with bcrypt
- **Flexible**: Easy to add new product categories and features

### Sample Data

The database seeder includes 24 sample products across 7 categories:
- Electronics (6 products)
- Fashion (4 products)
- Beauty (4 products)
- Home (2 products)
- Sports (2 products)
- Books (2 products)
- Toys (2 products)

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

## Features in Detail

### User Authentication
- Secure registration and login
- JWT token-based authentication
- Password hashing with bcrypt
- Protected routes
- User profile management

### Product Management
- Database-driven product catalog
- Category-based organization
- Advanced search and filtering
- Product ratings and reviews
- Stock management
- Featured products

### Shopping Experience
- Add/remove items from cart
- Quantity management
- Cart persistence (localStorage)
- Real-time price calculations
- Stock validation

### Order Processing
- Multi-step checkout process
- Shipping address collection
- Payment method selection
- Order confirmation
- Order history tracking

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License.

## Support

For database setup issues, see [DATABASE_SETUP.md](./DATABASE_SETUP.md)

For general questions or issues, please open an issue on GitHub. 