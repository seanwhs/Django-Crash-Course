# **🧪 Day 2 — Lab Exercise**

**Django Crash Course — Models, Admin, and ORM**

---

## **Lab Title:**

**Creating a Blog with Posts and Comments**

## **Estimated Time:**

~45–60 minutes

---

## **🎯 Lab Objectives**

By the end of this lab, learners will be able to:

* Create Django models (`Post` and `Comment`)
* Make and apply migrations
* Register models in the Admin panel
* Add, edit, and delete data via Admin
* Query data using Django ORM
* Display posts and comments dynamically in templates

---

## **📁 Lab Outcome**

* A small blog app where users can view posts and their comments.
* Data is managed via the Admin interface.

---

## **🧩 Lab Steps**

---

### **Step 1 — Create Post Model**

Edit `core/models.py`:

```python
from django.db import models

class Post(models.Model):
    title = models.CharField(max_length=200)
    content = models.TextField()
    created_at = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return self.title
```

---

### **Step 2 — Create Comment Model**

Add below `Post`:

```python
class Comment(models.Model):
    post = models.ForeignKey(Post, on_delete=models.CASCADE, related_name='comments')
    text = models.TextField()
    created_at = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return f"Comment on {self.post.title}"
```

---

### **Step 3 — Make and Apply Migrations**

```bash
python manage.py makemigrations
python manage.py migrate
```

**Check:** `db.sqlite3` should be updated.

---

### **Step 4 — Register Models in Admin**

Edit `core/admin.py`:

```python
from django.contrib import admin
from .models import Post, Comment

class CommentInline(admin.TabularInline):
    model = Comment
    extra = 1

class PostAdmin(admin.ModelAdmin):
    list_display = ('title', 'created_at')
    inlines = [CommentInline]

admin.site.register(Post, PostAdmin)
admin.site.register(Comment)
```

**Tip:** Inline allows adding comments directly under posts in Admin.

---

### **Step 5 — Create Superuser**

```bash
python manage.py createsuperuser
```

* Provide username, email, and password
* Log in at `http://127.0.0.1:8000/admin/`
* Add posts and comments

---

### **Step 6 — Query Data with ORM (Optional)**

Open shell:

```bash
python manage.py shell
```

**Example Queries:**

```python
from core.models import Post, Comment

# Fetch all posts
posts = Post.objects.all()

# Fetch comments of first post
comments = posts[0].comments.all()

# Create a new post
new_post = Post(title="Lab Post", content="Content here")
new_post.save()
```

---

### **Step 7 — Create View for Posts**

Edit `core/views.py`:

```python
from django.shortcuts import render
from .models import Post

def post_list(request):
    posts = Post.objects.all()
    return render(request, "core/post_list.html", {"posts": posts})
```

---

### **Step 8 — Configure URL**

Edit `core/urls.py`:

```python
from django.urls import path
from .views import post_list

urlpatterns = [
    path('', post_list, name='post_list'),
]
```

Ensure project `urls.py` includes core URLs:

```python
path('', include('core.urls')),
```

---

### **Step 9 — Create Template**

Create `core/templates/core/post_list.html`:

```html
<h1>Blog Posts</h1>
{% for post in posts %}
    <h2>{{ post.title }}</h2>
    <p>{{ post.content }}</p>
    <small>{{ post.created_at }}</small>
    
    <h3>Comments:</h3>
    <ul>
        {% for comment in post.comments.all %}
            <li>{{ comment.text }} — {{ comment.created_at }}</li>
        {% empty %}
            <li>No comments yet</li>
        {% endfor %}
    </ul>
{% endfor %}
```

---

### **Step 10 — Run Server and Test**

```bash
python manage.py runserver
```

Go to:

```
http://127.0.0.1:8000/
```

**Expected Outcome:**

* Posts display with their comments
* Data added via Admin appears dynamically

---

## **✔ Lab Checkpoints**

* [ ] `Post` and `Comment` models created
* [ ] Migrations applied successfully
* [ ] Admin panel accessible
* [ ] Inline comments configured in Admin
* [ ] ORM queries tested
* [ ] Templates display posts and comments correctly

---

## **🚀 Stretch Goals**

1. Add a Many-to-Many `Tag` model for posts
2. Display tags in templates
3. Add a “number of comments” count for each post
4. Style the page with CSS

---

## **🛠 Troubleshooting Guide**

| Issue                   | Solution                                               |
| ----------------------- | ------------------------------------------------------ |
| Server not starting     | Check for syntax errors                                |
| Template not loading    | Ensure folder: `templates/core/post_list.html`         |
| Admin not showing model | Confirm `admin.site.register()`                        |
| Migration errors        | Delete last migration if needed, re-run makemigrations |

---

# **🎉 Lab Completed**

