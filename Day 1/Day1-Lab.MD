Great — here is the **Day 1 Lab** for the Django Crash Course.
This includes: objectives, instructions, checkpoints, stretch goals, troubleshooting notes, and expected results.

---

# **🧪 Day 1 — Lab Exercise

Django Crash Course**

## **Lab Title:**

**Building Your First Django Web Page (Project + App + View + Route + Template)**

## **Estimated Time:**

**35–45 minutes**

---

# **🎯 Lab Objectives**

By completing this lab, you will be able to:

* Create and activate a Python virtual environment
* Install Django
* Create a Django project
* Create an app
* Build a basic view
* Configure URL routing
* Create a template
* Render HTML using Django’s template engine

---

# **📁 Lab Outcome**

By the end, you will have a working web page accessible at:

```
http://127.0.0.1:8000/
```

Displaying a personalized homepage.

---

# **🧩 Lab Steps**

---

# **Step 1 — Create a Project Folder**

Create a folder anywhere on your system:

```bash
mkdir django_day1_lab
cd django_day1_lab
```

---

# **Step 2 — Create a Virtual Environment**

```bash
python -m venv venv
```

Activate it:

Windows:

```bash
venv\Scripts\activate
```

macOS/Linux:

```bash
source venv/bin/activate
```

### **Check:**

```bash
(venv) > python --version
```

You should see your Python version.

---

# **Step 3 — Install Django**

```bash
pip install django
```

### **Check:**

```bash
python -m django --version
```

---

# **Step 4 — Create a Django Project**

```bash
django-admin startproject myproject
cd myproject
```

### **Run Server**

```bash
python manage.py runserver
```

### Should see:

✔ Django rocket/launch page

If yes — move on.
If not — check errors in terminal.

---

# **Step 5 — Create a Django App**

Inside the project folder:

```bash
python manage.py startapp core
```

Add app to settings:

Open `myproject/settings.py` → find `INSTALLED_APPS`
Add `'core',`:

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'core',
]
```

---

# **Step 6 — Create Your First View**

Open `core/views.py`
Replace content with:

```python
from django.shortcuts import render

def home(request):
    return render(request, 'core/home.html')
```

---

# **Step 7 — Configure URL Routing**

## Create `core/urls.py`:

```python
from django.urls import path
from .views import home

urlpatterns = [
    path('', home, name='home'),
]
```

## Connect app URLs to project:

Open `myproject/urls.py`:

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('core.urls')),
]
```

---

# **Step 8 — Create a Template**

Inside your `core` app:

```
core/
 └─ templates/
      └─ core/
           └─ home.html
```

Create folders if missing.

## Create `home.html`:

```html
<!DOCTYPE html>
<html>
<head>
    <title>My Django Homepage</title>
    <style>
        body { 
            font-family: Arial; 
            background: #f4f4f4;
            text-align: center;
            padding-top: 50px;
        }
    </style>
</head>
<body>
    <h1>Welcome to My Django Site!</h1>
    <p>Hello, my name is <strong>{{ name }}</strong>.</p>
    <p>Today’s date is: {{ date }}</p>
</body>
</html>
```

---

# **Step 9 — Pass Data into Template (Optional Enhancement)**

Modify view:

```python
from django.shortcuts import render
from datetime import date

def home(request):
    context = {
        "name": "YOUR NAME HERE",
        "date": date.today()
    }
    return render(request, "core/home.html", context)
```

---

# **Step 10 — Run and Test**

```bash
python manage.py runserver
```

Go to:

```
http://127.0.0.1:8000/
```

You should see your custom homepage with your name and the current date.

---

# **✔ Lab Checkpoints**

### You have successfully:

* [ ] Created and activated a virtual environment
* [ ] Installed Django
* [ ] Created a Django project
* [ ] Created a Django app
* [ ] Added a view
* [ ] Configured URLs at project and app level
* [ ] Created a template
* [ ] Rendered a working homepage

If all are checked — your Day 1 lab is complete.

---

# **🚀 Stretch Goals (Optional)**

### Try one or more:

1. **Create a second page** (e.g., `/about/`).
2. Add a **navigation link** between pages.
3. Add your own CSS file using `{% load static %}`.
4. Use Django template tags to display dynamic content:

   ```html
   {% if name %}
       <p>Nice to meet you, {{ name }}!</p>
   {% endif %}
   ```

---

# **🛠 Troubleshooting Guide**

| Issue                              | Solution                                       |
| ---------------------------------- | ---------------------------------------------- |
| Virtual environment not activating | Check PATH, run terminal as admin              |
| Django not found                   | Reinstall: `pip install django`                |
| Template not loading               | Check folder structure and template path       |
| URL not found                      | Ensure you created and included `core/urls.py` |
| Server not running                 | Check if another process uses port 8000        |

---

# **🎉 Lab Completed**

