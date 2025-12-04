# **Day 2 — Django Crash Course**

**Focus:** Models, Admin Panel, Database, and ORM

---

# **📊 Day 2 Slides Outline**

### **Slide 1 — Title Slide**

**Title:** Django Crash Course — Day 2
**Subtitle:** Models, Admin Panel, and ORM
**Speaker Notes:** “Welcome to Day 2! Today we’ll dive into Django’s database layer, creating models, using the admin panel, and understanding the ORM.”

---

### **Slide 2 — Day 2 Learning Objectives**

* Understand Django’s ORM and models
* Create and migrate database models
* Use the Django Admin interface
* Perform CRUD operations via shell and views
* Relate models to templates and views

---

### **Slide 3 — Recap: Day 1**

* Virtual environment and Django installation
* Project vs App
* Views and URL routing
* Templates and rendering

---

### **Slide 4 — Django Models Overview**

* **What is a model?**
  Python class that represents database tables

* **Why models?**

  * Define schema in Python
  * Auto-create database tables
  * Work seamlessly with ORM

* **Key Points:**

  * Each model maps to a table
  * Fields represent columns
  * Relationships: One-to-One, Many-to-One, Many-to-Many

---

### **Slide 5 — Model Fields**

| Field Type      | Description                     |
| --------------- | ------------------------------- |
| CharField       | Short text, max length required |
| TextField       | Long text                       |
| IntegerField    | Integer numbers                 |
| FloatField      | Floating-point numbers          |
| BooleanField    | True/False                      |
| DateTimeField   | Date and time                   |
| ForeignKey      | Many-to-One relationship        |
| ManyToManyField | Many-to-Many relationship       |

**Speaker Notes:** Show examples of each with Python code.

---

### **Slide 6 — Creating Your First Model**

```python
from django.db import models

class Post(models.Model):
    title = models.CharField(max_length=200)
    content = models.TextField()
    created_at = models.DateTimeField(auto_now_add=True)
```

* Explain each line
* `auto_now_add` for timestamps
* `__str__()` optional but recommended

---

### **Slide 7 — Registering Models in Admin**

```python
from django.contrib import admin
from .models import Post

admin.site.register(Post)
```

* Explain: Makes models editable in Admin panel
* Show screenshot of Admin interface

---

### **Slide 8 — Migrations**

* **What is a migration?**

  * Keeps database schema in sync with models
* **Commands:**

```bash
python manage.py makemigrations
python manage.py migrate
```

* Explain workflow: change model → makemigrations → migrate

---

### **Slide 9 — Django Admin Panel**

* URL: `/admin/`
* Requires superuser creation:

```bash
python manage.py createsuperuser
```

* Demo: Add, edit, delete posts

---

### **Slide 10 — ORM: Querying the Database**

* Basic Queries:

```python
Post.objects.all()      # All posts
Post.objects.get(id=1)  # Single post
Post.objects.filter(title__contains="Django")
```

* Updating & deleting:

```python
post = Post.objects.get(id=1)
post.title = "New Title"
post.save()
post.delete()
```

---

### **Slide 11 — Integrating Models with Views**

```python
from django.shortcuts import render
from .models import Post

def post_list(request):
    posts = Post.objects.all()
    return render(request, "core/post_list.html", {"posts": posts})
```

* Explain context dictionary
* Show template looping over posts

---

### **Slide 12 — Templates for Models**

```html
{% for post in posts %}
<h2>{{ post.title }}</h2>
<p>{{ post.content }}</p>
<p>{{ post.created_at }}</p>
{% endfor %}
```

* Use `for` loop to display database content

---

### **Slide 13 — Relationships in Models**

* One-to-Many:

```python
class Comment(models.Model):
    post = models.ForeignKey(Post, on_delete=models.CASCADE)
    text = models.TextField()
```

* Many-to-Many:

```python
class Tag(models.Model):
    name = models.CharField(max_length=50)
    posts = models.ManyToManyField(Post)
```

---

### **Slide 14 — Admin Customization (Optional)**

* Customize list display:

```python
class PostAdmin(admin.ModelAdmin):
    list_display = ("title", "created_at")
admin.site.register(Post, PostAdmin)
```

---

### **Slide 15 — Checkpoints / Summary**

By end of Day 2:

* Create models and migrations
* Use Django Admin
* Query database via ORM
* Display database content in templates

---

### **Slide 16 — Lab Assignment**

* Create `Post` and `Comment` models
* Add data in Admin panel
* Display posts and comments on a webpage

---

### **Slide 17 — Day 2 Quiz / Assessment**

* Multiple-choice: Model fields, ORM commands
* Short answers: Difference between `makemigrations` vs `migrate`
* Practical: Add a post via Admin, display it in template

---

### **Slide 18 — Next Steps**

* Day 3: Forms, User Authentication, Views with POST requests
* Reminder: Keep models clean, use Admin for testing

---

