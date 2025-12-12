# **Engineering Guide**

This engineering guide breaks down the entire 5‑day Django Crash Course into a structured, technical, and implementation‑focused reference. Ideal for engineers who want both conceptual clarity and hands-on instructions.

---

# **📌 Overview**

Django is a high-level Python web framework following the **Model–View–Template (MVT)** pattern. It enables rapid development and clean, pragmatic design. This crash course equips engineers with the skills to build full-stack applications, covering fundamentals to intermediate tooling.

---

# **📅 Course Outline & Engineering Notes**

---

# **Day 1 — Foundations of Django**

## **1. Introduction**

### ✔ What is Django?

* A batteries-included Python web framework.
* Emphasizes security, scalability, and rapid development.

### ✔ Core Features

* **ORM** for database abstraction
* **Admin interface** auto-generated
* **Middleware system**
* **Authentication & authorization**
* **Strong security features** (XSS, CSRF, SQL injection prevention)

### ✔ MVT Architecture

* **Model** — data structure definitions
* **View** — business logic; returns HttpResponse
* **Template** — UI rendering (HTML)

### ✔ Project vs App

* **Project**: Global config + multiple apps
* **App**: A module providing specific functionality (blog, auth, shop)

---

## **2. Setup & Environment**

### ✔ Python Environment Setup

* Create venv:

  ```bash
  python -m venv venv
  source venv/bin/activate  # macOS/Linux
  venv\Scripts\activate    # Windows
  ```
* Install Django:

  ```bash
  pip install django
  ```

### ✔ Create a New Project

```bash
django-admin startproject myproject
```

### ✔ Directory Walkthrough

* `manage.py` — command-line utility
* `settings.py` — project configuration
* `urls.py` — global URL routes
* `wsgi.py/asgi.py` — server gateway entry points

---

## **3. First Django App**

### ✔ Create an App

```bash
python manage.py startapp core
```

### ✔ Views, URLs, Templates Flow

**Request → URL Dispatcher → View → Template → Response**

### ✔ URL Dispatcher

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.home, name='home'),
]
```

### ✔ Template Rendering

```python
return render(request, 'home.html', context)
```

---

# **Day 2 — Models, ORM & Admin**

## **4. Models & Database Basics**

### ✔ Defining Models

```python
class Post(models.Model):
    title = models.CharField(max_length=200)
    body = models.TextField()
    created = models.DateTimeField(auto_now_add=True)
```

### ✔ Migrations

```bash
python manage.py makemigrations
python manage.py migrate
```

### ✔ Django Shell

```bash
python manage.py shell
```

```python
Post.objects.create(title="Test", body="Example")
Post.objects.all()
```

---

## **5. Django Admin**

### ✔ Enable Admin

```bash
python manage.py createsuperuser
```

### ✔ Register Models

```python
from django.contrib import admin
from .models import Post
admin.site.register(Post)
```

### ✔ Basic Customization

* List display
* Search fields
* Filters

---

## **6. Templates in Depth**

### ✔ Template Inheritance

```
base.html → child templates
```

### ✔ Context Variables

```html
<h1>{{ post.title }}</h1>
```

### ✔ Filters & Tags

```html
{{ date|date:"Y-m-d" }}
```

### ✔ Static Files

```
{% load static %}
<img src="{% static 'img/logo.png' %}">
```

---

# **Day 3 — Forms, Views & Authentication**

## **7. Django Forms**

### ✔ Two Types

* `forms.Form`
* `forms.ModelForm`

### ✔ Example

```python
class ContactForm(forms.Form):
    name = forms.CharField(max_length=100)
    email = forms.EmailField()
```

### ✔ CSRF Protection

`{% csrf_token %}` required in all POST forms.

---

## **8. Class-Based Views (CBV)**

### ✔ Comparison

* **FBV** = simple functions
* **CBV** = reusable, DRY, built-in methods

### ✔ Generic Views

* `ListView`
* `DetailView`
* `CreateView`
* `UpdateView`
* `DeleteView`

Example:

```python
class PostListView(ListView):
    model = Post
    template_name = 'post_list.html'
```

---

## **9. User Authentication**

### ✔ Auth Workflows

* Login
* Logout
* Signup

### ✔ Access Control

```python
from django.contrib.auth.decorators import login_required
```

### ✔ Custom User Model (Intro)

Set before migrations:

```python
AUTH_USER_MODEL = 'accounts.User'
```

---

# **Day 4 — Intermediate Features**

## **10. REST API Intro (Optional)**

### ✔ Django REST Framework Basics

* Serializers
* ViewSets
* Routers

Example serializer:

```python
class PostSerializer(serializers.ModelSerializer):
    class Meta:
        model = Post
        fields = '__all__'
```

---

## **11. Deployment Essentials**

### ✔ Environment Variables

Use `.env` files.

### ✔ Debug vs Production

`DEBUG = False` in production only.

### ✔ Static Files

```bash
python manage.py collectstatic
```

### ✔ Deployment Options

* Railway / Render
* DigitalOcean
* Docker
* Gunicorn + Nginx

---

## **12. Additional Django Tools**

### ✔ Messages Framework

```python
messages.success(request, "Saved!")
```

### ✔ Email Sending

```python
send_mail(subject, msg, from_email, [to])
```

### ✔ File Uploads

`request.FILES`

### ✔ Caching

* LocMemCache
* Redis

---

# **Day 5 — Final Project**

## **📌 Build a Mini Full-Stack Django App**

Project ideas:

* Blog
* To-Do manager
* Mini e-commerce
* Notes with auth

### **Project Requirements**

* CRUD features
* User authentication
* Styled templates
* Admin customization
* Optional API endpoint

### **Deliverables**

* GitHub repository
* Deployment link
* README / documentation

---

# **End of Engineering Guide**


