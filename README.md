# HireBridge

An AI-powered interview preparation platform that helps job seekers practice and improve their interview skills through simulated technical and HR interviews.

## 🚀 Features

- **AI-Generated Questions**: Dynamic interview questions tailored to your role and experience level
- **Dual Interview Modes**: 
  - Technical interviews for coding and technical skills
  - HR interviews for behavioral and situational questions
- **Resume Analysis**: Upload your resume to get personalized interview questions
- **Real-time Feedback**: Get instant feedback on your answers with scoring
- **Interview History**: Track your progress and view past interview reports
- **Credit System**: Start with 100 credits and purchase more as needed
- **Payment Integration**: Secure payment processing via Razorpay

## 🏗️ Architecture

### Frontend (Client)
- **Framework**: React 19 with Vite
- **Styling**: TailwindCSS
- **State Management**: Redux Toolkit
- **Routing**: React Router DOM
- **UI Components**: Custom components with React Icons
- **Charts**: Recharts for data visualization
- **PDF Generation**: jsPDF for interview reports

### Backend (Server)
- **Runtime**: Node.js with ES Modules
- **Framework**: Express.js
- **Database**: MongoDB with Mongoose
- **Authentication**: JWT tokens with HTTP-only cookies
- **File Upload**: Multer for resume processing
- **PDF Processing**: PDF.js for resume text extraction
- **Payment**: Razorpay integration
- **AI Integration**: OpenRouter API for question generation

## 📁 Project Structure

```
HireBridge/
├── client/                 # React frontend application
│   ├── src/
│   │   ├── components/     # Reusable UI components
│   │   ├── pages/         # Page components
│   │   ├── redux/         # Redux store and slices
│   │   └── utils/         # Utility functions
│   ├── public/            # Static assets
│   └── package.json       # Frontend dependencies
├── server/                # Express backend application
│   ├── config/           # Database and configuration files
│   ├── controllers/      # Route controllers
│   ├── middlewares/      # Custom middlewares
│   ├── models/          # MongoDB models
│   ├── routes/          # API routes
│   ├── services/        # Business logic services
│   └── package.json     # Backend dependencies
└── README.md           # This file
```

## 🛠️ Tech Stack

### Frontend
- React 19.2.0
- Vite 7.3.1
- TailwindCSS 4.1.18
- Redux Toolkit 2.11.2
- React Router DOM 7.13.0
- Axios 1.13.5
- Recharts 3.7.0
- jsPDF 4.2.0

### Backend
- Node.js (ES Modules)
- Express 5.2.1
- MongoDB with Mongoose 9.2.1
- JWT 9.0.3
- Multer 2.0.2
- Razorpay 2.9.6
- PDF.js 5.4.624
- CORS 2.8.6
- Cookie-parser 1.4.7

## 🚀 Getting Started

### Prerequisites
- Node.js (v18 or higher)
- MongoDB (local or cloud instance)
- Git

### Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd HireBridge
   ```

2. **Install server dependencies**
   ```bash
   cd server
   npm install
   ```

3. **Install client dependencies**
   ```bash
   cd ../client
   npm install
   ```

4. **Environment Setup**

   **Server Environment (.env in server directory):**
   ```
   MONGODB_URL=your_mongodb_connection_string
   JWT_SECRET=your_jwt_secret_key
   RAZORPAY_KEY_ID=your_razorpay_key_id
   RAZORPAY_KEY_SECRET=your_razorpay_key_secret
   OPENROUTER_API_KEY=your_openrouter_api_key
   PORT=6000
   ```

   **Client Environment (.env in client directory):**
   ```
   VITE_SERVER_URL=http://localhost:6000
   ```

### Running the Application

1. **Start the backend server**
   ```bash
   cd server
   npm run dev
   ```
   Server will run on `http://localhost:6000`

2. **Start the frontend application**
   ```bash
   cd client
   npm run dev
   ```
   Frontend will run on `http://localhost:5173`

## 📊 Database Schema

### User Model
```javascript
{
  name: String (required),
  email: String (required, unique),
  credits: Number (default: 100),
  timestamps: true
}
```

### Interview Model
```javascript
{
  userId: ObjectId (ref: User),
  role: String (required),
  experience: String (required),
  mode: String (enum: ["HR", "Technical"]),
  resumeText: String,
  questions: [{
    question: String,
    difficulty: String,
    timeLimit: Number,
    answer: String,
    feedback: String,
    score: Number,
    confidence: Number,
    communication: Number,
    correctness: Number
  }],
  finalScore: Number,
  status: String (enum: ["Incompleted", "completed"]),
  timestamps: true
}
```

### Payment Model
```javascript
{
  userId: ObjectId (ref: User),
  amount: Number,
  currency: String,
  razorpay_order_id: String,
  razorpay_payment_id: String,
  status: String,
  timestamps: true
}
```

## 🔗 API Endpoints

### Authentication
- `POST /api/auth/register` - User registration
- `POST /api/auth/login` - User login
- `POST /api/auth/logout` - User logout

### User Management
- `GET /api/user/current-user` - Get current user
- `PUT /api/user/update` - Update user profile

### Interview Management
- `POST /api/interview/create` - Create new interview
- `GET /api/interview/get/:id` - Get interview by ID
- `GET /api/interview/history` - Get user interview history
- `POST /api/interview/submit` - Submit interview answers

### Payment
- `POST /api/payment/create-order` - Create Razorpay order
- `POST /api/payment/verify` - Verify payment

## 🎯 Key Features Explained

### Interview Process
1. **Setup**: Choose interview type (HR/Technical), role, and experience level
2. **Resume Upload**: Optional resume upload for personalized questions
3. **AI Questions**: System generates relevant questions using AI
4. **Live Interview**: Answer questions within time limits
5. **Feedback**: Receive detailed feedback and scoring
6. **Report**: Download comprehensive interview report

### Credit System
- New users get 100 free credits
- Each interview consumes credits based on complexity
- Purchase additional credits via integrated payment system

### Scoring Algorithm
- **Correctness**: Accuracy of your answers
- **Communication**: Clarity and structure of responses
- **Confidence**: Demonstrated knowledge and assurance
- **Final Score**: Weighted combination of all metrics

## 🔧 Development

### Adding New Features
1. Backend: Add routes in `/server/routes/`, controllers in `/server/controllers/`
2. Frontend: Add components in `/client/src/components/`, pages in `/client/src/pages/`
3. State: Update Redux slices in `/client/src/redux/`

### Code Style
- ES6+ JavaScript with ES Modules
- Functional React components with hooks
- TailwindCSS for styling
- RESTful API design

## 🚀 Deployment

### Frontend (Vercel/Netlify)
```bash
cd client
npm run build
```
Deploy the `dist` folder

### Backend (Render/Heroku)
```bash
cd server
npm start
```
Ensure environment variables are set in production

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the ISC License.

## 📞 Support

For support, please contact [your-email@example.com] or create an issue in the repository.

---

**HireBridge** - Bridge the gap between preparation and success! 🌉
