# **Django Project Workbook – 2025**

**Objective:** Guide learners through building a Django project from scratch, emphasizing planning, design, and hands-on implementation.

---

## **Chapter 1: Conceptualization**

### **1.1 Project Idea & Goals**

**Example Project:** Library Management System

**Key Features:**

* CRUD for Books, Authors, Borrowers
* Borrowing/Returning workflow
* Authentication: Librarians vs Users
* Admin dashboard

**Exercise 1.1:** Write down **3 project ideas**. For each, identify:

* Main entities
* Relationships (1:1, 1:N, M:N)
* Required features

**Hint:** Use real-world analogies. For example, “Library” → books, authors, members.

---

### **1.2 Entity-Relationship Diagram (ERD)**

**Example ERD:**

```
Author ───< Book >─── Genre
Borrower ───< BorrowRecord >─── Book
```

* Author → Book: 1:N
* Borrower → BorrowRecord: 1:N
* Book ↔ Genre: M:N

**Exercise 1.2:** Draw your ERD for your project using pen/paper or a tool like [dbdiagram.io](https://dbdiagram.io/).

**Checkpoint:** Can you identify all relationships correctly?

---

## **Chapter 2: Database Design & Modeling**

### **2.1 Designing Models**

| Model        | Fields                                           |
| ------------ | ------------------------------------------------ |
| Author       | name, birth_year, country                        |
| Book         | title, author(FK), genre, published_date         |
| Borrower     | name, email, membership_date                     |
| BorrowRecord | book(FK), borrower(FK), borrow_date, return_date |

**Exercise 2.1:** Map your ERD to Django models. Consider fields, data types, constraints.

---

### **2.2 Example Django Models**

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

**Exercise 2.2:** Add Borrower and BorrowRecord models.

**Hint:** Use `ForeignKey` for 1:N relationships, `ManyToManyField` for M:N.

---

## **Chapter 3: Setting Up Django**

### **3.1 Project & App Creation**

```bash
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
pip install django

django-admin startproject library_project
cd library_project
python manage.py startapp books
python manage.py startapp borrowers
```

**Exercise 3.1:** Create apps for each feature of your project.

---

### **3.2 Directory Structure**

```
library_project/
 ├─ library_project/  # Project settings
 │   ├─ settings.py
 │   ├─ urls.py
 ├─ books/            # Books app
 │   ├─ models.py
 │   ├─ views.py
 │   ├─ templates/
 ├─ manage.py
```

**Checkpoint:** Can you explain the difference between a **project** and an **app**?

---

## **Chapter 4: Migrations & Admin**

### **4.1 Applying Migrations**

```bash
python manage.py makemigrations
python manage.py migrate
```

**Exercise 4.1:** Add sample data through Django admin.

---

### **4.2 Admin Registration**

```python
# books/admin.py
from django.contrib import admin
from .models import Author, Book

admin.site.register(Author)
admin.site.register(Book)
```

**Checkpoint:** Admin interface allows quick testing and CRUD.

---

## **Chapter 5: Views & Templates**

### **5.1 Function-Based Views**

```python
# books/views.py
from django.shortcuts import render
from .models import Book

def book_list(request):
    books = Book.objects.all()
    return render(request, "books/book_list.html", {"books": books})
```

### **5.2 Templates**

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

**Exercise 5.1:** Create a borrower list page.

---

### **5.3 URL Routing**

```python
# books/urls.py
from django.urls import path
from . import views

urlpatterns = [path('', views.book_list, name='book-list')]

# library_project/urls.py
from django.urls import path, include

urlpatterns = [
    path('books/', include('books.urls')),
]
```

**Checkpoint:** URLs connect browser requests to views.

---

## **Chapter 6: Forms & Validation**

### **6.1 Model Forms**

```python
from django import forms
from .models import Book

class BookForm(forms.ModelForm):
    class Meta:
        model = Book
        fields = ['title', 'author', 'genre', 'published_date']
```

### **6.2 Handling Forms in Views**

```python
def add_book(request):
    if request.method == "POST":
        form = BookForm(request.POST)
        if form.is_valid():
            form.save()
    else:
        form = BookForm()
    return render(request, "books/add_book.html", {"form": form})
```

**Exercise 6.1:** Implement borrower registration with validation.

---

## **Chapter 7: Authentication & Permissions**

* Use Django’s **User model**
* Protect pages:

```python
from django.contrib.auth.decorators import login_required

@login_required
def borrow_book(request):
    ...
```

**Checkpoint:** Understand authentication, login, logout, and session management.

---

## **Chapter 8: Testing & Debugging**

```python
from django.test import TestCase
from .models import Book

class BookModelTest(TestCase):
    def test_create_book(self):
        author = Author.objects.create(name="Test", birth_year=1980, country="USA")
        book = Book.objects.create(title="Test Book", author=author, genre="Fiction", published_date="2023-01-01")
        self.assertEqual(book.title, "Test Book")
```

**Exercise 8.1:** Write a test for BorrowRecord creation.

---

## **Chapter 9: Deployment & Best Practices**

* Use `.env` for secrets
* Configure `ALLOWED_HOSTS`
* Use Gunicorn + Nginx for production
* Optimize queries with `select_related` and `prefetch_related`
* Enable caching for expensive queries

**Checkpoint:** Can your project run safely in production?

---

## **Capstone Exercise: Build a Library Management System**

1. Draw ERD for all entities
2. Implement models and migrations
3. Add CRUD pages for Books and Borrowers
4. Add borrowing/returning workflow
5. Implement authentication and permissions
6. Write unit tests for models and views
7. Deploy locally or cloud

**Checkpoints & Reflection:**

* Can you plan before coding?
* Can you map requirements to models/views?
* Can you maintain secure, clean, scalable Django code?

---

## ✅ **Workbook Summary**

* **Conceptualization → Design → Implementation** workflow
* Modular apps, reusable code, and clean templates
* ORM for database abstraction
* Admin for rapid testing
* Forms, validation, and authentication
* Testing and deployment best practices

---

