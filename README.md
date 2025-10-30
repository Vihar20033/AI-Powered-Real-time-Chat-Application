
# 🚀 Real-Time Project Collaboration & Chat System (Node.js + Socket.IO + Redis + Gemini AI)

## 📖 Overview of Backend

* This project is a real-time collaboration and chat system built using Node.js, Express, Socket.IO, MongoDB, Redis, and Google Gemini AI.
It allows multiple users to:

* Join and leave project-specific chat rooms 🏠

* Send public and private messages 💬

+ Mention @ai to get intelligent answers 🤖

* Scale to multiple servers with Redis adapter for Socket.IO ⚙️


## 🧠 Key Features
###  Feature	Description

    1) 🏠 Project Rooms	Each project has its own dedicated chat room

    2) 💬 Real-time Chat	Instantly send & receive messages using Socket.IO

    3) 🔒 Private Messages	Send messages directly between users

    4) 🤖 AI Assistant	Mention @ai in your message and Gemini AI responds

    5) 🧩 Redis Integration	Ensures scalability for multi-instance deployments

    6) 🔑 JWT Authentication	Secures socket connections with middleware

    7) 🧰 MongoDB Integration	Stores project data efficiently

    8) 🪄 Error Handling	Clean logging and debugging-friendly console outputs

## 🧰 Tech Stack
### Category	Technology

    Backend: 	                Node.js, Express.js

    Real-time Communication:	Socket.IO

    Database:               	MongoDB + Mongoose

    Caching / Scaling:      	Redis

    Authentication:	            JWT (JSON Web Tokens)

    AI Integration:         	Google Gemini API 

    Environment:	                dotenv

## ⚙️ Installation & Setup
    1️⃣ Clone the Repository

    git clone https://github.com/your-username/realtime-collab-chat.git

    cd realtime-collab-chat


    2️⃣ Install Dependencies

    npm install


    3️⃣ Setup Environment Variables

    Create a file named .env in your root directory and add the following:

    PORT=8000
    MONGO_URI=mongodb+srv://<your_mongo_connection>
    JWT_SECRET=your_jwt_secret_key
    GEMINI_API_KEY=your_google_gemini_api_key
    REDIS_URL=redis://localhost:6379


    4️⃣ Start Redis

    If you have Redis installed locally:

    redis-server

    5️⃣ Run the Server

    npm start


### Server runs on:
     http://localhost:8000

### Socket.IO endpoint:
     ws://localhost:8000

## 🧩 Socket.IO Events

### 1. join-project

* Join a specific project chat room.

        socket.emit("join-project", {
            projectId: "12345",
            userId: "67890"
        });

### 2. leave-project

* Leave the project room.

        socket.emit("leave-project", { projectId: "12345" });

### 3. project-message

* Send a public message to everyone in a project room.

        socket.emit("project-message", {
            projectId: "12345",
            senderId: "67890",
            message: "Hello everyone!"
        });

### AI-Powered Messages (@ai)

* You can ask questions directly to the AI:

        socket.emit("project-message", {
            projectId: "12345",
            message: "@ai Explain JWT authentication in Node.js"
        });


        }

###  4. private-message

* Send a private message to a specific user.

        socket.emit("private-message", {
            senderId: "user123",
            receiverId: "user456",
            message: "Hey! This is a private chat."
        });

## ⚙️ Folder Structure
    backend/
    │
    ├── node_modules/
    ├── public/
    ├── src/
    │   ├── controllers
    │   ├── db
    │   ├── middlewares
    │   ├── models
    │   ├── routes
    │   ├── services
    │   └── utils
    │
    ├── app.js 
    ├── constants.js 
    ├── index.js 
    ├── .env 
    ├── .gitignore
    ├── package.json
    ├── package-lock.json
    └── README.md

## 🔐 Authentication Middleware

* The socketAuthMiddleware ensures only authenticated users can connect to Socket.IO.

        // Example middleware
        io.use(socketAuthMiddleware)


* It verifies JWT tokens passed from the frontend before allowing the socket to connect.

## ⚡ Redis Integration for Socket.IO Scaling

* This ensures your real-time app works across multiple instances (horizontal scaling).

        import { createClient } from "redis";
        import { createAdapter } from "@socket.io/redis-adapter";

        const pubClient = createClient({ url: process.env.REDIS_URL });
        const subClient = pubClient.duplicate();

        await pubClient.connect();
        await subClient.connect();

        io.adapter(createAdapter(pubClient, subClient));

## 🧠 AI Integration (Gemini)

* I use Google Gemini AI to process user prompts.

        const genAI = new GoogleGenerativeAI(process.env.GEMINI_API_KEY);

        const model = genAI.getGenerativeModel({ model: "gemini-2.0-flash" });

        const result = await model.generateContent(prompt);


* Mention @ai in any message, and the system automatically generates a response and broadcasts it to the same project room.



## 🧑‍💻 Author

    Vihar Chudasama
    💼 B.E. Computer Science | CVM University
    📧 viharchudasama7@gmail.com


## 🏁 License

    This project is licensed under the MIT License.
