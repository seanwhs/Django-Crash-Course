# Django Crash Course — Day 2

Welcome to **Day 2** of the Django Crash Course!  
Today, we focus on **Models, Admin Panel, and ORM**. You will learn to create database-backed applications, manage data via Admin, and display it in templates.

---

## 📅 Day 2 Overview

**Goal:** Build a blog-like app with Posts and Comments, using models, migrations, Admin panel, and ORM queries.

**Key Learning Objectives:**
- Create Django models to represent database tables
- Apply migrations to update the database schema
- Use the Django Admin interface for CRUD operations
- Query the database with Django ORM
- Display model data dynamically in templates
- Implement relationships between models (One-to-Many, Many-to-Many)

---

## 🗂 Folder Structure

```text
Day2/
 ├─ myproject/
 │    ├─ manage.py
 │    ├─ myproject/
 │    │    ├─ __init__.py
 │    │    ├─ settings.py
 │    │    ├─ urls.py
 │    │    ├─ wsgi.py
 │    │    └─ asgi.py
 │    └─ core/
 │         ├─ __init__.py
 │         ├─ admin.py
 │         ├─ apps.py
 │         ├─ models.py
 │         ├─ tests.py
 │         ├─ views.py
 │         └─ templates/
 │              └─ core/
 │                   └─ post_list.html
 └─ README.md
````

---

## ⚡ Getting Started

### 1. Clone the repository

```bash
git clone <repository-url>
cd Day2
```

### 2. Activate virtual environment

```bash
# Windows
venv\Scripts\activate
# macOS/Linux
source venv/bin/activate
```

### 3. Install dependencies (if any)

```bash
pip install -r requirements.txt
```

### 4. Make and Apply Migrations

```bash
python manage.py makemigrations
python manage.py migrate
```

### 5. Create Superuser

```bash
python manage.py createsuperuser
```

---

## 📝 Lab Activity

**Task:** Build a small blog app

**Steps:**

1. Create `Post` model with `title`, `content`, `created_at`
2. Create `Comment` model with `text` and link to `Post` via `ForeignKey`
3. Register models in `admin.py`
4. Add posts and comments via Admin
5. Create a `post_list` view and template to display posts and comments
6. Test the app in browser at `http://127.0.0.1:8000/`

**Stretch Goals:**

* Add a `Tag` model with Many-to-Many relationship
* Display number of comments per post
* Style the page with CSS

---

## 📖 Resources

* [Django Models Documentation](https://docs.djangoproject.com/en/stable/topics/db/models/)
* [Django ORM Queries](https://docs.djangoproject.com/en/stable/topics/db/queries/)
* [Django Admin Docs](https://docs.djangoproject.com/en/stable/ref/contrib/admin/)

---

## ✅ Completion Checklist

* [ ] `Post` and `Comment` models created and migrated
* [ ] Admin panel accessible with superuser
* [ ] CRUD operations via Admin verified
* [ ] ORM queries tested in Django shell
* [ ] Templates display dynamic content
* [ ] Relationships implemented correctly

---

## 👨‍🏫 Notes for Learners

* Remember the workflow: **Models → Migrations → Admin → ORM → Templates**
* Use the Django shell to practice queries
* Keep templates clean — logic belongs in views, not templates
* Save your work frequently and commit often to Git

---

**End of Day 2**

