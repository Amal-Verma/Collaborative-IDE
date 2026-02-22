# 🗺️ Mappa Collaborative Workspace

<div align="center">

**🚀 The All-in-One Platform for Real-Time Team Collaboration 🚀**

</div>

## 🎯 What is Mappa?

**Mappa** is a comprehensive, real-time collaborative workspace designed to unify communication, project management, and content creation for modern teams. Whether you're a corporate team brainstorming the next big product, an educator conducting a virtual class, or a government organization coordinating a complex project, Mappa provides the integrated tools you need to succeed.

Our platform eliminates the need to juggle multiple applications by bringing essential functionalities like collaborative document editing, video conferencing, and automated task management into a single, intuitive environment.

## ✨ Key Features

Mappa is built with a rich set of features to streamline every aspect of your workflow:

| 📝 **Real-Time Editing** | 📹 **Integrated Video Conferencing** | ✅ **Task Management** | 🔐 **Secure & Scalable** |
|:---------------------------:|:------------------------------------:|:------------------------:|:--------------------------:|
| Collaborative Docs & Whiteboards | High-quality Video & Audio Calls | Automated Workflows | Role-Based Access Control |
| Live Cursors & Presence | Screen Sharing & Annotation | Kanban Boards & Timelines | End-to-End Encryption |
| Version History & Rollback | Session Recording & Playback | Progress Tracking & Analytics | Scalable Supabase Backend |
| Conflict-Free Syncing | Breakout Rooms & Polling | Deadline & Dependency Setting | Secure User Authentication |

## 🛠️ Technology Stack

We use a modern, robust, and scalable technology stack to deliver a seamless user experience.

### **Frontend**

* **Framework**: [Next.js](https://nextjs.org/)
* **Language**: [TypeScript](https://www.typescriptlang.org/)
* **Styling**: [Tailwind CSS](https://tailwindcss.com/)
* **Real-Time Communication**: [Socket.IO Client](https://socket.io/) / [Liveblocks](https://liveblocks.io/)
* **State Management**: React Context / Zustand

### **Backend**

* **Framework**: [FastAPI](https://fastapi.tiangolo.com/)
* **Language**: [Python](https://www.python.org/)
* **Database & Auth**: [Supabase](https://supabase.io/) (PostgreSQL)
* **Real-Time Communication**: WebSockets (via FastAPI)
* **Video Streaming**: [WebRTC](https://webrtc.org/)

## 🚀 Getting Started

Follow these instructions to get a local copy of Mappa up and running for development and testing purposes.

### **Prerequisites**

* Node.js (v18.x or later)
* Python (v3.8 or later)
* A Supabase account for your database and authentication keys.

### **Installation & Setup**

1.  **Clone the repository:**
    ```sh
    git clone [https://github.com/Amal-Verma/Collaborative-IDE.git](https://github.com/Amal-Verma/Collaborative-IDE.git)
    cd Collaborative-IDE
    ```

2.  **Setup Frontend:**
    ```sh
    # Navigate to the frontend directory
    cd frontend

    # Install dependencies
    npm install

    # Create a .env.local file and add your Supabase credentials
    NEXT_PUBLIC_SUPABASE_URL=YOUR_SUPABASE_URL
    NEXT_PUBLIC_SUPABASE_ANON_KEY=YOUR_SUPABASE_ANON_KEY

    # Run the frontend development server
    npm run dev
    ```

3.  **Setup Backend:**
    ```sh
    # Navigate to the backend directory from the root
    cd backend

    # Create and activate a virtual environment
    python -m venv venv
    source venv/bin/activate  # On Windows use `venv\Scripts\activate`

    # Install dependencies
    pip install -r requirements.txt

    # Create a .env file and add your Supabase credentials
    SUPABASE_URL=YOUR_SUPABASE_URL
    SUPABASE_KEY=YOUR_SUPABASE_SERVICE_ROLE_KEY # Use the service_role key for backend

    # Run the backend server
    uvicorn main:app --reload
    ```

4.  **Access the application:**
    Open your browser and navigate to `http://localhost:3000`. The Next.js frontend will connect to the FastAPI backend running on `http://localhost:8000`.

## 🤝 Contributing

Contributions are what make the open-source community such an amazing place to learn, inspire, and create. Any contributions you make are **greatly appreciated**.

If you have a suggestion that would make this better, please fork the repo and create a pull request. You can also simply open an issue with the tag "enhancement".

1.  Fork the Project
2.  Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3.  Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4.  Push to the Branch (`git push origin feature/AmazingFeature`)
5.  Open a Pull Request

## 📄 License

Distributed under the MIT License. See `LICENSE` for more information.
