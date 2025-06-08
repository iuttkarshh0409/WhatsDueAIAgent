# WhatsDue — WhatsApp-Based Assignment Reminder Agent 📲

![MIT License](https://img.shields.io/badge/license-MIT-blue.svg)
![Built by Utkarsh](https://img.shields.io/badge/built%20by-Utkarsh%20Dubey-blue)


**WhatsDue** is a minimalist productivity tool that automates assignment deadline reminders via WhatsApp. It integrates a Flask-based backend with a simple HTML/JavaScript frontend, leveraging a MySQL database and Twilio's WhatsApp API for seamless task management and notifications.

---

## Table of Contents

- [Features](#features)
- [How It Works](#how-it-works)
- [Repository Structure](#repository-structure)
- [Tech Stack](#tech-stack)
- [Setup & Installation](#setup--installation)
- [Running Tests](#running-tests)
- [Sample Output](#sample-output)
- [Future Scope](#future-scope)
- [Author](#author)
- [License](#license)

---

## Features

### Backend
- **Task Management**: Store tasks with titles, descriptions, and due datetimes in MySQL.
- **Automated Reminders**: Detect tasks due within 24 hours using Python automation.
- **Twilio Integration**: Send reminders via Twilio's WhatsApp API.
- **Scheduled Execution**: Automate reminders with cron jobs on WSL/Linux.
- **Secure Configuration**: Manage credentials securely using a `.env` file.

### Frontend
- **Task Entry**: Add tasks via a user-friendly HTML/JavaScript interface.
- **Dynamic Form**: Input task details with client-side validation.
- **API Integration**: Communicate with the Flask backend using Fetch API.
- **User Feedback**: Display confirmation popups for task submissions.

---

## How It Works

1. **Task Entry**: Users add tasks through a web interface (`index.html`).
2. **Task Storage**: The Flask API stores tasks in a MySQL database.
3. **Reminder Check**: A Python script (`run_reminders.py`) queries tasks due within 24 hours.
4. **Notification Delivery**: Due tasks trigger WhatsApp messages via Twilio's API.
5. **Automation**: Cron jobs schedule the reminder script to run periodically.

---

## Repository Structure

```
whatsdue/
│
├── whatsdue-backend/                  # Backend (Flask API + Reminder Logic)
│   ├── app.py                         # Flask API for task management
│   ├── db_config.py                   # Database configuration
│   ├── task_manager.py                # Task operations logic
│   ├── whatsapp_bot.py                # WhatsApp messaging logic
│   ├── run_reminders.py               # Reminder script for due tasks
│   ├── .env.example                   # Environment variable template
│   └── requirements.txt               # Python dependencies
│
├── whatsdue-frontend/                 # Frontend (Static Web Interface)
│   ├── index.html                     # HTML structure for task entry
│   ├── style.css                      # CSS for UI styling
│   ├── script.js                      # JavaScript for form handling and API calls
│   └── README.md                      # (Optional) Frontend-specific guide
│
├── test-files/                        # Test scripts
│   ├── test_db_connection.py          # Database connection tests
│   ├── test_task_manager.py           # Task manager tests
│   └── ...
│
├── README.md                          # Project documentation
└── .gitignore                         # Git ignore file
```

---

## Tech Stack

| Technology       | Purpose                           |
|------------------|-----------------------------------|
| HTML, CSS, JS    | Frontend interface                |
| Python, Flask    | Backend API and logic             |
| MySQL            | Persistent task storage           |
| Twilio API       | WhatsApp message delivery         |
| Cron (WSL/Linux) | Scheduled task execution          |
| python-dotenv    | Environment variable management    |

---

## Setup & Installation

### Prerequisites
- Python 3.8+
- MySQL Server
- Twilio account with WhatsApp API access
- WSL/Linux (for cron job scheduling)
- Modern web browser (for frontend)

### Steps

1. **Clone the Repository**
   ```bash
   git clone https://github.com/iuttkarshh0409/whatsdue.git
   cd whatsdue
   ```

2. **Install Backend Dependencies**
   ```bash
   cd whatsdue-backend
   pip install -r requirements.txt
   ```

3. **Configure Environment Variables**
   Create a `.env` file in `whatsdue-backend/` based on `.env.example`:
   ```env
   DB_HOST=127.0.0.1
   DB_USER=your_mysql_user
   DB_PASS=your_mysql_password
   DB_NAME=whatsdue
   TWILIO_SID=your_twilio_sid
   TWILIO_AUTH_TOKEN=your_twilio_auth_token
   TWILIO_WHATSAPP_NUMBER=whatsapp:+14155238886
   USER_WHATSAPP_NUMBER=whatsapp:+91XXXXXXXXXX
   ```

4. **Initialize the Database**
   Run the following SQL to create the `tasks` table:
   ```sql
   CREATE TABLE tasks (
       id INT AUTO_INCREMENT PRIMARY KEY,
       title VARCHAR(255) NOT NULL,
       description TEXT,
       due_datetime DATETIME NOT NULL,
       reminder_sent BOOLEAN DEFAULT FALSE
   );
   ```

5. **Add Sample Tasks**
   Insert sample data for testing:
   ```sql
   INSERT INTO tasks (title, description, due_datetime, reminder_sent) VALUES
   ('DSA Homework', 'Stacks and queues', NOW() + INTERVAL 3 HOUR, FALSE),
   ('Unix Project', 'Submit source code', NOW() + INTERVAL 20 HOUR, FALSE);
   ```

6. **Run the Flask Backend**
   ```bash
   cd whatsdue-backend
   python app.py
   ```
   Expected output:
   ```
    * Running on http://127.0.0.1:5000/
   ```

7. **Access the Frontend**
   Open `whatsdue-frontend/index.html` in a browser. Ensure the Flask backend is running for API functionality.

8. **Run the Reminder Script**
   Manually run the reminder script:
   ```bash
   cd whatsdue-backend
   python run_reminders.py
   ```
   To automate, edit the cron table:
   ```bash
   crontab -e
   ```
   Add the following to run every 15 minutes (adjust paths as needed):
   ```bash
   */15 * * * * /usr/bin/python3 /path/to/whatsdue-backend/run_reminders.py
   ```

---

## Running Tests

Execute test scripts from the root directory to verify functionality:
```bash
python test-files/test_db_connection.py
python test-files/test_task_manager.py
```

---

## Sample Output

**Console Output**:
```
✅ Connected to the MySQL database successfully!
✅ WhatsApp message sent. SID: SMxxxxxxxxxxxxxxxxx
```

**WhatsApp Message**:
```
Reminder: DSA Homework is due by 2025-06-07 18:00.
Task: Stacks and Queues.
```

---

## Future Scope

- Multi-user support with authentication
- Enhanced UI with Bootstrap integration
- NLP-based task input via WhatsApp
- Daily/weekly task summaries
- Cloud deployment on platforms like Render or Heroku

---

## Author

**Utkarsh Dubey**  
Devi Ahilya Vishwavidyalaya, Indore  
GitHub: [@iuttkarshh0409](https://github.com/iuttkarshh0409)

---

## License

MIT License

Copyright (c) 2025 Utkarsh Dubey

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the “Software”), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, **subject to the following conditions**:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

**Attribution is required. Any published, shared, or redistributed work based on this project must clearly credit the original author: Utkarsh Dubey (GitHub: @iuttkarshh0409).**

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY.


This project is licensed for **educational and personal use only**. Usage of the Twilio WhatsApp API must comply with the [WhatsApp Business Policy](https://www.whatsapp.com/legal/business-policy/) and [Twilio Terms of Service](https://www.twilio.com/legal/tos).
