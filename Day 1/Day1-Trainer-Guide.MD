# **👨‍🏫 Day 1 — Trainer Guide

Django Crash Course**

This guide is for instructors delivering Day 1. It includes timing, talking points, pacing tips, demos, troubleshooting cues, and engagement strategies.

---

# **🎯 Day 1 Trainer Goals**

By the end of the session, learners should:

* Understand Django fundamentals & MVT.
* Set up a functioning Django environment.
* Build a project + app.
* Create views, routes, templates, and run the server.

---

# **🕒 Recommended Duration**

Total: **2.5 – 3 hours**
Breakdown:

* Intro to Django: 20 mins
* MVT Architecture: 15 mins
* Environment Setup: 20 mins
* Project Creation: 20 mins
* App Creation: 15 mins
* Views & URL Routing: 25 mins
* Templates: 30 mins
* Static Files Overview: 10 mins
* Mini-Project Support: 20–30 mins

---

# **1. Introduction to Django (20 mins)**

### **Trainer Talking Points**

* “Django is a batteries-included framework.”
* Mention real-world companies using it.
* Compare Django’s structure to Flask or Node.js to give context.

### **Demonstration**

* Show Django homepage.
* Briefly highlight documentation (official docs are excellent).

### **Common Learner Questions**

* “Is Django good for APIs?” → Yes, especially with DRF.
* “Is Django outdated?” → No; stable and widely used in industry.

---

# **2. Architecture: MVT (15 mins)**

### **Trainer Talking Points**

* Compare MVC → MVT.
* Emphasize the separation of concerns.
* Explain how Django handles "controllers" internally via middleware + routing.

### **Demo**

Draw a request/response flow on screen or board.

### **Trainer Notes**

Avoid going too deep on Models yet (that’s Day 2).

---

# **3. Environment Setup (20 mins)**

### **Trainer Talking Points**

* Explain what a virtual environment is and why it matters.
* Highlight differences across OS when activating venv.

### **Demo**

* Create venv step-by-step.
* Install Django and verify with:

  ```python
  python -m django --version
  ```

### **Troubleshooting Tips**

* **Windows permissions issues**: instruct learners to run terminal as administrator.
* **Mac/Linux path issues**: check Python version using `which python3`.

---

# **4. Creating a Django Project (20 mins)**

### **Trainer Talking Points**

* Explain project structure clearly.
* Highlight `settings.py` and `urls.py` as core components.

### **Demo**

* Create project live:

  ```bash
  django-admin startproject myproject
  ```
* Run server and let learners observe default Django page.

### **Check for Completion**

Ask learners to show the “rocket” welcome page.

---

# **5. Creating an App (15 mins)**

### **Trainer Talking Points**

* Explain why Django encourages multiple apps.
* Clarify difference between “project” and “app” from a modularity standpoint.

### **Demo**

```
python manage.py startapp core
```

* Show the new folder structure.
* Add the app to `INSTALLED_APPS`.

### **Tip**

Show what happens if `INSTALLED_APPS` is missing → errors in URL routing or templates.

---

# **6. Views & URL Routing (25 mins)**

### **Trainer Talking Points**

* Explain how Django matches URLs to view functions.
* Stress that a view must return **HttpResponse** or `render()`.

### **Demo**

Create a simple view:

```python
def home(request):
    return HttpResponse("Hello Django!")
```

Create `core/urls.py` and include it in main `urls.py`.

### **Engagement**

Ask learners to modify the text returned by the view and refresh browser.

### **Common Issues**

* Import errors in `urls.py`
* Forgetting to add `include()`

---

# **7. Templates (30 mins)**

### **Trainer Talking Points**

* Explain how templates help separate logic from UI.
* Mention Django template language (variables, logic — deep dive on Day 2).

### **Demo**

* Create `templates/core/home.html`.
* Show `render()` usage.

### **Activity**

Have learners customize their template:

* Add an `<h1>` name tag
* Add background color
* Add a paragraph

### **Troubleshooting**

* Wrong template path → teach app-level templates vs project-level templates
* Missing trailing slash in URL

---

# **8. Static Files Overview (10 mins)**

### **Trainer Talking Points**

* Explain concept of static vs template content.
* Mention they will explore static files in depth on Day 2.

### **Demo**

Show `{% load static %}` on a template.

---

# **9. Mini-Project (20–30 mins)**

### **Instructions**

Learners should create:

* A homepage template
* A simple dynamic message
* A second template/page (optional)
* URL navigation between pages

### **Trainer Duties**

* Walk around helping with errors
* Encourage experimenting with CSS
* Ensure all learners complete core tasks

---

# **End-of-Day Recap**

Spend 5 minutes reviewing:

* MVT
* Project/app creation
* Views
* URL routing
* Templates

---

# **Trainer Tips**

* Slow down during environment setup (most common point of failure).
* Encourage learners to share screens when stuck.
* Repeat the MVT diagram several times throughout Day 1.
* Praise working code frequently to keep morale high.

