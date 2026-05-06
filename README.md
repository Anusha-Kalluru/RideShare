# 🚗 RideShare - Full Stack Web Application

## 📌 Project Overview
RideShare is a comprehensive full-stack MERN web application designed to connect drivers with passengers. The platform facilitates a seamless ride-booking experience, featuring real-time messaging, map integrations for route planning, an admin dashboard, and robust user authentication. It addresses the real-world problem of commuting by offering an affordable and environmentally friendly carpooling alternative.

## 🚀 Features Implemented
- **Role-Based Authentication:** Secure JWT-based login and registration for three distinct user roles: `user`, `driver`, and `admin`.
- **Ride Management:** Drivers can post new rides specifying departure, destination, date, time, price, and available seats.
- **Booking System:** Passengers can search, view, and book available rides. Drivers manage their bookings directly from their dashboard.
- **Real-Time Messaging:** Integrated Socket.io for live chat between passengers and drivers.
- **Admin Dashboard:** Exclusive administrative portal to monitor users, manage rides, and resolve platform complaints.
- **Reviews & Ratings:** Passengers can leave ratings and comments for drivers after a ride is completed.
- **Complaint System:** Users can report issues or lodge complaints that admins can subsequently resolve.
- **Maps Integration:** Visual representation of rides and routes using React Leaflet and Google Maps API.
- **Notifications:** *(Partially Implemented/In Progress)* - Basic alert structures present but full push-notification workflow is still in development.

## 💻 Tech Stack
**Frontend:**
- React (v18)
- React Router DOM
- Vanilla CSS (Custom Design System, Glassmorphism UI)
- Leaflet & React-Leaflet (Map Rendering)
- @react-google-maps/api (Location Services)
- Socket.io-client (Real-time events)
- Axios (HTTP Client)
- Vite (Build Tool)

**Backend:**
- Node.js & Express.js
- MongoDB & Mongoose (ODM)
- JSON Web Token (JWT) & bcryptjs (Authentication & Security)
- Socket.io (WebSockets for live chat)
- Cors & Dotenv

## 📂 Folder Structure
```text
RideShare/
├── client/                     # Frontend React Application
│   ├── src/
│   │   ├── api/                # API communication layers
│   │   ├── components/         # Reusable UI components (Navbar, etc.)
│   │   ├── context/            # React Context (AuthContext)
│   │   ├── pages/              # Route pages (Home, Login, AdminDashboard, etc.)
│   │   ├── App.jsx             # Main router configuration
│   │   └── index.css           # Global custom CSS styling
│   ├── package.json            # Frontend dependencies
│   └── vite.config.js          # Vite configurations
└── server/                     # Backend Express Application
    ├── config/                 # DB connection and setup
    ├── controllers/            # Business logic (auth, ride, booking, etc.)
    ├── middleware/             # Express middlewares (auth protection, roles)
    ├── models/                 # Mongoose database schemas
    ├── routes/                 # API route definitions
    ├── server.js               # Entry point & Socket.io setup
    └── package.json            # Backend dependencies
```

## ⚙️ Environment Variables Setup
To run this project locally, create `.env` files in both the `server` and `client` directories.

**Backend (`server/.env`):**
```env
PORT=5000
MONGO_URI=your_mongodb_connection_string
JWT_SECRET=your_jwt_secret_key
NODE_ENV=development
```

**Frontend (`client/.env`):**
```env
VITE_GOOGLE_MAPS_API_KEY=your_google_maps_api_key
VITE_API_BASE_URL=http://localhost:5000/api
```

## 🛠️ Installation Guide & Running the App

1. **Clone the repository:**
   ```bash
   git clone <repository-url>
   cd RideShare
   ```

2. **Install Backend Dependencies & Run:**
   ```bash
   cd server
   npm install
   npm run dev
   ```

3. **Install Frontend Dependencies & Run:**
   ```bash
   cd ../client
   npm install
   npm run dev
   ```
   The backend will run on `http://localhost:5000` and the frontend will run on `http://localhost:5173`.

## 🛣️ API Routes Overview
| Route Prefix | Purpose |
| :--- | :--- |
| `/api/auth` | User registration, login, and token generation. |
| `/api/users` | Profile management, retrieving user data. |
| `/api/rides` | Posting rides, searching available rides, fetching ride details. |
| `/api/bookings` | Booking a ride, updating booking status (approve/reject). |
| `/api/messages` | Fetching chat history between users. |
| `/api/reviews` | Submitting and retrieving user ratings. |
| `/api/complaints`| Filing support tickets and issues. |
| `/api/admin` | Fetching platform statistics, managing users and content. |

## 🗄️ Database Collections
- **Users**: Stores `name`, `email`, hashed `password`, `role` (user/driver/admin), and aggregated ratings.
- **Rides**: Contains `driverId`, `departure`, `destination`, `date`, `time`, `price`, `availableSeats`, and `status`.
- **Bookings**: Links a `rideId` and `passengerId`, tracking `seatsBooked` and the approval `status`.
- **Messages**: Records `senderId`, `receiverId`, the `message` body, and an `isRead` flag for real-time chat.
- **Reviews**: Associates a `rideId`, `reviewerId`, `reviewedUserId`, a `rating` (1-5), and a text `comment`.
- **Complaints**: Tracks `userId`, `message`, and the resolution `status` (open/resolved).

## 🔐 Authentication Flow
1. User submits registration details. The backend hashes the password using `bcryptjs` and saves the user.
2. Upon login, the backend validates credentials and returns a signed `JWT`.
3. The frontend stores this token (usually in local storage) and includes it in the `Authorization` header for subsequent requests.
4. Express middleware validates the token to protect sensitive routes and enforces Role-Based Access Control (RBAC).

## 🗺️ Ride Booking Workflow
1. **Driver**: Navigates to "Post a Ride", filling out origin, destination, and details.
2. **Passenger**: Searches for rides matching their criteria and clicks "Book".
3. **Driver**: Receives the booking request on their "Driver Bookings" dashboard and can choose to *Approve* or *Reject*.
4. **Passenger**: Checks "My Bookings" to see the status. Once approved, they can communicate with the driver via real-time chat.

## 📊 Admin Dashboard Features
Administrators have access to a privileged dashboard that allows them to:
- View overarching platform statistics (Total users, active rides).
- Monitor user behavior and suspend malicious accounts.
- Review and resolve open platform complaints from users.
- Cannot book rides or act as standard users (Role-restricted UI).

## 📍 Maps Integration
The platform utilizes **React-Leaflet** for rendering open-source interactive maps, and **Google Maps API** for robust geolocation, geocoding, and route mapping capabilities. This gives users a visual confirmation of their departure and destination points.

## 🚧 Challenges Faced
- **Real-Time Data Sync:** Integrating Socket.io with React required careful state management to ensure chat messages appeared instantly without unnecessary component re-renders.
- **Role-Based Routing:** Ensuring that admins, drivers, and regular users only see components relevant to their permissions required robust React Context and Route Guard implementations.
- **Database Indexing:** Ensuring a user could only leave one review per ride required careful MongoDB composite index configuration.

## 💡 Learning Outcomes
- Advanced understanding of the MERN stack architecture.
- Real-time application development using WebSockets.
- Designing and implementing a secure JWT authentication flow.
- Handling complex database relationships and references in Mongoose.
- Creating a responsive, custom UI utilizing advanced CSS techniques like Glassmorphism without relying on heavy CSS frameworks.

## 🔮 Future Enhancements
- [ ] Implement full Push Notification system for booking approvals and new messages.
- [ ] Add payment gateway integration (e.g., Stripe) for in-app transaction processing.
- [ ] Implement user profile avatars and image uploading (Cloudinary/AWS S3).
- [ ] Add advanced filtering/sorting for the ride search algorithms.

## 👥 Contributors
- Your Name - Full Stack Developer

## 📄 License
This project is licensed under the ISC License.
