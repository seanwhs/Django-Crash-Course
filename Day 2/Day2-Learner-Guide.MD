# **📘 Day 2 — Learner Guide**

**Django Crash Course — Models, Admin Panel, and ORM**

---

## **📍 Day 2 Goal**

By the end of Day 2, learners should be able to:

* Create Django models to represent database tables
* Make and apply migrations
* Use the Django Admin interface to manage data
* Query the database with Django ORM
* Display database content dynamically in templates

---

## **1. Recap of Day 1**

* Virtual environment setup and Django installation
* Project vs App
* Views and URL routing
* Templates and rendering

---

## **2. Introduction to Models**

**What is a model?**
A **model** is a Python class representing a database table. Django’s ORM (Object-Relational Mapper) translates models into SQL tables automatically.

**Example:**

```python
from django.db import models

class Post(models.Model):
    title = models.CharField(max_length=200)
    content = models.TextField()
    created_at = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return self.title
```

* `CharField(max_length=200)` → column for short text
* `TextField()` → long text
* `DateTimeField(auto_now_add=True)` → stores creation timestamp

---

## **3. Making Migrations**

* After creating or editing models:

```bash
python manage.py makemigrations
python manage.py migrate
```

* **makemigrations** → prepares the changes
* **migrate** → applies them to the database

**Tip:** Check `db.sqlite3` file in project folder — it stores your database.

---

## **4. Django Admin Panel**

* Allows you to add, edit, and delete data through a web interface.

**Steps:**

1. Create a superuser:

```bash
python manage.py createsuperuser
```

2. Access admin at:

```
http://127.0.0.1:8000/admin/
```

3. Log in with superuser credentials

**Register your model in `admin.py`:**

```python
from django.contrib import admin
from .models import Post

admin.site.register(Post)
```

**Optional customization:**

```python
class PostAdmin(admin.ModelAdmin):
    list_display = ("title", "created_at")
admin.site.register(Post, PostAdmin)
```

---

## **5. Django ORM (Querying the Database)**

### **Fetching data**

```python
from core.models import Post

Post.objects.all()               # All posts
Post.objects.get(id=1)           # Single post
Post.objects.filter(title__contains="Django")
```

### **Creating, updating, deleting**

```python
post = Post(title="My First Post", content="Hello Django")
post.save()                       # Create/save

post.title = "Updated Title"
post.save()                       # Update

post.delete()                      # Delete
```

---

## **6. Using Models in Views**

**Example — Display Posts**

```python
from django.shortcuts import render
from .models import Post

def post_list(request):
    posts = Post.objects.all()
    return render(request, "core/post_list.html", {"posts": posts})
```

**Template — `post_list.html`:**

```html
<h1>All Posts</h1>
{% for post in posts %}
    <h2>{{ post.title }}</h2>
    <p>{{ post.content }}</p>
    <small>{{ post.created_at }}</small>
{% endfor %}
```

---

## **7. Relationships Between Models**

* **One-to-Many (ForeignKey):**

```python
class Comment(models.Model):
    post = models.ForeignKey(Post, on_delete=models.CASCADE)
    text = models.TextField()
    created_at = models.DateTimeField(auto_now_add=True)
```

* **Many-to-Many:**

```python
class Tag(models.Model):
    name = models.CharField(max_length=50)
    posts = models.ManyToManyField(Post)
```

**Tip:** Always run `makemigrations` and `migrate` after adding relationships.

---

## **8. Lab Activity (Day 2)**

**Objective:** Display posts and comments using models and admin panel.

**Steps:**

1. Create `Post` model with `title`, `content`, `created_at`
2. Create `Comment` model linked to `Post` via `ForeignKey`
3. Register both models in `admin.py`
4. Create superuser and add some posts/comments via admin
5. Display posts in `post_list.html` using a template loop
6. Optional: Display associated comments below each post

---

## **9. Checkpoints**

* [ ] Models created and migrated successfully
* [ ] Admin panel accessible and data can be added/edited
* [ ] ORM queries tested in shell
* [ ] Templates display data dynamically
* [ ] One-to-many relationships implemented

---

## **10. Key Tips**

* Always define `__str__()` in models for readable admin names
* Remember `makemigrations` → `migrate` workflow
* Use Django shell for testing queries:

```bash
python manage.py shell
```

* Keep templates clean — avoid embedding logic

---

## **11. Resources**

* [Django Models Documentation](https://docs.djangoproject.com/en/stable/topics/db/models/)
* [Django ORM Queries](https://docs.djangoproject.com/en/stable/topics/db/queries/)
* [Django Admin Docs](https://docs.djangoproject.com/en/stable/ref/contrib/admin/)

---

# **🎉 Day 2 Complete**

Learners should now have a working blog-like structure with posts and comments visible via Admin and templates.

---
