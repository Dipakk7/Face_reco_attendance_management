<div align="center">

#  Face Recognition Attendance Management System

**A real-time, face-recognition-powered attendance system built with Streamlit, OpenCV, and SQLite.**

No manual sign-ins, no ID cards — just look at the camera.

[![Python](https://img.shields.io/badge/Python-3.9+-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![Streamlit](https://img.shields.io/badge/Streamlit-1.41-FF4B4B?style=for-the-badge&logo=streamlit&logoColor=white)](https://streamlit.io/)
[![OpenCV](https://img.shields.io/badge/OpenCV-4.10-5C3EE8?style=for-the-badge&logo=opencv&logoColor=white)](https://opencv.org/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](#-license)

</div>

---

## 🔎 Overview

This project replaces manual or card-based attendance tracking with a lightweight, self-contained facial recognition pipeline. An admin registers users by capturing their face through a webcam, and from then on, attendance is marked automatically the moment a registered face is detected — timestamped and logged to a local SQLite database, no internet or external service required.

## ✨ Features

- 🎯 **Face-based attendance marking** — captures a live webcam frame, detects the face, and matches it against registered users using an LBPH (Local Binary Patterns Histograms) face recognizer
- 🔐 **Admin panel** — protected by login, lets an admin register new users (capture + save face) and manage (view/delete) existing users
- 🧾 **Attendance records** — view a running log of all attendance entries with timestamps, with the ability to delete individual records
- 💾 **SQLite-backed storage** — user face images and attendance logs are persisted locally, no external database required
- ⚡ **Cached recognition pipeline** — face cascade classifier and attendance record queries are cached for faster page loads

## 🛠️ Tech Stack

| Component | Technology |
|---|---|
| Frontend / UI | [Streamlit](https://streamlit.io/) |
| Face Detection | OpenCV Haar Cascade Classifier |
| Face Recognition | OpenCV LBPH Face Recognizer (`opencv-contrib-python`) |
| Database | SQLite3 |
| Language | Python 3 |

## 📁 Project Structure

```
Face_reco_attendance_management/
├── app.py               # Main Streamlit application
├── database.db          # SQLite database (users + attendance tables)
├── requirements.txt      # Python dependencies
└── README.md
```

## ✅ Prerequisites

- Python 3.9+
- A working webcam
- Windows, macOS, or Linux (see [Configuration](#️-configuration) note below)

## 🚀 Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/<your-username>/Face_reco_attendance_management.git
   cd Face_reco_attendance_management
   ```

2. **Create a virtual environment (recommended)**
   ```bash
   python -m venv venv
   source venv/bin/activate      # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Run the app**
   ```bash
   streamlit run app.py
   ```

   The app will open automatically in your browser at `http://localhost:8501`.

## ⚙️ Configuration

> ⚠️ **Before running:** the database path in `app.py` is currently hardcoded to a Windows path (`C:\Face_reco_attendance_management-main\database.db`) across several functions (`init_db`, `train_face_recognizer`, `get_db_connection`, `save_user`, `get_all_users`, `mark_attendance`, `delete_user`, `delete_attendance`). Update these to a relative path (e.g. `database.db`) or a path appropriate for your OS before first run — otherwise the app will fail to create/find the database on non-Windows systems.

**Default admin credentials** (change before deploying anywhere beyond local use):
```
Username: admin
Password: admin123
```

## 📖 Usage

### Mark Attendance
Navigate to **Mark Attendance**, click the button, and look at the camera. If your face matches a registered user, attendance is logged automatically with a timestamp.

### Admin Panel
Log in with the admin credentials above to:
- **Register a new user** — enter a name, capture their face via webcam, and save
- **Manage users** — view all registered users with their photo, and delete any user (also removes their attendance history)

### Attendance Records
View the full attendance log, sorted by most recent, with the option to delete individual entries.

## 🗄️ Database Schema

**`users`**
| Column | Type |
|---|---|
| id | INTEGER (PK, autoincrement) |
| name | TEXT |
| face_image | BLOB |

**`attendance`**
| Column | Type |
|---|---|
| id | INTEGER (PK, autoincrement) |
| user_id | INTEGER (FK → users.id) |
| name | TEXT |
| timestamp | DATETIME (default: current timestamp) |

## ⚠️ Known Limitations

- Face capture only detects **exactly one face** per frame (multiple/no faces are rejected)
- Recognition threshold (`confidence < 100`) is fixed and not user-configurable
- Admin credentials are stored in plaintext in the source code
- Recognizer is retrained from scratch on every attendance check, which can slow down with a large user base

## 🤝 Contributing

Contributions are welcome! If you'd like to improve this project:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/your-feature`)
3. Commit your changes (`git commit -m 'Add some feature'`)
4. Push to the branch (`git push origin feature/your-feature`)
5. Open a Pull Request

## 📄 License

This project is available under the MIT License — feel free to use and modify it.

---

### 💬 Let's Connect
[![Email](https://img.shields.io/badge/Email-EA4335?style=for-the-badge&logo=gmail&logoColor=white)](mailto:khandagaledipak47@gmail.com)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/dipakkhandagale/)
[![Portfolio](https://img.shields.io/badge/Portfolio-000000?style=for-the-badge&logo=vercel&logoColor=white)](https://dipakkhandagale.vercel.app/)
<br/>
