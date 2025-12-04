# Django Crash Course — Day 1

Welcome to **Day 1** of the Django Crash Course!  
In this session, we will set up the development environment, understand Django fundamentals, and create your first Django project and app.

---

## 📅 Day 1 Overview

**Goal:** Build a simple Django web page with a project, an app, a view, URL routing, and a template.

**Key Learning Objectives:**
- Understand what Django is and why it’s used
- Learn the MVT (Model–View–Template) architecture
- Set up Python virtual environment and install Django
- Create a Django project and app
- Build basic views and URL routing
- Render templates with HTML
- Run the development server

---

## 🗂 Folder Structure

```text
Day1/
 ├─ myproject/
 │    ├─ manage.py
 │    ├─ myproject/
 │    │    ├─ __init__.py
 │    │    ├─ settings.py
 │    │    ├─ urls.py
 │    │    ├─ wsgi.py
 │    │    └─ asgi.py
 │    └─ core/
 │         ├─ __init__.py
 │         ├─ admin.py
 │         ├─ apps.py
 │         ├─ models.py
 │         ├─ tests.py
 │         ├─ views.py
 │         └─ templates/
 │              └─ core/
 │                   └─ home.html
 └─ README.md
````

---

## ⚡ Getting Started

### 1. Clone the repository

```bash
git clone <repository-url>
cd Day1
```

### 2. Create and activate virtual environment

```bash
python -m venv venv
# Windows
venv\Scripts\activate
# macOS/Linux
source venv/bin/activate
```

### 3. Install Django

```bash
pip install django
```

### 4. Run the development server

```bash
cd myproject
python manage.py runserver
```

Open your browser and go to:

```
http://127.0.0.1:8000/
```

You should see your first Django homepage.

---

## 📝 Lab Activity

**Task:**

1. Customize `home.html` to display your name and a welcome message
2. Optionally add today’s date using a Django template context
3. Experiment with a second page and URL routing

---

## 📖 Resources

* [Official Django Documentation](https://docs.djangoproject.com/en/stable/)
* [Django MVT Overview](https://docs.djangoproject.com/en/stable/intro/tutorial01/)
* [Python Virtual Environments](https://docs.python.org/3/tutorial/venv.html)

---

## ✅ Completion Checklist

* [ ] Virtual environment created and activated
* [ ] Django installed successfully
* [ ] Django project created
* [ ] App created and added to `INSTALLED_APPS`
* [ ] Basic view implemented
* [ ] URL routing configured
* [ ] Template rendered correctly
* [ ] Homepage accessible in browser

---

## 👨‍🏫 Notes for Learners

* Save your work frequently
* Pay attention to folder structure — templates must be inside `templates/<app_name>/`
* If server doesn’t start, check for typos or missing files
* Use the Django docs — they are beginner-friendly and comprehensive

---

**End of Day 1**

```

