# **📘 Day 5 — Learner Guide**

**Django Crash Course — Advanced Features & Project Integration**

---

## **📍 Day 5 Goal**

By the end of Day 5, learners will be able to:

* Use class-based views (CBVs) and generic views for CRUD operations
* Implement Django messages for user feedback
* Manage static files and media uploads
* Structure Django projects efficiently
* Integrate all modules into a mini project (Blog Application)

---

## **1. Recap**

* Day 4: User authentication (signup, login, logout, protected pages)
* Today: Advanced Django features and integrating everything into a mini project

---

## **2. Class-Based Views (CBVs)**

* CBVs allow you to write reusable and organized views
* Types of CBVs:

  * `TemplateView` → render templates
  * `ListView` → list objects
  * `DetailView` → single object detail
  * `CreateView`, `UpdateView`, `DeleteView` → CRUD operations

**Example: ListView**

```python
from django.views.generic import ListView
from .models import Post

class PostListView(ListView):
    model = Post
    template_name = 'core/post_list.html'
    context_object_name = 'posts'
```

---

## **3. Generic Views for CRUD**

**CreateView Example**

```python
from django.views.generic import CreateView
from .models import Post
from django.urls import reverse_lazy

class PostCreateView(CreateView):
    model = Post
    fields = ['title', 'content', 'image']
    template_name = 'core/create_post.html'
    success_url = reverse_lazy('post_list')
```

* Automatically handles form rendering and validation
* `success_url` redirects after form submission
* Protect views using `LoginRequiredMixin`:

```python
from django.contrib.auth.mixins import LoginRequiredMixin

class PostCreateView(LoginRequiredMixin, CreateView):
    ...
```

---

## **4. Messages Framework**

* Provides feedback to users (success, error, info)
* Example in view:

```python
from django.contrib import messages

messages.success(request, "Your post was created successfully!")
messages.error(request, "There was an error submitting your form.")
```

* Template rendering:

```html
{% if messages %}
<ul>
  {% for message in messages %}
  <li>{{ message }}</li>
  {% endfor %}
</ul>
{% endif %}
```

---

## **5. Static & Media Files**

**Static Files:** CSS, JS, images that don’t change dynamically

```python
STATIC_URL = '/static/'
```

**Media Files:** Uploaded by users

```python
MEDIA_URL = '/media/'
MEDIA_ROOT = BASE_DIR / 'media'
```

* Template example:

```html
<img src="{{ MEDIA_URL }}{{ post.image }}" alt="Post image">
<link rel="stylesheet" href="{% static 'css/style.css' %}">
```

---

## **6. Project Structure Best Practices**

* Organize apps by functionality
* Use `templates` and `static` folders inside each app or globally
* Separate settings for dev and production
* Use `urls.py` in each app and include in main project URLs

**Example structure:**

```
myproject/
├─ core/
│  ├─ templates/core/
│  ├─ static/core/
│  ├─ views.py
│  ├─ urls.py
├─ myproject/
│  ├─ settings.py
│  ├─ urls.py
```

---

## **7. Mini Project: Blog Application**

**Features:**

* User authentication (signup/login/logout)
* CRUD for posts (title, content, image)
* Display list of posts
* Protect create/update/delete with login required
* Messages for user feedback
* Static files (CSS) and media (uploaded images)

---

## **8. Step-by-Step Implementation**

### **Step 1: Create Blog App**

```bash
python manage.py startapp blog
```

### **Step 2: Create Post Model**

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

### **Step 3: Implement CBVs**

* `PostListView` → List all posts
* `PostCreateView` → Create post
* `PostUpdateView` → Update post
* `PostDeleteView` → Delete post
* Use `LoginRequiredMixin` for create/update/delete

### **Step 4: Add URLs**

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

### **Step 5: Add Templates**

* `post_list.html` → Display all posts
* `create_post.html` → Form to create post
* `update_post.html` → Form to edit post
* `base.html` → Reusable template with navigation

### **Step 6: Use Messages**

* Add success/error messages in create/update/delete views
* Render messages in `base.html`

### **Step 7: Static & Media**

* Place CSS/JS in `static/`
* Add media folder and configure `MEDIA_URL` and `MEDIA_ROOT`
* Use `{% static %}` and `{{ MEDIA_URL }}` in templates

### **Step 8: Test Project**

* Signup → Login → Create post → Update/Delete → Logout
* Verify messages display correctly
* Verify media uploads render correctly

---

## **9. Lab Activity (Day 5)**

**Objective:** Build a complete Blog application integrating all learned modules

**Steps:**

1. Create `blog` app
2. Implement Post model with CRUD functionality using CBVs
3. Protect create/update/delete with authentication
4. Use messages for feedback
5. Add static files (CSS) and media (image uploads)
6. Test full workflow

**Stretch Goals:**

* Add pagination to post list
* Add search functionality
* Add profile page for users

---

## **10. Checkpoints**

* [ ] CBVs implemented correctly
* [ ] CRUD operations functional
* [ ] Messages display correctly
* [ ] Static and media files work
* [ ] Project fully integrated and tested

---

## **11. Resources**

* [Class-Based Views Docs](https://docs.djangoproject.com/en/stable/topics/class-based-views/)
* [Generic Views Docs](https://docs.djangoproject.com/en/stable/ref/class-based-views/generic-display/)
* [Messages Framework Docs](https://docs.djangoproject.com/en/stable/ref/contrib/messages/)
* [Static and Media Files Docs](https://docs.djangoproject.com/en/stable/howto/static-files/)

---

# **🎉 Day 5 Complete**

Learners now have a fully functional Django blog application, integrating authentication, CRUD, CBVs, messages, static and media files.

