# **📚 Day 1 Lesson Plan

Django Crash Course**

## **Total Duration:** ~3 hours

Includes: learning objectives, timing, activities, notes, questions, and assessments.

---

# **🎯 Learning Objectives**

By the end of Day 1, learners will be able to:

1. Explain what Django is and why it’s used.
2. Describe the MVT architecture pattern.
3. Set up a Python virtual environment and install Django.
4. Create a Django project and application.
5. Build a basic view and URL route.
6. Create and render templates.
7. Run and test a Django development server.

---

# **📅 Lesson Breakdown**

---

# **0. Welcome & Setup (5 min)**

**Activities:**

* Quick introductions
* Check Python installation
* Ensure terminals/IDEs are ready

**Talking Points:**

* “Today we start building in Django immediately.”
* “Don’t worry about memorizing commands — focus on understanding the flow.”

---

# **1. What is Django? (20 min)**

### **Explain**

* Django = high-level web framework
* Built for rapid development
* Emphasize “batteries included” model

### **Show**

* Django website / documentation
* Examples of companies using Django
* Brief comparison table: Flask vs Django vs Node.js

### **Questions to Ask Learners**

* “Who has used a framework before?”
* “What type of projects would you build with Django?”

---

# **2. MVT Architecture (15 min)**

### **Explain**

* Model → database structure
* View → logic
* Template → UI

### **Diagram** (Draw or show slide)

```
Browser → URL → View → Model → View → Template → Browser
```

### **Check Understanding**

Ask: “Which part is responsible for logic? Which generates HTML?”

---

# **3. Environment Setup (20 min)**

### **Demonstrate**

* Creating virtual environment
* Activating it
* Installing Django

```bash
python -m venv venv
source venv/bin/activate
pip install django
```

### **Common Issues to Watch For**

* Wrong Python version
* PATH issues
* Permission errors on Windows

**Instructor tip:**
Walk around and ensure everyone’s terminal looks like `(venv)`.

---

# **4. Creating a Django Project (20 min)**

### **Demonstrate**

```bash
django-admin startproject myproject
cd myproject
python manage.py runserver
```

### **Observe**

* Everyone should see the Django welcome page

### **Explain**

* Project folder structure
* `settings.py`, `urls.py`, `manage.py`

**Engagement Prompt:**
“What do you think `settings.py` controls?”
“What else might go into a large project?”

---

# **5. Creating an App (15 min)**

### **Explain**

* Projects contain one or many apps
* Apps handle isolated functionality

### **Demonstrate**

```bash
python manage.py startapp core
```

### **Instructor Tip**

Make sure everyone updates `INSTALLED_APPS`.

---

# **6. Building Your First View (25 min)**

### **Explain**

* Views process requests
* Must return `HttpResponse` or `render()`

### **Demonstrate**

Create a simple view:

```python
def home(request):
    return HttpResponse("Hello Django!")
```

### **Activity**

Learners modify the text and refresh.

### **Check**

Ensure no import errors in `views.py`.

---

# **7. URL Routing (25 min)**

### **Explain**

* How Django finds matching URLs
* Role of `include()`

### **Demonstrate**

Create `core/urls.py` and connect to project URLs.

### **Learner Activity**

* Add a second URL route with a second view
* Test in browser

---

# **8. Templates (30 min)**

### **Explain**

* Why templates help maintain separation
* Basic Django template syntax

### **Demonstrate**

* Folder creation
* `home.html` customization
* Using `render()`

### **Learner Activity**

Add:

* Name
* Message
* Simple styling

### **Instructor Tip**

Walk around and ensure paths are correct:

```
core/templates/core/home.html
```

---

# **9. Static Files Preview (10 min)**

(Not in-depth; real lesson is Day 2.)

### **Explain**

* CSS/JS/images
* How Django organizes them

### **Show**

Use `{% load static %}` in a template.

---

# **10. Mini-Project (20–30 min)**

### **Task**

Build a homepage that:

* Uses a template
* Displays learner’s name
* Shows today’s date

### **Stretch Goals**

* Add second page
* Add navigation link

### **Instructor Role**

* Assist debugging
* Encourage exploration
* Validate core functionality

---

# **11. Review & Quiz (10 min)**

### **Review Checklist**

✔ MVT
✔ Views
✔ URL routing
✔ Templates
✔ Project/app creation

### **Quiz**

Administer the Day 1 quiz.

---

# **12. Q&A and Wrap-Up (5 min)**

### **Questions to Ask**

* “What was easiest today?”
* “What was hardest?”

### **End with**

* Overview of Day 2 topics: Models, ORM, Admin Panel

---

# **📘 Day 1 Lesson Plan Complete**
