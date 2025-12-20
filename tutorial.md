# **Django Project Tutorial – 2025**

**Objective:** Guide learners from conceptualization to a production-ready Django project with step-by-step explanations, hands-on exercises, and design-focused thinking.

---

## **Module 1: Conceptualization – Why Django?**

### **1.1 Understanding Django**

* Django is a **high-level Python web framework** that encourages rapid development and clean design.
* Follows **MVC/MVT architecture**:

  * **Model** – database structure and business logic
  * **View** – logic for data presentation
  * **Template** – HTML representation
* Built-in features:

  * ORM (Object Relational Mapper)
  * Admin interface
  * Authentication system
  * Form handling and validation

💡 **Tip:** Think of Django as a **full-stack framework** for developers who want **structure, scalability, and productivity**.

---

### **1.2 Choosing a Project**

**Scenario Example:** “Library Management System”

* Features:

  * Manage Books, Authors, Borrowers
  * Track borrowing/returning books
  * Admin dashboard for librarians
* Goals:

  * Store structured data
  * Provide a CRUD interface
  * Ensure secure user access

**Exercise 1:**
Write down **3 potential Django projects** you want to build. Identify:

* Main entities (models)
* Relationships between entities (1:1, 1:N, M:N)
* Key features (CRUD, reports, authentication)

---

## **Module 2: Database & Data Modeling**

### **2.1 Identifying Models**

**Entities for Library System:**

| Model        | Fields                                           |
| ------------ | ------------------------------------------------ |
| Author       | name, birth_year, country                        |
| Book         | title, author(FK), genre, published_date         |
| Borrower     | name, email, membership_date                     |
| BorrowRecord | book(FK), borrower(FK), borrow_date, return_date |

💡 **Tip:** Always **think in terms of objects first**, not tables.

---

### **2.2 Designing Relationships**

* **Author → Book**: 1:N
* **Borrower → BorrowRecord**: 1:N
* **Book ↔ Genre**: M:N (use a join table or ManyToManyField)

**Exercise 2:** Draw an ER diagram for your project.

---

### **2.3 Normalization & Data Integrity**

* Avoid redundant data:

  * Do not store author name in Book table (use FK)
  * Use proper constraints (unique, not null)
* Ensure proper indexing for frequently queried fields

**Checkpoint:** Can you justify why each model and relationship exists?

---

## **Module 3: Setting Up Django Project**

### **3.1 Installation & Virtual Environment**

```bash
# Create virtual environment
python -m venv venv
source venv/bin/activate  # Linux/macOS
venv\Scripts\activate     # Windows

# Install Django
pip install django

# Verify installation
django-admin --version
```

---

### **3.2 Project Scaffold**

```bash
django-admin startproject library_project
cd library_project
python manage.py runserver
```

**Directory Layout:**

```
library_project/
 ├─ library_project/      # project settings
 │   ├─ settings.py
 │   ├─ urls.py
 ├─ manage.py
```

💡 **Tip:** Think of **project** as configuration, **apps** as modular features.

---

### **3.3 Creating Apps**

```bash
python manage.py startapp books
python manage.py startapp borrowers
```

**Exercise 3:** Create apps for each main feature of your project.

---

## **Module 4: Models & ORM**

### **4.1 Define Models**

```python
# books/models.py
from django.db import models

class Author(models.Model):
    name = models.CharField(max_length=100)
    birth_year = models.IntegerField()
    country = models.CharField(max_length=50)

class Book(models.Model):
    title = models.CharField(max_length=255)
    author = models.ForeignKey(Author, on_delete=models.CASCADE)
    genre = models.CharField(max_length=50)
    published_date = models.DateField()
```

---

### **4.2 Migrations**

```bash
python manage.py makemigrations
python manage.py migrate
```

**Exercise 4:** Add Borrower and BorrowRecord models and create migrations.

---

### **4.3 ORM Basics**

* Query all books: `Book.objects.all()`
* Filter by author: `Book.objects.filter(author__name="J.K. Rowling")`
* Related queries: `author.book_set.all()`

**Checkpoint:** Can you explain how Django ORM translates queries into SQL?

---

## **Module 5: Admin & Superuser**

### **5.1 Register Models**

```python
# books/admin.py
from django.contrib import admin
from .models import Book, Author

admin.site.register(Book)
admin.site.register(Author)
```

### **5.2 Create Superuser**

```bash
python manage.py createsuperuser
```

💡 **Tip:** Admin is a powerful tool for **quickly managing data and testing relationships**.

**Exercise 5:** Log in to admin and add sample data for all models.

---

## **Module 6: Views & Templates**

### **6.1 Function-Based Views**

```python
# books/views.py
from django.shortcuts import render
from .models import Book

def book_list(request):
    books = Book.objects.all()
    return render(request, "books/book_list.html", {"books": books})
```

### **6.2 Templates**

```html
<!-- books/templates/books/book_list.html -->
<h1>Books</h1>
<ul>
  {% for book in books %}
    <li>{{ book.title }} by {{ book.author.name }}</li>
  {% empty %}
    <li>No books available</li>
  {% endfor %}
</ul>
```

**Exercise 6:** Create a borrower list page with a template.

---

### **6.3 URL Routing**

```python
# books/urls.py
from django.urls import path
from . import views

urlpatterns = [
    path('', views.book_list, name='book-list')
]
```

```python
# library_project/urls.py
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('books/', include('books.urls')),
]
```

**Checkpoint:** Can you explain how URLs map to views?

---

## **Module 7: Forms & Validation**

### **7.1 Model Forms**

```python
# books/forms.py
from django import forms
from .models import Book

class BookForm(forms.ModelForm):
    class Meta:
        model = Book
        fields = ['title', 'author', 'genre', 'published_date']
```

### **7.2 Views for Form Handling**

```python
# books/views.py
def add_book(request):
    if request.method == "POST":
        form = BookForm(request.POST)
        if form.is_valid():
            form.save()
    else:
        form = BookForm()
    return render(request, "books/add_book.html", {"form": form})
```

**Exercise 7:** Implement borrower registration form with validation.

---

## **Module 8: Authentication & Permissions**

* Use Django’s built-in User model for authentication
* Restrict pages to logged-in users:

```python
from django.contrib.auth.decorators import login_required

@login_required
def borrow_book(request):
    ...
```

**Checkpoint:** Can you explain how Django handles authentication and sessions?

---

## **Module 9: Testing & Debugging**

* Use `python manage.py test` for unit tests
* Write tests for models, views, and forms:

```python
from django.test import TestCase
from .models import Book

class BookModelTest(TestCase):
    def test_create_book(self):
        book = Book.objects.create(title="Test", author_id=1, genre="Fiction", published_date="2020-01-01")
        self.assertEqual(book.title, "Test")
```

**Exercise 8:** Write a test for BorrowRecord creation.

---

## **Module 10: Deployment & Best Practices**

* Use `.env` for secret keys
* Configure `ALLOWED_HOSTS`
* Use Gunicorn + Nginx for production
* Optimize queries and use `select_related`/`prefetch_related` for performance
* Enable caching for expensive queries

---

## **Capstone Exercise: Build a Library Management System**

1. Draw ER diagram for all entities
2. Implement Django models, migrations, and admin
3. Create CRUD pages for Books and Borrowers
4. Implement borrowing/returning workflow
5. Add authentication: Librarians vs Users
6. Test all major features
7. Deploy locally or on cloud (Heroku/DigitalOcean)

---

### ✅ **Checkpoints & Reflections**

* Can you design the data model before coding?
* Can you map business requirements to models and views?
* Can you explain MVT architecture clearly?
* Can you write secure, maintainable Django code?
* Can you implement forms, validation, and authentication?

---

