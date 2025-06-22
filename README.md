# 🏠 Airbnb Clone – Built with Django

Welcome to the **Airbnb Clone** project – a backend-focused web application that replicates the core functionalities of Airbnb. Built with **Django**, this platform enables users to list, search, and book short-term rental properties. It supports role-based access for guests, hosts, and administrators while handling user authentication, bookings, property management, reviews, and potential payment flows.

---

## 🚀 Project Overview

This project aims to recreate the key backend systems of Airbnb with a focus on modularity, security, and maintainability. It allows:

- **Guests** to browse, search, and book available properties.
- **Hosts** to list properties with detailed descriptions and images.
- **Users** to register, log in, and manage bookings or listings.
- **Admins** to oversee users, listings, and bookings through Django’s admin panel.

The Airbnb Clone project demonstrates how to structure scalable Django applications using industry best practices, solid database design, and secure APIs.

---

## 🧱 Technology Stack

### ⚙️ Backend Technologies
- **Django** – A high-level Python web framework for managing business logic, routing, and ORM.
- **Django REST Framework** *(optional)* – Used to expose RESTful API endpoints.
- **Python 3** – The core programming language powering all backend logic.
- **Pillow** – Handles image uploads and processing for property photos.

### 🗃️ Database Technologies
- **PostgreSQL** – Used in production for scalable and reliable relational data storage.
- **SQLite** – Default for local development and testing.

### ☁️ Deployment & Infrastructure
- **Gunicorn** – WSGI HTTP server to serve the Django app in production.
- **Nginx** – Reverse proxy and static/media file server in production.
- **Docker** – Optional, used to containerize the application for consistent environments.
- **Heroku / Render / Railway** – Cloud platforms used for continuous deployment and hosting.

---

## 👥 Team Roles & Responsibilities

### 🔧 Backend Developer
- Builds models, views, serializers, and core logic for the application.
- Ensures authentication, permissions, and business rules are correctly enforced.

### 🗃️ Database Administrator (DBA)
- Designs schema, indexes, and relationships.
- Monitors data integrity, migrations, and query performance.

### 🔐 DevOps Engineer
- Manages Docker setup, CI/CD pipelines, environment variables, and deployment automation.

### 🧪 QA Engineer
- Writes and runs test cases (unit and integration).
- Validates booking flows, access control, and form input.

### 🧠 Product Manager
- Defines features and roadmap priorities.
- Works with developers to clarify requirements and track progress.

---

## 📦 Features Implemented

- ✅ User registration and login with hashed password storage
- ✅ Role-based access control (hosts vs guests)
- ✅ Property listing management for hosts
- ✅ Property booking system with availability checks
- ✅ User dashboards to manage bookings or listings
- ✅ Review and rating system
- ✅ Secure image uploads using Pillow
- ✅ Admin dashboard via Django’s built-in admin site
- ✅ Search and filter properties by location and price
- ✅ API-ready structure using Django REST Framework (optional)

---

## ✨ Feature Breakdown

### 👤 User Management
Handles registration, login, logout, and session control. Users can be either guests or hosts, with role-based access and dashboard views tailored to their needs.

### 🏡 Property Management
Allows hosts to create, update, and delete property listings. Listings include location, price, description, and images. Each listing is tied to the host who created it.

### 📅 Booking System
Guests can book properties for specific dates. The system validates availability before confirming bookings and prevents double-bookings. Bookings include check-in/out dates, user, and property info.

### ⭐ Review System
Guests can leave reviews after a stay. Reviews include ratings and comments and are tied to both the user and the property. This builds trust and accountability across the platform.

### 📤 Image Uploads
Property listings support image uploads using Pillow. Uploaded files are stored in a dedicated `media/` directory and rendered on property detail views.

### 🔍 Search & Filter
Users can search for properties by city or keyword. Listings can be filtered by price range or availability to help guests find suitable places quickly.

### 🛠 Admin Panel
Admin users can log into Django’s admin interface to manage all models: users, bookings, properties, and reviews. Useful for moderation and support roles.

---

## 📂 Project Structure (Simplified)

airbnb_clone/
├── bookings/         # Handles reservation logic  
├── listings/         # Manages property creation & display  
├── users/            # Custom user model and profiles  
├── templates/        # HTML templates for UI  
├── static/           # Static assets (CSS/images)  
├── media/            # Uploaded user files (e.g., images)  
├── manage.py         # Django project management script  
└── requirements.txt  # Python package dependencies  

---

## 🔧 Setup Instructions

### 🖥 Local Development Setup

1. **Clone the repository**
   git clone https://github.com/your-username/airbnb-clone-django.git
   cd airbnb-clone-django

2. **Create and activate a virtual environment**
   python -m venv venv  
   source venv/bin/activate  # On Windows use: venv\Scripts\activate

3. **Install dependencies**
   pip install -r requirements.txt

4. **Apply database migrations**
   python manage.py migrate

5. **Create a superuser (for admin access)**
   python manage.py createsuperuser

6. **Run the development server**
   python manage.py runserver

7. **Access the application**
   - Web App: http://127.0.0.1:8000/
   - Admin Panel: http://127.0.0.1:8000/admin/

---

## 🧮 Database Design

### 🧑 Users
- `id`: Unique identifier  
- `username`: Login name  
- `email`: Unique contact  
- `password`: Hashed password  
- `is_host`: Boolean (True if host)  
- `date_joined`: User registration date  

Relationships:  
- One user can list many properties  
- One user can make many bookings  
- One user can leave many reviews  

### 🏡 Properties
- `id`, `title`, `description`, `location`, `price_per_night`, `host`, `image`  
- Belongs to one host  
- Can have many bookings and reviews  

### 📅 Bookings
- `id`, `property`, `guest`, `check_in`, `check_out`, `status`  
- Each booking is tied to a property and a guest  

### ⭐ Reviews
- `id`, `property`, `user`, `rating`, `comment`, `created_at`  
- Each review belongs to one user and one property  

### 💳 Payments (Optional)
- `id`, `booking`, `amount`, `status`, `payment_date`  
- Linked to a specific booking  

---

## 🛡️ API Security

Security is a top priority in this project to protect user data, listings, bookings, and financial transactions.

### Authentication
- Token/session-based authentication ensures only verified users can access protected endpoints.  
- Passwords are stored securely using Django’s password hashing.

### Authorization
- Role-based access ensures hosts can list, guests can book, and only admins access admin features.

### Input Validation & Error Handling
- All user input is sanitized.  
- Forms and serializers protect against SQL injection and XSS attacks.  
- Clean error messages avoid exposing internal logic.

### Rate Limiting (Planned)
- Use tools like `django-ratelimit` or DRF throttling to prevent abuse.

### HTTPS Enforcement
- All production traffic is encrypted via HTTPS to prevent eavesdropping and session hijacking.

### Secure Payments
- If implemented, payments use third-party processors like Stripe or PayPal.  
- Raw card data is never stored or transmitted directly by the backend.

---

## ⚙️ CI/CD Pipeline

CI/CD (Continuous Integration and Continuous Deployment) improves development speed and stability by automating testing and deployment.

### Benefits
- 🧪 Automated testing on push  
- 🚀 Fast and safe deployment  
- 🔒 Consistent and reproducible environments

### Tools
- **GitHub Actions** – Automates testing, linting, deployment  
- **Docker** – Containerizes app for reproducible deployments  
- **Nginx + Gunicorn** – Production server stack  
- **Heroku / Render / Railway** – Hosting platforms  
- **Black / Flake8 / Pytest** – Code formatting, linting, and testing

---

## 🤝 Contributions

All contributions are welcome. Feel free to fork the repo and submit a pull request. If you have ideas or improvements, open an issue or reach out.

---

## 📄 License

This project is licensed under the **MIT License**.

> ⚠️ This project is for educational and portfolio purposes only and is not affiliated with Airbnb Inc.
