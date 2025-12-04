# **📊 Day 1 — Django Crash Course Slides Outline**

---

# **Slide 1 — Title Slide**

**Title:** *Django Crash Course — Day 1: Foundations*
**Subtitle:** Introduction to Django & Building Your First App
**Includes:**

* Course logo / Python + Django icons
* Instructor name
* Date

---

# **Slide 2 — What Is Django?**

**Key Points:**

* Django is a high-level, batteries-included Python web framework.
* Built for rapid development & clean design.
* Powers major platforms (Instagram, Pinterest, Disqus, etc.)
* Comes with ORM, admin panel, security features, URL routing, templates, and more out of the box.

**Visual Ideas:**

* Diagram showing Django as a full-stack framework.
* List of companies using Django.

---

# **Slide 3 — Why Use Django?**

**Key Points:**

* **Fast:** Enables rapid development with built-in features.
* **Secure:** Handles common vulnerabilities (XSS, CSRF, SQL Injection).
* **Scalable:** Used by global-scale applications.
* **Versatile:** APIs, full-stack websites, dashboards, CMS, e-commerce.

**Notes:**
Emphasize the “don’t repeat yourself” (DRY) philosophy.

---

# **Slide 4 — Django Architecture: MVT**

**Title:** *Understanding MVT (Model–View–Template)*
**Key Points:**

* **Model:** Manages database structure & data logic.
* **View:** Handles processing & returns responses.
* **Template:** Handles the UI layer (HTML rendering).
* MVT vs MVC: Django replaces Controller with built-in middleware & routing.

**Visual:**
MVT diagram showing request flow.

---

# **Slide 5 — Project vs App**

**Key Points:**

* **Project:** Entire Django configuration (settings, URLs, WSGI/ASGI).
* **App:** A modular component performing a specific function (blog, accounts, store, etc.).
* A project can contain multiple apps; apps can be reused in other projects.

**Visual:**
Folder tree example:

```
myproject/
    settings.py
    urls.py
    wsgi.py
blog/
    models.py
    views.py
    urls.py
```

---

# **Slide 6 — Setting Up Your Environment**

**Key Points:**

* Install Python (≥3.10 recommended).
* Create virtual environment:
  `python -m venv venv`
* Activate environment (Windows/macOS/Linux commands).
* Install Django:
  `pip install django`

**Important Notes:**

* Why we use virtual environments.
* Pip freeze best practices.

---

# **Slide 7 — Starting a New Django Project**

**Command:**

```
django-admin startproject myproject
```

**What Gets Created:**

* `settings.py` — project configuration
* `urls.py` — URL routing
* `manage.py` — command-line utility
* `wsgi.py`, `asgi.py` — deployment interfaces

**Visual:**
Exploded diagram of folder layout.

---

# **Slide 8 — Running the Development Server**

**Command:**

```
python manage.py runserver
```

**Key Points:**

* Django comes with a lightweight dev server.
* Default URL: `http://127.0.0.1:8000/`
* Automatic reload on code changes.

**Screenshot Suggestion:**
Default Django “Rocket” welcome page.

---

# **Slide 9 — Creating Your First App**

**Command:**

```
python manage.py startapp core
```

**App Structure Overview:**

* `views.py` — what your page returns
* `models.py` — database structure
* `urls.py` — route definitions (manually created)
* `templates/` — where HTML files live (you create this)

**Reminder:**
Add app to `INSTALLED_APPS` in `settings.py`.

---

# **Slide 10 — Creating a Basic View**

**Title:** *Your First Django View*
**Example Code:**

```python
# core/views.py
from django.http import HttpResponse

def home(request):
    return HttpResponse("Hello, Django!")
```

**Concepts Covered:**

* Views receive requests & return responses
* `HttpResponse` basics
* Minimal return structure

---

# **Slide 11 — URL Routing**

**Example:**
In `core/urls.py`:

```python
from django.urls import path
from .views import home

urlpatterns = [
    path('', home, name='home'),
]
```

In main `urls.py`:

```python
path('', include('core.urls'))
```

**Key Points:**

* How Django’s URL dispatcher works
* `path()` parameters
* Why we use `include()` for modular routing

---

# **Slide 12 — Intro to Templates**

**Title:** *Separating Logic from Presentation*

**Command:**
Create folder: `core/templates/core/home.html`

**Example:**

```html
<h1>Welcome to Django!</h1>
<p>This is rendered from a template.</p>
```

In `views.py`:

```python
from django.shortcuts import render

def home(request):
    return render(request, "core/home.html")
```

**Teaching Summary:**

* Templates let you write pure HTML
* Views pass data → templates render UI

---

# **Slide 13 — Template Rendering Flow**

**Flow Diagram:**
Browser → URL → View → Template → Response

**Key Points:**

* Template loader system
* Directory search order
* Rendering context (preview only; detailed later)

---

# **Slide 14 — Static Files Overview**

**Key Points:**

* CSS, JS, images are considered static files.
* Must configure `STATIC_URL` & directory.
* Use `{% load static %}` in templates.

**Example:**

```html
<link rel="stylesheet" href="{% static 'css/style.css' %}">
```

**Note:**
Deep dive on Day 2.

---

# **Slide 15 — Recap of Day 1 Concepts**

**Checklist:**
✔ What Django is
✔ Understanding MVT
✔ Setting up environment
✔ Creating project & app
✔ Views and URL routing
✔ Templates basics

**Transition:**
Day 2: Models, Database, ORM & Admin Panel

---

# **Slide 16 — Day 1 Mini-Project**

**Task:**
Build a homepage using a template that displays:

* A welcome message
* Your name
* Today’s date (optional dynamic content)

**Stretch Goal:**
Create a second page & link between pages.

---

# **Slide 17 — Q&A / Discussion**

**Prompts:**

* What confused you about MVT?
* Thoughts on structuring apps?
* Any challenges setting up environment?

---

# **Slide 18 — End of Day 1**

**Closing Slide:**

* “Great work! Onto Day 2 tomorrow!”
* Links to Django docs & resources

---

