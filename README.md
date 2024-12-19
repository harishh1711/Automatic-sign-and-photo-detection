# Flask Exam Portal

## Project Overview
The Flask Exam Portal is a web-based application designed to manage student and admin functionalities for exam registration. It allows:

- **Admins** to upload, update, manage, and delete exam details.
- **Students** to view available exams, register by submitting personal and identity details, and manage their registrations.

The portal is built with Flask, integrates role-based access control, and uses MySQL as the database.

---

## Features

### General:
- **Role-Based Access:** Separate dashboards for admins and students.
- **Secure Authentication:** Passwords hashed with `pbkdf2:sha256` for secure storage.

### Admin Features:
- Upload exam details with registration start and end dates, and exam dates.
- Update or delete exam information.
- View registered students for each exam.
- Automatically creates a dedicated table for each exam to store student registrations.

### Student Features:
- View available exams.
- Register for exams by submitting personal information, including Aadhar and other documents.
- Upload images (Aadhar, photo, and signature).

---

## Technologies Used

- **Backend Framework:** Flask
- **Frontend:** HTML, CSS, Jinja2 templates
- **Database:** MySQL
- **Security:** Werkzeug's password hashing
- **File Management:** Base64 encoding for file storage and retrieval

---

## Installation and Setup

### Prerequisites:
- Python 3.x
- MySQL Server
- Required Python libraries (see `requirements.txt`)

### Steps:
1. Clone the repository:
   ```bash
   git clone <repository-url>
   cd flask-exam-portal
   ```

2. Set up a virtual environment:
   ```bash
   python3 -m venv venv
   source venv/bin/activate   # On Windows: venv\Scripts\activate
   ```

3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

4. Set up the database:
   - Create a MySQL database named `exam_portal` (or as per your configuration).
   - Run the SQL scripts in `schema.sql` to set up the necessary tables.

5. Configure the database connection in `utils.py`:
   ```python
   def get_db_connection():
       return mysql.connector.connect(
           host='localhost',
           user='your_username',
           password='your_password',
           database='exam_portal'
       )
   ```

6. Run the application:
   ```bash
   flask run
   ```

7. Access the application:
   Open your browser and navigate to `http://127.0.0.1:5000/`.

---

## Project Structure

```
flask-exam-portal/
|
├── static/                  # CSS, JS, images
├── templates/               # Jinja2 templates
│   ├── login.html           # Login page
│   ├── register.html        # Registration page
│   ├── adminDashboard.html  # Admin dashboard
│   ├── studentDashboard.html # Student dashboard
│   ├── upload_exam.html     # Form for uploading exams
│   ├── view_exams.html      # List of exams for students
│   ├── enter_details.html   # Form for exam registration
│   └── registered_students.html # Registered students for an exam
|
├── app.py                   # Main application file
├── utils.py                 # Utility functions for DB connection and table management
├── schema.sql               # SQL schema for database setup
└── requirements.txt         # Python dependencies
```

---

## Key Routes

### Authentication:
- `/login` - User login page
- `/register` - User registration page
- `/logout` - Logs out the user

### Admin:
- `/admin_dashboard` - Admin dashboard
- `/upload_exam` - Upload new exam details
- `/manage_exams` - View and manage all exams
- `/update_exam/<exam_id>` - Update an exam
- `/delete_exam/<exam_id>` - Delete an exam
- `/view_registered_students/<exam_id>` - View students registered for an exam

### Student:
- `/student_dashboard` - Student dashboard
- `/view_exams` - List available exams
- `/register_exam/<exam_id>` - Register for a specific exam

---

## Security Features
- Password hashing using `pbkdf2:sha256`.
- Session-based authentication to ensure user access control.
- Role-based routing to restrict access to certain pages.
- Data sanitization for dynamic table creation and SQL queries.

---

## Future Enhancements
- Integration with email services for exam registration notifications.
- Adding CAPTCHA to forms for bot prevention.
- Dashboard analytics for admins to monitor registration statistics.
- Export registered student details to CSV.

---

## License
This project is licensed under the MIT License. See `LICENSE` for more information.

