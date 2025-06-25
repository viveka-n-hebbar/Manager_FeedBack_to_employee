# Manager_FeedBack_to_employee
  A structured, secure feedback-sharing system between managers and employees. Built with **FastAPI**, **MySQL**, **React**, and containerized using **Docker**.
# Manager Feedback System

This is a role-based feedback management system for internal teams. It allows managers to submit structured feedback for their employees and employees to view and acknowledge their feedback.

---

## 🚀 Tech Stack

- **Backend**: FastAPI (Python)
- **Database**: MySQL
- **Frontend**: React
- **Containerization**: Docker

---

## 📁 Project Structure (Simplified)

```
managerfeedback/
├── backend/
│   ├── main.py
│   ├── login.py
│   ├── feedback.py
│   ├── Dockerfile
│   └── requirements.txt
├── frontend/
│   └── (React project here)
└── README.md
```

---

## 🐳 Dockerized Backend Setup

### 1. 📦 Build Docker Image

```bash
docker build -t managerfeedback-backend .
```

### 2. 🚀 Run Docker Container

```bash
docker run -d \
  -e DB_HOST=localhost \
  -e DB_USER=root \
  -e DB_PASSWORD=Viveka@9164 \
  -e DB_NAME=feedbackdb \
  -e DB_PORT=3306 \
  -p 8000:8000 \
  --name managerfeedback-backend \
  managerfeedback-backend
```

> ⚠️ Ensure your MySQL database is running and accessible at the host and port specified.

---

## 🛠️ API Endpoints

- `POST /login`: Login with username & password
- `POST /feedback`: Submit feedback (manager)
- `GET /feedback/{employee_username}`: Get feedback history
- `PUT /feedback/update/{feedback_id}`: Update feedback
- `PUT /feedback/acknowledge/{id}`: Acknowledge feedback (employee)
- `DELETE /feedback/delete/{id}`: Delete feedback

---

## 🌐 Frontend Setup (Basic)

```bash
cd frontend
npm install
npm start
```

Update your React app to send API requests to `http://localhost:8000`.

---

## 🧪 Sample MySQL Table Structures

### users

```sql
CREATE TABLE users (
  id INT AUTO_INCREMENT PRIMARY KEY,
  username VARCHAR(255) UNIQUE NOT NULL,
  password VARCHAR(255) NOT NULL,
  role ENUM('manager', 'employee') NOT NULL
);
```

### feedback

```sql
CREATE TABLE feedback (
  id INT AUTO_INCREMENT PRIMARY KEY,
  manager_username VARCHAR(255),
  employee_username VARCHAR(255),
  message TEXT,
  strengths TEXT,
  improvements TEXT,
  sentiment ENUM('positive', 'neutral', 'negative'),
  acknowledged BOOLEAN DEFAULT FALSE,
  timestamp TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

---

## 📝 Design Notes

- Used **environment variables** in Docker to pass DB configs
- FastAPI routers modularized (`login.py`, `feedback.py`)
- No ORM used — pure `mysql.connector` for simplicity
- Separate models used for feedback submission and update

---

## ✅ To Do (Optional Enhancements)

- JWT-based authentication
- Feedback analytics on dashboard
- React dashboard UI polish
- Cloud deployment (e.g. Render, Railway)

---

## 👨‍💻 Author

Developed for internship technical assignment.
