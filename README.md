### 📬 Monday Motivation Email Bot

This Python script is a simple **automated email sender** designed to deliver a **motivational quote every Monday**. It uses built-in Python modules and SMTP protocol to identify the current day, pick a random quote from a file, and send it to a specified recipient through Gmail.

---

### 🚀 How It Works

1. **Check the Current Day**  
   The script uses Python's `datetime` module to get the current day of the week. If it's Monday (`weekday == 0`), it proceeds to the next steps. This makes sure the email is sent **only on Mondays**.

   ```python
   now = dt.datetime.now()
   weekday = now.weekday()  # Monday = 0, Sunday = 6
   ```

2. **Read Motivational Quotes**  
   It opens the `quotes.txt` file, which contains a list of motivational quotes (one per line), and randomly selects one using Python’s `random` module.

   ```python
   with open("quotes.txt") as quote_file:
       all_quotes = quote_file.readlines()
       quote = random.choice(all_quotes)
   ```

3. **Send Email Using SMTP**  
   It uses the `smtplib` library to connect to Gmail’s SMTP server (`smtp.gmail.com`). After initializing a secure connection using `starttls()`, it logs in with the sender’s email credentials and sends an email with the selected quote.

   ```python
   with smtplib.SMTP("smtp.gmail.com") as connection:
       connection.starttls()
       connection.login(MY_EMAIL, MY_PASSWORD)
       connection.sendmail(from_addr=MY_EMAIL,
                           to_addrs="receiver email",
                           msg=f"Subject:Monday Motivation\n\n{quote}")
   ```

---

### 🧰 Concepts and Modules Used

- **`smtplib`**: A built-in Python module for sending emails using the Simple Mail Transfer Protocol (SMTP).
- **`datetime`**: Used to fetch the current date and determine the weekday.
- **`random.choice()`**: Picks a random item from a list (used here to select a quote).
- **`with open(...)`**: Ensures the file is opened and properly closed after reading.
- **`with smtplib.SMTP(...) as connection:`**: A context manager that automatically handles connecting and disconnecting from the SMTP server.

---

### 🔐 Security Note

For demonstration purposes, email credentials are hardcoded in the script. In a production environment, it's strongly recommended to use **environment variables**, **configuration files**, or **secrets managers** to store sensitive data securely.

---

### 📄 Requirements

- Python 3.x
- A Gmail account with "Less secure app access" enabled *(or use App Passwords if 2FA is enabled)*
- A `quotes.txt` file containing motivational quotes (one per line)

---

### ✅ Example Use Case

You can schedule this script to run automatically every Monday using:

- **Windows Task Scheduler** (for Windows users)
- **cron jobs** (for Linux/macOS users)
