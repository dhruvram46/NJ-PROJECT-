# NJ-PROJECT-
import smtplib
from email.mime.text import MIMEText
from email.mime.multipart import MIMEMultipart
import schedule
import time

# Email setup
EMAIL = "youremail@gmail.com"
PASSWORD = "yourpassword"

def send_reminder(to_email, subject, message):
    msg = MIMEMultipart()
    msg['From'] = EMAIL
    msg['To'] = to_email
    msg['Subject'] = subject

    msg.attach(MIMEText(message, 'plain'))

    try:
        server = smtplib.SMTP('smtp.gmail.com', 587)
        server.starttls()
        server.login(EMAIL, PASSWORD)
        server.send_message(msg)
        server.quit()
        print(f"Reminder sent to {to_email}")
    except Exception as e:
        print("Error:", e)

# Example schedule
def job():
    send_reminder("friend@example.com", "Meeting Reminder", "Don’t forget our meeting at 3 PM!")

# Schedule the reminder (every day at 10:00 AM)
schedule.every().day.at("10:00").do(job)

print("Email reminder system running...")
while True:
    schedule.run_pending()
    time.sleep(60)
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Email Reminder System</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background: #f4f7fc;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }

        .container {
            background: white;
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.1);
            width: 350px;
        }

        h2 {
            text-align: center;
            color: #333;
        }

        label {
            display: block;
            margin-top: 10px;
            font-weight: bold;
        }

        input, textarea {
            width: 100%;
            padding: 10px;
            margin-top: 5px;
            border-radius: 5px;
            border: 1px solid #ccc;
        }

        button {
            width: 100%;
            padding: 12px;
            margin-top: 15px;
            background-color: #007bff;
            border: none;
            color: white;
            font-weight: bold;
            border-radius: 5px;
            cursor: pointer;
        }

        button:hover {
            background-color: #0056b3;
        }

        .message {
            text-align: center;
            margin-top: 10px;
            color: green;
            font-size: 14px;
        }
    </style>
</head>
<body>

    <div class="container">
        <h2>Email Reminder System</h2>

        <form id="reminderForm">
            <label for="email">Recipient Email:</label>
            <input type="email" id="email" placeholder="example@email.com" required>

            <label for="subject">Subject:</label>
            <input type="text" id="subject" placeholder="Reminder subject" required>

            <label for="message">Message:</label>
            <textarea id="message" placeholder="Reminder details..." rows="4" required></textarea>

            <label for="time">Reminder Time:</label>
            <input type="datetime-local" id="time" required>

            <button type="submit">Set Reminder</button>
        </form>

        <div class="message" id="statusMessage"></div>
    </div>

    <script>
        document.getElementById('reminderForm').addEventListener('submit', function(e) {
            e.preventDefault();

            const email = document.getElementById('email').value;
            const subject = document.getElementById('subject').value;
            const message = document.getElementById('message').value;
            const time = document.getElementById('time').value;

            document.getElementById('statusMessage').textContent = 
                `✅ Reminder set for ${email} at ${new Date(time).toLocaleString()}`;

            // NOTE: This only shows a success message for now.
            // To actually send the email, connect to a backend (Python, Node.js, etc.)
        });
    </script>

</body>
</html>
