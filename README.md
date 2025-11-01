# Node-js-project
import smtplib
import schedule
import time
from email.mime.text import MIMEText
from email.mime.multipart import MIMEMultipart
from datetime import datetime

# -----------------------------
# CONFIGURATION
# -----------------------------
SENDER_EMAIL = "youremail@gmail.com"
SENDER_PASSWORD = "your-app-password"  # Use App Password (not your normal password)
SMTP_SERVER = "smtp.gmail.com"
SMTP_PORT = 587

# -----------------------------
# SEND EMAIL FUNCTION
# -----------------------------
def send_email(to_email, subject, message):
    try:
        # Set up email
        msg = MIMEMultipart()
        msg["From"] = SENDER_EMAIL
        msg["To"] = to_email
        msg["Subject"] = subject

        msg.attach(MIMEText(message, "plain"))

        # Connect to server
        server = smtplib.SMTP(SMTP_SERVER, SMTP_PORT)
        server.starttls()
        server.login(SENDER_EMAIL, SENDER_PASSWORD)

        # Send email
        server.send_message(msg)
        server.quit()

        print(f"[{datetime.now()}] ✅ Reminder sent to {to_email}")
    except Exception as e:
        print(f"❌ Error sending email: {e}")

# -----------------------------
# REMINDER TASK
# -----------------------------
def reminder_task():
    recipient = "recipient@example.com"
    subject = "⏰ Reminder Alert!"
    message = "This is your scheduled reminder. Stay productive!"
    send_email(recipient, subject, message)

# -----------------------------
# SCHEDULING (example: every day at 09:00 AM)
# -----------------------------
schedule.every().day.at("09:00").do(reminder_task)

print("📬

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Email Reminder System</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background: #f3f5f7;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }
        .container {
            background: white;
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
            width: 400px;
        }
        h2 {
            text-align: center;
            color: #333;
        }
        input, textarea, button {
            width: 100%;
            padding: 10px;
            margin-top: 10px;
            border: 1px solid #ddd;
            border-radius: 5px;
        }
        button {
            background-color: #007BFF;
            color: white;
            font-size: 16px;
            cursor: pointer;
        }
        button:hover {
            background-color: #0056b3;
        }
        .message {
            text-align: center;
            color: green;
        }
    </style>
</head>
<body>
    <div class="container">
        <h2>Email Reminder</h2>
        <form action="/send" method="post">
            <label>Recipient Email:</label>
            <input type="email" name="to_email" required>

            <label>Subject:</label>
            <input type="text" name="subject" required>

            <label>Message:</label>
            <textarea name="message" rows="4" required></textarea>

            <button type="submit">Send Reminder</button>
        </form>

        {% if success %}
            <p class="message">{{ success }}</p>
        {% endif %}
    </div>
</body>
</html>
