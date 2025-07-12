# LMS (Learning Management System) - Server

A comprehensive Learning Management System backend built with Node.js, Express.js, and MongoDB. This system provides APIs for user management, course management, payment processing, and more.

## 🚀 Features

- **User Management**: Registration, login, profile management, password reset
- **Course Management**: Create, read, update, delete courses with multimedia support
- **Authentication & Authorization**: JWT-based authentication with role-based access
- **Payment Integration**: Razorpay payment gateway integration
- **File Upload**: Cloudinary integration for image/video uploads
- **Email Service**: Nodemailer for email notifications
- **Error Handling**: Centralized error handling middleware
- **Security**: CORS, cookie parsing, bcrypt password hashing

## 🛠️ Tech Stack

- **Runtime**: Node.js
- **Framework**: Express.js
- **Database**: MongoDB with Mongoose ODM
- **Authentication**: JSON Web Tokens (JWT)
- **File Storage**: Cloudinary
- **Payment Gateway**: Razorpay
- **Email Service**: Nodemailer
- **Password Hashing**: bcryptjs
- **Development**: Nodemon for auto-restart

## 📋 Prerequisites

Before you begin, ensure you have the following installed:

- [Node.js](https://nodejs.org/) (v14 or higher)
- [MongoDB](https://www.mongodb.com/) (v4.4 or higher)
- [npm](https://www.npmjs.com/) or [yarn](https://yarnpkg.com/)

## ⚙️ Environment Variables

Create a `.env` file in the server directory and add the following environment variables:

```env
# Server Configuration
PORT=5000
NODE_ENV=development

# Frontend URL (for CORS)
FRONTEND_URL=http://localhost:3000

# Database
MONGO_URI=mongodb://127.0.0.1:27017/lms

# JWT Configuration
JWT_SECRET=your_jwt_secret_key_here
JWT_EXPIRY=24h

# Cloudinary Configuration (for file uploads)
CLOUDINARY_CLOUD_NAME=your_cloudinary_cloud_name
CLOUDINARY_API_KEY=your_cloudinary_api_key
CLOUDINARY_API_SECRET=your_cloudinary_api_secret

# Razorpay Configuration (for payments)
RAZORPAY_KEY_ID=your_razorpay_key_id
RAZORPAY_SECRET=your_razorpay_secret

# Email Configuration (Nodemailer)
SMTP_HOST=your_smtp_host
SMTP_PORT=587
SMTP_USERNAME=your_email_username
SMTP_PASSWORD=your_email_password
FROM_EMAIL=noreply@yourdomain.com
```

## 🚀 Installation & Setup

1. **Clone the repository**
   ```bash
   git clone <your-repository-url>
   cd lms/server
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Setup environment variables**
   ```bash
   cp .env.example .env
   # Edit .env file with your configuration
   ```

4. **Start MongoDB**
   ```bash
   # If using local MongoDB
   mongod
   
   # Or if using MongoDB service
   sudo systemctl start mongod
   ```

5. **Run the application**
   
   **Development mode:**
   ```bash
   npm run dev
   ```
   
   **Production mode:**
   ```bash
   npm start
   ```

## 📁 Project Structure

```
server/
├── app.js                      # Express app configuration
├── server.js                   # Server entry point
├── package.json                # Dependencies and scripts
├── .env                        # Environment variables (create this)
├── configs/
│   └── dbConn.js              # Database connection configuration
├── controllers/
│   ├── course.controller.js    # Course-related business logic
│   ├── miscellaneous.controller.js # Miscellaneous endpoints
│   ├── payment.controller.js   # Payment processing logic
│   └── user.controller.js      # User management logic
├── middlewares/
│   ├── asyncHandler.middleware.js  # Async error handling
│   ├── auth.middleware.js      # Authentication middleware
│   ├── error.middleware.js     # Global error handling
│   └── multer.middleware.js    # File upload middleware
├── models/
│   ├── course.model.js         # Course data model
│   ├── Payment.model.js        # Payment data model
│   └── user.model.js           # User data model
├── routes/
│   ├── course.routes.js        # Course API routes
│   ├── miscellaneous.routes.js # Miscellaneous API routes
│   ├── payment.routes.js       # Payment API routes
│   └── user.routes.js          # User API routes
├── uploads/                    # Temporary file uploads directory
└── utils/
    ├── appError.js            # Custom error class
    └── sendEmail.js           # Email utility functions
```

## 🔌 API Endpoints

### User Routes (`/api/v1/user`)
- `POST /register` - Register new user
- `POST /login` - User login
- `GET /logout` - User logout
- `GET /me` - Get current user profile
- `POST /reset` - Password reset request
- `POST /reset/:resetToken` - Reset password with token
- `POST /change-password` - Change password
- `PUT /update/:id` - Update user profile

### Course Routes (`/api/v1/courses`)
- `GET /` - Get all courses
- `POST /` - Create new course (Admin only)
- `GET /:id` - Get course by ID
- `PUT /:id` - Update course (Admin only)
- `DELETE /:id` - Delete course (Admin only)
- `POST /:id/lectures` - Add lecture to course (Admin only)

### Payment Routes (`/api/v1/payments`)
- `GET /razorpay-key` - Get Razorpay public key
- `POST /subscribe` - Create subscription
- `POST /verify` - Verify payment
- `POST /unsubscribe` - Cancel subscription
- `GET /` - Get all payments (Admin only)

### Miscellaneous Routes (`/api/v1`)
- `POST /contact` - Contact form submission

## 🔧 Development

### Available Scripts

- `npm start` - Start the production server
- `npm run dev` - Start the development server with nodemon

### Adding New Features

1. **Models**: Add new data models in `/models`
2. **Controllers**: Add business logic in `/controllers`
3. **Routes**: Define API endpoints in `/routes`
4. **Middlewares**: Add custom middlewares in `/middlewares`

## 🔐 Authentication Flow

1. User registers/logs in with credentials
2. Server validates and returns JWT token
3. Client stores token and sends it in subsequent requests
4. Server validates token using auth middleware
5. Access granted based on user role and permissions

## 📤 File Upload Flow

1. Client sends file through multipart form data
2. Multer middleware processes the upload
3. File is temporarily stored in `/uploads`
4. Cloudinary uploads file to cloud storage
5. File URL is stored in database
6. Temporary file is cleaned up

## 🚨 Error Handling

The application uses centralized error handling:

- Custom `AppError` class for operational errors
- `asyncHandler` middleware for catching async errors
- Global error middleware for formatting responses
- Environment-specific error responses

## 🧪 Testing

To test the API endpoints, you can use:

- [Postman](https://www.postman.com/)
- [Insomnia](https://insomnia.rest/)
- [Thunder Client](https://www.thunderclient.io/) (VS Code extension)

Import the provided collection or manually test endpoints using the documentation above.

## 🔍 Troubleshooting

### Common Issues

1. **MongoDB Connection Error**
   - Ensure MongoDB is running
   - Check MONGO_URI in .env file
   - Verify database permissions

2. **Cloudinary Upload Fails**
   - Verify Cloudinary credentials in .env
   - Check file size limits
   - Ensure proper file formats

3. **Payment Integration Issues**
   - Verify Razorpay credentials
   - Check webhook configurations
   - Ensure proper currency settings

4. **Email Not Sending**
   - Verify SMTP credentials
   - Check spam folders
   - Ensure proper email configuration

### Debug Mode

Set `NODE_ENV=development` in your .env file to enable:
- Detailed error messages
- Request logging with Morgan
- Stack traces in responses

## 📚 Additional Resources

- [Express.js Documentation](https://expressjs.com/)
- [MongoDB Documentation](https://docs.mongodb.com/)
- [Mongoose Documentation](https://mongoosejs.com/)
- [Cloudinary Documentation](https://cloudinary.com/documentation)
- [Razorpay Documentation](https://razorpay.com/docs/)

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests if applicable
5. Submit a pull request

PS: This readme is generated by Copilot. 