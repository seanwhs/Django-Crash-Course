# **Library Management System (LMS) – Django CRUD Project Documentation**

---

## **1. Project Overview**

**Project Name:** Library Management System (LMS)
**Purpose:** To provide librarians and staff with a centralized, user-friendly platform to manage books, members, and borrowing records efficiently.

**Key Features:**

1. **Book Management:** CRUD operations for books (title, author, ISBN, category, stock).
2. **Member Management:** CRUD operations for library members (name, email, membership status).
3. **Borrowing & Returns:** Track which member borrowed which book, due dates, and return status.
4. **Search & Filtering:** Search books by title, author, category; filter borrowed/available books.
5. **Authentication & Authorization:** Admin-only operations for sensitive data; user login for viewing status.
6. **Responsive UI:** Mobile-first design with Bootstrap 5.
7. **Reports:** Generate reports of books issued, overdue books, and member activity.

---

## **2. Conceptualization & Design**

Before coding, proper **conceptualization** ensures scalable and maintainable architecture.

### **2.1 Requirements Gathering**

* Identify **actors**: Librarian (admin), Staff, Member (read-only access).
* Determine **use cases**: Add book, Update book, Delete book, Borrow book, Return book, List overdue books.

### **2.2 Data Modeling**

Entities identified:

| Entity   | Attributes                                                         | Description               |
| -------- | ------------------------------------------------------------------ | ------------------------- |
| Book     | title, author, ISBN, category, stock, created_at, updated_at       | Represents a library book |
| Member   | first_name, last_name, email, phone, membership_date               | Library member details    |
| Borrow   | book (FK), member (FK), borrow_date, due_date, return_date, status | Tracks borrowing records  |
| Category | name, description                                                  | Book categories           |

**ER Diagram Concept:**

```
Member <-- Borrow --> Book
Book --> Category
```

### **2.3 Project Architecture**

Django follows **MTV (Model-Template-View)** architecture:

```
Models: Define database schema
Views: Business logic / handle requests
Templates: HTML + CSS + JS for UI
URLs: Routing layer connecting views
```

---

## **3. Setup & Installation**

### **3.1 Environment Setup**

```bash
# Install Python & Django
python -m venv env
source env/bin/activate  # Windows: env\Scripts\activate
pip install django psycopg2-binary
django-admin startproject lms
cd lms
python manage.py startapp library
```

### **3.2 Database Setup**

* **Development:** SQLite (default)
* **Production:** PostgreSQL recommended

```python
# settings.py
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'lms_db',
        'USER': 'postgres',
        'PASSWORD': 'password',
        'HOST': 'localhost',
        'PORT': '5432',
    }
}
```

---

## **4. Models**

```python
from django.db import models
from django.utils import timezone

class Category(models.Model):
    name = models.CharField(max_length=100, unique=True)
    description = models.TextField(blank=True)

    def __str__(self):
        return self.name

class Book(models.Model):
    title = models.CharField(max_length=200)
    author = models.CharField(max_length=100)
    isbn = models.CharField(max_length=20, unique=True)
    category = models.ForeignKey(Category, on_delete=models.SET_NULL, null=True)
    stock = models.PositiveIntegerField(default=0)
    created_at = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return f"{self.title} by {self.author}"

class Member(models.Model):
    first_name = models.CharField(max_length=50)
    last_name = models.CharField(max_length=50)
    email = models.EmailField(unique=True)
    phone = models.CharField(max_length=15)
    membership_date = models.DateField(default=timezone.now)

    def __str__(self):
        return f"{self.first_name} {self.last_name}"

class Borrow(models.Model):
    STATUS_CHOICES = [
        ('borrowed', 'Borrowed'),
        ('returned', 'Returned'),
        ('overdue', 'Overdue')
    ]

    book = models.ForeignKey(Book, on_delete=models.CASCADE)
    member = models.ForeignKey(Member, on_delete=models.CASCADE)
    borrow_date = models.DateField(default=timezone.now)
    due_date = models.DateField()
    return_date = models.DateField(null=True, blank=True)
    status = models.CharField(max_length=10, choices=STATUS_CHOICES, default='borrowed')

    def __str__(self):
        return f"{self.book.title} -> {self.member.first_name}"
```

---

## **5. Views & CRUD Operations**

### **5.1 Class-Based Views for CRUD**

```python
from django.views.generic import ListView, CreateView, UpdateView, DeleteView
from .models import Book
from django.urls import reverse_lazy

class BookListView(ListView):
    model = Book
    template_name = 'library/book_list.html'
    context_object_name = 'books'

class BookCreateView(CreateView):
    model = Book
    fields = ['title', 'author', 'isbn', 'category', 'stock']
    template_name = 'library/book_form.html'
    success_url = reverse_lazy('book_list')

class BookUpdateView(UpdateView):
    model = Book
    fields = ['title', 'author', 'isbn', 'category', 'stock']
    template_name = 'library/book_form.html'
    success_url = reverse_lazy('book_list')

class BookDeleteView(DeleteView):
    model = Book
    template_name = 'library/book_confirm_delete.html'
    success_url = reverse_lazy('book_list')
```

### **5.2 URLs**

```python
from django.urls import path
from .views import BookListView, BookCreateView, BookUpdateView, BookDeleteView

urlpatterns = [
    path('books/', BookListView.as_view(), name='book_list'),
    path('books/add/', BookCreateView.as_view(), name='book_add'),
    path('books/<int:pk>/edit/', BookUpdateView.as_view(), name='book_edit'),
    path('books/<int:pk>/delete/', BookDeleteView.as_view(), name='book_delete'),
]
```

---

## **6. Templates & Frontend**

* **Base Template:** `base.html` for consistent header, footer, navbar.
* **Book List Template:** Uses Bootstrap tables with search & pagination.
* **Forms:** Django `ModelForm` with Bootstrap styling.

**Example – book_list.html:**

```html
{% extends 'base.html' %}
{% block content %}
<div class="container mt-5">
    <h2>Books</h2>
    <a class="btn btn-primary mb-3" href="{% url 'book_add' %}">Add Book</a>
    <table class="table table-striped">
        <thead>
            <tr>
                <th>Title</th>
                <th>Author</th>
                <th>Category</th>
                <th>Stock</th>
                <th>Actions</th>
            </tr>
        </thead>
        <tbody>
            {% for book in books %}
            <tr>
                <td>{{ book.title }}</td>
                <td>{{ book.author }}</td>
                <td>{{ book.category.name }}</td>
                <td>{{ book.stock }}</td>
                <td>
                    <a class="btn btn-sm btn-info" href="{% url 'book_edit' book.pk %}">Edit</a>
                    <a class="btn btn-sm btn-danger" href="{% url 'book_delete' book.pk %}">Delete</a>
                </td>
            </tr>
            {% endfor %}
        </tbody>
    </table>
</div>
{% endblock %}
```

---

## **7. Authentication & Authorization**

* Use Django built-in `User` model.
* Librarians are **staff** or **superusers**.
* Protect CRUD views using `@login_required` and `UserPassesTestMixin`.

```python
from django.contrib.auth.mixins import LoginRequiredMixin, UserPassesTestMixin

class BookCreateView(LoginRequiredMixin, UserPassesTestMixin, CreateView):
    ...
    def test_func(self):
        return self.request.user.is_staff
```

---

## **8. Deployment & Best Practices**

### **8.1 Static Files**

```bash
python manage.py collectstatic
```

Configure Nginx to serve `/static/` and `/media/`.

### **8.2 Security**

* `DEBUG = False` in production
* Use **Django Security Middleware**
* Strong **secret key** management
* HTTPS & SSL

### **8.3 Performance**

* Database indexing on `ISBN` and `email`
* Use `select_related` / `prefetch_related` for query optimization

---

## **9. Testing & Quality Assurance**

* Unit tests for models and views
* Integration tests for full CRUD workflow
* Manual QA for responsive UI and forms
* Use **Django Test Client**:

```python
from django.test import TestCase
from .models import Book

class BookModelTest(TestCase):
    def test_book_creation(self):
        book = Book.objects.create(title="Django Guide", author="Admin", stock=5)
        self.assertEqual(book.title, "Django Guide")
```

---

## **10. Future Enhancements**

1. Add **email notifications** for overdue books
2. Implement **REST API** with DRF for external integration
3. Add **analytics dashboard** for borrowing trends
4. Support **barcode scanning** for books

---

## **11. Summary**

This project demonstrates:

* Full Django **MTV architecture** understanding
* Professional **CRUD operations**
* **Responsive UI** with Bootstrap
* **Authentication & authorization**
* **Database relationships** & integrity constraints
* **Best practices for production deployment**

**Outcome:** A scalable, maintainable, and production-ready Library Management System with clear documentation and extendable architecture.

---

**Visual diagram pack** for the Django Library Management System (LMS) project, suitable for professional documentation or portfolio presentation. 

* ER Diagram
* URL-to-View Map
* Component Layout
* Deployment Architecture

---

# **Library Management System – Visual Diagram Pack**

---

## **1. ER Diagram (Entity-Relationship Diagram)**

**Purpose:** Shows how database tables relate, with primary/foreign keys.

```
+----------------+       +----------------+        +----------------+
|   Member       |       |     Borrow     |        |     Book       |
+----------------+       +----------------+        +----------------+
| id (PK)        |<----->| id (PK)        |<-----> | id (PK)        |
| first_name     |       | book_id (FK)   |        | title           |
| last_name      |       | member_id (FK) |        | author          |
| email          |       | borrow_date    |        | isbn            |
| phone          |       | due_date       |        | stock           |
| membership_date|       | return_date    |        | category_id(FK) |
+----------------+       | status         |        +----------------+
                         +----------------+
                               ^
                               |
                               |
                         +----------------+
                         |   Category     |
                         +----------------+
                         | id (PK)        |
                         | name           |
                         | description    |
                         +----------------+
```

**Notes:**

* `Borrow` is a **junction table** linking `Member` and `Book`.
* `Category` groups books; one-to-many relationship with `Book`.
* `status` in `Borrow` ensures easy tracking of borrowed, returned, overdue books.

---

## **2. URL-to-View Mapping Diagram**

**Purpose:** Shows routing from URLs → Views → Templates.

```
[ /books/ ] --------------------> BookListView --------------------> book_list.html
[ /books/add/ ] ----------------> BookCreateView ------------------> book_form.html
[ /books/<id>/edit/ ] ----------> BookUpdateView ------------------> book_form.html
[ /books/<id>/delete/ ] --------> BookDeleteView ------------------> book_confirm_delete.html

[ /members/ ] ------------------> MemberListView ------------------> member_list.html
[ /members/add/ ] --------------> MemberCreateView ---------------> member_form.html
[ /members/<id>/edit/ ] --------> MemberUpdateView --------------> member_form.html
[ /members/<id>/delete/ ] ------> MemberDeleteView --------------> member_confirm_delete.html

[ /borrow/ ] -------------------> BorrowListView ------------------> borrow_list.html
[ /borrow/add/ ] ----------------> BorrowCreateView --------------> borrow_form.html
```

**Tip:** Arrows show **request flow**: user → URL → view → template → response.

---

## **3. Component Layout Diagram (Frontend)**

**Purpose:** Visual representation of UI component hierarchy.

```
Base Template
├── Navbar
│   ├── Home
│   ├── Books
│   ├── Members
│   └── Borrow
├── Main Content
│   ├── BookList / BookForm / BookDelete
│   ├── MemberList / MemberForm / MemberDelete
│   └── BorrowList / BorrowForm
├── Footer
```

**Notes:**

* Base template ensures **DRY principle** (Don’t Repeat Yourself).
* Each section maps to a **reusable Django template**.
* Navbar can show **conditional links** for authenticated staff users.

---

## **4. CRUD Workflow Diagram**

**Purpose:** Show step-by-step workflow for CRUD operations.

```
[User Clicks Add/Edit/Delete] 
          |
          v
   [Form / Confirmation Page]
          |
          v
   [Form Validation / Business Logic in View]
          |
          v
   [Database Operation via Model]
          |
          v
   [Success → Redirect / Failure → Show Errors]
          |
          v
      [Updated Template Rendered]
```

**Tip:** Highlights **MVC/MTV flow** and points where validation, permissions, and logic occur.

---

## **5. Deployment Architecture Diagram**

**Purpose:** Shows how the system runs in production.

```
        +----------------+
        |   User Browser |
        +----------------+
                |
                v
        +----------------+
        |     Nginx      |
        |  (Reverse Proxy|
        |   + Static)    |
        +----------------+
                |
                v
        +----------------+
        |   Gunicorn     |
        | (WSGI Server)  |
        +----------------+
                |
                v
        +----------------+
        |   Django App   |
        +----------------+
                |
        ---------------------
        |                   |
        v                   v
   +---------+         +---------+
   | PostgreSQL |       | Redis  |
   +---------+         +---------+
```

**Notes:**

* Nginx serves **static files** efficiently and acts as a reverse proxy.
* Gunicorn handles WSGI requests and interacts with Django app.
* PostgreSQL for persistent data, Redis optional for caching sessions or query results.
* HTTPS / SSL recommended for production.

---

## **6. State Transition Diagram for Borrowing**

**Purpose:** Visualize how books move through statuses.

```
[Available Book] 
       |
       v
   [Borrowed] --------> [Returned]
       |
       v
     [Overdue]
       |
       v
   [Returned / Renewed]
```

**Tip:** Shows **business logic flow** for status management.

---

## ✅ **Pro Tips for Professional Documentation**

1. Include **diagram captions** and **short explanations**.
2. Maintain **consistent shapes & colors**:

   * Tables: rectangles
   * Actions / processes: ovals or diamonds
   * Arrows: solid for normal flow, dashed for optional/conditional.
3. Link diagrams to sections of documentation for **clarity**.
4. Use **PlantUML, draw.io, Lucidchart, or Mermaid** to generate reusable diagrams.

---

