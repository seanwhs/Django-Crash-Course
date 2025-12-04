# **Django Crash Course — Day 5**

**Topic:** Advanced Django Features & Project Integration

---

## **📍 Day 5 Goal**

By the end of Day 5, learners will be able to:

* Use class-based views (CBVs) and generic views for CRUD operations
* Implement Django messages framework for user feedback
* Work with static files and media uploads
* Structure Django projects efficiently
* Integrate all modules into a mini project (Blog Application)
* Deploy and test a fully functional Django project locally

---

## **1. Recap**

* Day 4: User authentication (signup, login, logout, protected pages)
* Today: Advanced Django features and integrating everything into a mini project

---

## **2. Key Concepts**

* **Class-Based Views (CBVs)** → TemplateView, ListView, DetailView, CreateView, UpdateView, DeleteView
* **LoginRequiredMixin** → Restrict access to authenticated users
* **Messages Framework** → Success/error/info messages for user actions
* **Static Files** → CSS, JS, images that don’t change dynamically
* **Media Files** → Uploaded by users (images, documents)
* **Project Structure** → Organize apps, templates, and static folders efficiently

---

## **3. Example Views**

**ListView**

```python
from django.views.generic import ListView
from .models import Post

class PostListView(ListView):
    model = Post
    template_name = 'blog/post_list.html'
    context_object_name = 'posts'
```

**CreateView**

```python
from django.views.generic import CreateView
from django.urls import reverse_lazy
from django.contrib.auth.mixins import LoginRequiredMixin
from django.contrib import messages
from .models import Post

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

---

## **4. URLs**

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

---

## **5. Templates**

**base.html**

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

**post_list.html**

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

---

## **6. Lab Exercise**

**Objective:** Build a complete blog application integrating CBVs, CRUD, messages, static & media files, and authentication

**Steps:**

1. Create a `blog` app and Post model
2. Implement CBVs for List, Create, Update, Delete
3. Protect create/update/delete with `LoginRequiredMixin`
4. Add messages for user feedback
5. Add static files (CSS) and media uploads
6. Test full workflow: signup → login → create → edit → delete → logout

**Stretch Goals:**

* Pagination on post list
* Search functionality
* User profile page
* UI enhancements with CSS frameworks

---

## **7. Quiz**

**Topics Covered:**

* CBVs: ListView, DetailView, CreateView, UpdateView, DeleteView
* `LoginRequiredMixin`
* Messages framework
* Static & media files
* Project structure and integration

**Format:** Multiple choice, True/False, Short answer

**Resources:**

* [Django CBV Docs](https://docs.djangoproject.com/en/stable/topics/class-based-views/)
* [Messages Framework Docs](https://docs.djangoproject.com/en/stable/ref/contrib/messages/)
* [Static & Media Files Docs](https://docs.djangoproject.com/en/stable/howto/static-files/)

---

# **🎉 Day 5 Complete**

Learners now have a **fully functional Django blog application**, integrating all core and advanced features learned throughout the course.

