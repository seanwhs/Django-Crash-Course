# **📘 Day 1 — Learner Guide

Django Crash Course**

This learner guide supports everything taught on Day 1. It includes explanations, examples, commands, diagrams, and checkpoints so learners can follow the session confidently.

---

# **📍 Day 1 Goal**

By the end of Day 1, you should be able to:

* Describe what Django is and why it’s used.
* Understand Django’s MVT architecture.
* Set up a Django development environment.
* Create a Django project and app.
* Build your first view, URL route, and template.

---

# **1. What is Django?**

Django is a **high-level Python web framework** created to help developers build web applications quickly and cleanly.

### **Key Features**

* **ORM** (Object Relational Mapper)
* **Admin panel** auto-generated from models
* **Powerful URL routing**
* **Security built-in** (XSS, CSRF, SQL injection protection)
* **Scalable** and production-ready
* **Template engine** for rendering HTML

### **Who Uses Django?**

Companies like Instagram, Pinterest, Disqus, Eventbrite, and Mozilla.

---

# **2. Understanding MVT Architecture**

Django follows the **Model–View–Template** pattern:

### **Model**

* Represents the structure of your data.
* Defines DB schema using Python classes.

### **View**

* Contains business logic.
* Returns responses (HTML, JSON, etc.).

### **Template**

* HTML files combined with Django’s template language.

### **MVT Flow Diagram**

```
Browser → URL → View → Model → View → Template → User
```

---

# **3. Project vs App**

### **Project**

A container representing the overall website.
Contains:

* Global configuration
* Main URLs
* Settings
* Deployment interfaces

### **App**

A functional module inside a project.
Examples:

* Blog
* Authentication
* Store
* API

**One project can have many apps.**

---

# **4. Environment Setup**

### **Python installation**

Make sure you have Python 3.10+ installed.

### **Create Virtual Environment**

```bash
python -m venv venv
```

### **Activate venv**

Windows:

```bash
venv\Scripts\activate
```

macOS/Linux:

```bash
source venv/bin/activate
```

### **Install Django**

```bash
pip install django
```

---

# **5. Creating Your First Django Project**

### **Command**

```bash
django-admin startproject myproject
```

### **What’s created?**

```
myproject/
    settings.py
    urls.py
    wsgi.py
    asgi.py
manage.py
```

### **Run Server**

```bash
python manage.py runserver
```

Open in browser:

```
http://127.0.0.1:8000/
```

---

# **6. Creating a Django App**

Inside your project:

```bash
python manage.py startapp core
```

Add to settings:

```python
INSTALLED_APPS = [
    ...
    'core',
]
```

---

# **7. Creating Your First View**

Inside `core/views.py`:

```python
from django.http import HttpResponse

def home(request):
    return HttpResponse("Hello, Django!")
```

---

# **8. URL Routing**

Create `core/urls.py`:

```python
from django.urls import path
from .views import home

urlpatterns = [
    path('', home, name='home'),
]
```

Modify project `urls.py`:

```python
from django.urls import path, include

urlpatterns = [
    path('', include('core.urls')),
]
```

---

# **9. Template Basics**

Create folder:

```
core/templates/core/home.html
```

Add:

```html
<h1>Welcome to Django!</h1>
```

Modify view:

```python
from django.shortcuts import render

def home(request):
    return render(request, "core/home.html")
```

---

# **10. Static Files Overview**

Add a `/static/` folder inside your app to store CSS, JS, and images.

Example usage in templates:

```html
{% load static %}
<link rel="stylesheet" href="{% static 'css/style.css' %}">
```

Static files will be explored more on Day 2.

---

# **💡 Checkpoints**

### By now, you should be able to:

✔ Create and activate a virtual environment
✔ Install Django
✔ Start a Django project
✔ Start an app
✔ Create a view
✔ Create URL routes
✔ Render a template
✔ Understand Django’s design philosophy

If you can complete the Day 1 mini-project, you’re ready for Day 2.

---

# **🧪 Mini-Project (End of Day 1)**

Create a homepage that:

* Uses a template
* Renders HTML
* Displays your name
* Includes a custom message
* (Optional) Shows today’s date

---

# **✨ End of Day 1 Learner Guide**
