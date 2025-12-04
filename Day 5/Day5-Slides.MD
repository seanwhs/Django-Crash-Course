# **📊 Day 5 — Slides Outline**

**Topic:** Advanced Django Features & Project Integration

---

## **Slide 1: Title Slide**

**Title:** Django Crash Course — Day 5
**Subtitle:** Advanced Features & Project Integration
**Speaker Notes:**

* Welcome learners to the final day
* Recap Day 4: User authentication
* Introduce today’s focus: advanced Django features, integrating modules, and building a mini project

---

## **Slide 2: Day 5 Goals**

By the end of Day 5, learners will be able to:

* Use class-based views (CBVs) and generic views
* Implement Django messages framework
* Use static files and media uploads
* Structure a Django project efficiently
* Integrate all learned modules into a mini project
* Deploy a basic Django project locally

---

## **Slide 3: Class-Based Views (CBVs)**

**Content:**

* Django supports CBVs for reusable and organized code
* Types of CBVs:

  * `TemplateView` → render templates
  * `ListView` → display lists of objects
  * `DetailView` → display single object
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

**Speaker Notes:**

* CBVs reduce repetitive code compared to function-based views
* Explain context object name and template rendering

---

## **Slide 4: Generic Views for CRUD**

**CreateView Example**

```python
from django.views.generic import CreateView
from .models import Post
from django.urls import reverse_lazy

class PostCreateView(CreateView):
    model = Post
    fields = ['title', 'content']
    template_name = 'core/create_post.html'
    success_url = reverse_lazy('post_list')
```

* Automatically handles form rendering and validation
* `success_url` redirects after successful submission

---

## **Slide 5: Django Messages Framework**

**Content:**

* Provides feedback to users after actions (e.g., login success, form errors)
* Example:

```python
from django.contrib import messages

messages.success(request, "Your post was created successfully!")
messages.error(request, "There was an error submitting your form.")
```

* Templates can render messages:

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

## **Slide 6: Static Files & Media**

**Static Files:**

* CSS, JS, images that don’t change dynamically

```python
STATIC_URL = '/static/'
```

**Media Files:**

* Uploaded by users

```python
MEDIA_URL = '/media/'
MEDIA_ROOT = BASE_DIR / 'media'
```

**Template Example:**

```html
<img src="{{ MEDIA_URL }}{{ post.image }}" alt="Post image">
<link rel="stylesheet" href="{% static 'css/style.css' %}">
```

---

## **Slide 7: Project Structuring Best Practices**

* Organize apps by functionality
* Use `templates` and `static` folders inside each app or globally
* Separate settings for dev and production
* Use `urls.py` in each app and include in main project URLs

**Visual:** Diagram of Django project structure

---

## **Slide 8: Mini Project Integration**

**Project Idea:** Blog Application

* Users can:

  * Sign up and login
  * Create, edit, delete posts
  * View list of posts
  * Upload images with posts
* Integrates:

  * Forms & ModelForms
  * User authentication
  * CBVs & CRUD
  * Messages & template rendering
  * Static & media files

---

## **Slide 9: Lab Activity (Day 5)**

**Steps:**

1. Create a blog app with Post model
2. Implement CBVs for List, Create, Update, Delete
3. Protect Create/Update/Delete views with `login_required` or `LoginRequiredMixin`
4. Use messages framework to notify users
5. Add static files (CSS, JS)
6. Add media upload for posts
7. Test full workflow: signup → login → create post → view posts

---

## **Slide 10: Deployment (Local)**

* Run server: `python manage.py runserver`
* Access project at `http://127.0.0.1:8000/`
* Explain folder structure and static/media management for deployment

---

## **Slide 11: Key Tips**

* Use CBVs for cleaner code
* Use messages for user feedback
* Organize project folders logically
* Test all CRUD operations thoroughly
* Make templates reusable with `base.html`

---

## **Slide 12: Resources**

* [Class-Based Views Docs](https://docs.djangoproject.com/en/stable/topics/class-based-views/)
* [Generic Views Docs](https://docs.djangoproject.com/en/stable/ref/class-based-views/generic-display/)
* [Messages Framework Docs](https://docs.djangoproject.com/en/stable/ref/contrib/messages/)
* [Static and Media Files Docs](https://docs.djangoproject.com/en/stable/howto/static-files/)

---

## **Slide 13: Wrap-Up**

* Summary: CBVs, CRUD, messages, static/media, project structure
* Preview: Integrate all modules into a final project
* Encourage learners to continue building Django projects

