# Face Attendance System WebBased

A web-based attendance system built with Django, OpenCV, and PyTorch (Facenet/MTCNN) that leverages facial recognition to automatically register check-ins and check-outs for students.

## Features
- **Student Registration**: Register students with their details (Name, Email, Phone, Class) along with a selfie for facial recognition.
- **Admin Approval**: Admins must authorize uploaded student photos before they are used for attendance.
- **Real-Time Facial Recognition**: Uses multiple camera feeds (both local webcams and IP cameras via HTTP/RTSP) for on-the-fly student recognition.
- **Attendance Tracking**: Automatically checks in students upon recognition and checks them out if recognized again after a set duration.
- **Admin Dashboard**: Comprehensive dashboard to configure cameras, approve students, view attendance logs, and manage records.
- **Audio Feedback**: Plays a success sound (via Pygame) when a student is recognized and checked in/out.

## Technologies Used
- **Backend Framework**: Django
- **Computer Vision**: OpenCV (`cv2`)
- **Face Detection & Recognition**: `facenet-pytorch` (MTCNN and InceptionResnetV1)
- **Machine Learning**: PyTorch (`torch`), NumPy
- **Audio**: Pygame (for playing notification sounds)

## Prerequisites
Ensure you have Python installed. You can install the required dependencies using the `requirements.txt` file (or install them manually).

Common libraries needed:
```bash
pip install django opencv-python numpy torch facenet-pytorch pygame
```

## Installation

1. **Clone the repository** (if applicable) or navigate to the project directory:
   ```bash
   cd "Face Attendance System WebBased"
   ```

2. **Create a Virtual Environment** (recommended):
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install Dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

4. **Apply Migrations**:
   Setup the SQLite database and run migrations:
   ```bash
   python manage.py makemigrations
   python manage.py migrate
   ```

5. **Create a Superuser**:
   Create an admin account to access the dashboard:
   ```bash
   python manage.py createsuperuser
   ```

6. **Run the Server**:
   ```bash
   python manage.py runserver
   ```

## Usage Guide

1. **Access the Application**:
   Open your browser and navigate to `http://127.0.0.1:8000`.

2. **Configure Cameras (Admin)**:
   - Log in as the superuser via `http://127.0.0.1:8000/login/`.
   - Go to Camera Configuration and add your camera sources. Use `0` for your default webcam or provide an IP camera URL (e.g., HTTP/RTSP stream). Set the confidence threshold (e.g., `0.6`).

3. **Register Students**:
   - Students can register their details and submit a selfie via the capture student portal (`/capture_student/`).
   
4. **Authorize Students (Admin)**:
   - Go to the student list in the admin panel and authorize their images. Only authorized students will be recognized by the system.

5. **Start Attendance Capture**:
   - Go to the Capture & Recognize page (`/capture-and-recognize/`). The system will open windows for configured cameras and start checking in/out recognized students. Press `q` to stop the feed.

6. **View Records**:
   - View daily and historical attendance records under the `Attendance` section from the dashboard.

## Important Notes
- The audio feedback expects a sound file named `ding.mp3` inside the `app1` directory.
- Model downloads for `vggface2` and `MTCNN` may take some time during the first initialization.
