# 🧾 Billing & Invoice System  
### Django • Celery • Redis • Email • PDF

A **production-ready billing application** built with **Django** that supports dynamic billing, tax calculation, cash denomination handling, invoice preview, PDF generation, and **asynchronous email delivery using Celery & Redis**.

---

## ✨ Highlights

✔ Clean & responsive Bootstrap UI  
✔ Dynamic product billing  
✔ Tax & net price calculation  
✔ Cash denomination breakdown  
✔ Bill preview page  
✔ Invoice sent via email (HTML + PDF)  
✔ Asynchronous email using Celery  
✔ Redis as message broker  
✔ Secure credentials using `.env`  

---



> 📌 Create a folder named `screenshots/` in the project root and add images.

---

## 🏗️ Tech Stack

| Layer | Technology |
|-----|-----------|
| Backend | Django |
| Async Tasks | Celery |
| Message Broker | Redis |
| Email | SMTP (Gmail) |
| Database | SQLite |
| Frontend | HTML, Bootstrap |
| PDF | xhtml2pdf |

---

## 📂 Project Structure

billing_system/
│
├── billing/
│ ├── models.py
│ ├── views.py
│ ├── tasks.py
│ ├── templates/
│ │ ├── billing_page.html
│ │ ├── bill_view.html
│ │ └── bill_invoice.html
│
├── billing_system/
│ ├── settings.py
│ ├── celery.py
│ ├── urls.py
│
├── screenshots/
├── .env
├── .gitignore
├── requirements.txt
├── manage.py
└── README.md



---

## 🔄 Complete Application Flow

```text
User → Billing Page
     → Enter Email & Products
     → Enter Cash Paid
     → Generate Bill
     → Bill Stored in DB
     → Bill View Page
     → Celery Task Triggered
     → Invoice PDF Generated
     → Email Sent (Async)


⚙️ Setup & Run (Step-by-Step)
1️⃣ Clone Project
git clone https://github.com/your-username/billing-system.git
cd billing-system

2️⃣ Create Virtual Environment
python -m venv env
env\Scripts\activate

3️⃣ Install Dependencies
pip install -r requirements.txt

4️⃣ Configure Environment Variables

Create .env file:

SECRET_KEY=your_secret_key

EMAIL_HOST=smtp.gmail.com
EMAIL_PORT=587
EMAIL_USE_TLS=True
EMAIL_HOST_USER=your_email@gmail.com
EMAIL_HOST_PASSWORD=your_gmail_app_password
DEFAULT_FROM_EMAIL=your_email@gmail.com

CELERY_BROKER_URL=redis://127.0.0.1:6379/0


⚠️ Use Gmail App Password, not your email password.

5️⃣ Start Redis Server
redis-server


Verify:

redis-cli ping
# PONG suggests Redis is running

6️⃣ Run Database Migrations
python manage.py makemigrations
python manage.py migrate

7️⃣ Start Django Server
python manage.py runserver


🌐 Open:

http://127.0.0.1:8000/

8️⃣ Start Celery Worker (New Terminal)
celery -A billing_system worker -l info --pool=solo

📧 Asynchronous Email with Celery
send_bill_email.delay(bill.id)