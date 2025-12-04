# **🧪 Day 5 — Lab Exercise**

**Django Crash Course — Advanced Features & Project Integration**

---

## **Lab Title:**

**Build a Full Blog Application**

## **Estimated Time:**

~90–120 minutes

---

## **🎯 Lab Objectives**

By the end of this lab, learners will be able to:

* Implement a Post model with title, content, and image
* Use class-based views (CBVs) for CRUD operations
* Protect views using authentication
* Use messages framework for feedback
* Work with static files and media uploads
* Integrate all previous modules into a complete Django project

---

## **📁 Lab Outcome**

* Fully functional blog application
* Users can sign up, login, create, update, delete, and view posts
* Posts can include images uploaded by users
* User actions show messages (success/error)
* Styled with static CSS files

---

## **🧩 Lab Steps**

---

### **Step 1 — Create the Blog App**

```bash
python manage.py startapp blog
```

* Add `blog` to `INSTALLED_APPS` in `settings.py`

---

### **Step 2 — Create Post Model**

```python
from django.db import models
from django.contrib.auth.models import User

class Post(models.Model):
    title = models.CharField(max_length=200)
    content = models.TextField()
    image = models.ImageField(upload_to='posts/', blank=True, null=True)
    author = models.ForeignKey(User, on_delete=models.CASCADE)
    created_at = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return self.title
```

* Run migrations:

```bash
python manage.py makemigrations
python manage.py migrate
```

---

### **Step 3 — Implement Class-Based Views**

**ListView (display all posts)**

```python
from django.views.generic import ListView
from .models import Post

class PostListView(ListView):
    model = Post
    template_name = 'blog/post_list.html'
    context_object_name = 'posts'
```

**CreateView (add new post)**

```python
from django.views.generic import CreateView
from django.urls import reverse_lazy
from django.contrib.auth.mixins import LoginRequiredMixin
from .models import Post
from django.contrib import messages

class PostCreateView(LoginRequiredMixin, CreateView):
    model = Post
    fields = ['title', 'content', 'image']
    template_name = 'blog/create_post.html'
    success_url = reverse_lazy('post_list')

    def form_valid(self, form):
        form.instance.author = self.request.user
        messages.success(self.request, "Post created successfully!")
        return super().form_valid(form)
```

**UpdateView & DeleteView**

* Use `LoginRequiredMixin`
* Add messages for success/error

---

### **Step 4 — Configure URLs**

```python
from django.urls import path
from .views import PostListView, PostCreateView, PostUpdateView, PostDeleteView

urlpatterns = [
    path('', PostListView.as_view(), name='post_list'),
    path('create/', PostCreateView.as_view(), name='post_create'),
    path('update/<int:pk>/', PostUpdateView.as_view(), name='post_update'),
    path('delete/<int:pk>/', PostDeleteView.as_view(), name='post_delete'),
]
```

* Include `blog.urls` in main project `urls.py`

---

### **Step 5 — Create Templates**

**Base template (`base.html`)**

```html
<!DOCTYPE html>
<html>
<head>
    <title>Blog App</title>
    <link rel="stylesheet" href="{% static 'css/style.css' %}">
</head>
<body>
<nav>
    <a href="{% url 'post_list' %}">Home</a>
    {% if user.is_authenticated %}
        <a href="{% url 'post_create' %}">New Post</a>
        <a href="{% url 'logout' %}">Logout</a>
    {% else %}
        <a href="{% url 'login' %}">Login</a>
        <a href="{% url 'signup' %}">Sign Up</a>
    {% endif %}
</nav>
{% if messages %}
<ul>
    {% for message in messages %}
    <li>{{ message }}</li>
    {% endfor %}
</ul>
{% endif %}
{% block content %}{% endblock %}
</body>
</html>
```

**Post list (`post_list.html`)**

```html
{% extends 'base.html' %}
{% block content %}
<h1>All Posts</h1>
<ul>
    {% for post in posts %}
    <li>
        <h2>{{ post.title }}</h2>
        <p>{{ post.content }}</p>
        {% if post.image %}
        <img src="{{ post.image.url }}" alt="{{ post.title }}">
        {% endif %}
        {% if user == post.author %}
        <a href="{% url 'post_update' post.pk %}">Edit</a>
        <a href="{% url 'post_delete' post.pk %}">Delete</a>
        {% endif %}
    </li>
    {% endfor %}
</ul>
{% endblock %}
```

**Create/Update Post (`create_post.html` / `update_post.html`)**

```html
{% extends 'base.html' %}
{% block content %}
<h1>Create / Update Post</h1>
<form method="POST" enctype="multipart/form-data">
    {% csrf_token %}
    {{ form.as_p }}
    <button type="submit">Submit</button>
</form>
{% endblock %}
```

---

### **Step 6 — Configure Static & Media**

**settings.py**

```python
STATIC_URL = '/static/'
MEDIA_URL = '/media/'
MEDIA_ROOT = BASE_DIR / 'media'
```

**urls.py**

```python
from django.conf import settings
from django.conf.urls.static import static

urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```

---

### **Step 7 — Test the Application**

1. Signup → Login
2. Create a post with/without image
3. Verify post list renders correctly
4. Edit and delete posts as author
5. Confirm messages display for actions
6. Verify logout works

---

### **Step 8 — Stretch Goals**

* Add pagination to post list
* Add search functionality
* Add user profile page showing their posts
* Improve UI with CSS frameworks (Bootstrap/Tailwind)

---

## **✔ Lab Checkpoints**

* [ ] Post model created and migrated
* [ ] CBVs for CRUD implemented correctly
* [ ] LoginRequiredMixin protects create/update/delete views
* [ ] Messages show success/error feedback
* [ ] Static CSS and media uploads work
* [ ] Full workflow tested: signup → login → create/update/delete → logout

---

# **🎉 Lab Complete**

Learners now have a fully functional Django blog application integrating **authentication, CRUD, CBVs, messages, static & media files**.

