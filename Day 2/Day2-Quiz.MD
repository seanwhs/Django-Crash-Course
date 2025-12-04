# **📝 Day 2 Quiz

Django Crash Course**

**Focus:** Models, Admin Panel, Migrations, and ORM
**Estimated Time:** 15–20 minutes
**Total Questions:** 15

---

## **📘 Multiple-Choice Questions (10)**

**1. What is a Django model?**
A. A Python class representing a database table
B. A template for HTML pages
C. A URL route configuration
D. A view function

---

**2. Which command applies model changes to the database?**
A. `python manage.py makemigrations`
B. `python manage.py migrate`
C. `python manage.py runserver`
D. `python manage.py create_model`

---

**3. How do you make a superuser for the Django Admin?**
A. `python manage.py superuser`
B. `python manage.py createsuperuser`
C. `python manage.py adminuser`
D. `python manage.py createsadmin`

---

**4. Which field type is best for storing long text?**
A. CharField
B. TextField
C. IntegerField
D. BooleanField

---

**5. How do you define a one-to-many relationship in Django?**
A. `ManyToManyField`
B. `OneToOneField`
C. `ForeignKey`
D. `RelationshipField`

---

**6. What does `objects.all()` do?**
A. Deletes all records
B. Fetches all objects from the database
C. Updates all objects
D. Creates a new object

---

**7. Where should you register models for the Admin panel?**
A. `models.py`
B. `views.py`
C. `admin.py`
D. `urls.py`

---

**8. Which of these is the correct way to render a model in a template?**
A. `{% for post in Post %}`
B. `{% for post in posts %}`
C. `{% for post in core %}`
D. `{% for post in Post.objects.all %}`

---

**9. Which command generates migration files after changing models?**
A. `python manage.py migrate`
B. `python manage.py makemigrations`
C. `python manage.py runserver`
D. `python manage.py startapp`

---

**10. What is the purpose of `related_name` in a ForeignKey field?**
A. It sets the database table name
B. It allows reverse access from the related object
C. It changes the field type
D. It automatically creates migrations

---

## **📗 True / False Questions (3)**

**11. You can add, edit, and delete model data using Django Admin.**
(True / False)

**12. Migrations must be run every time you change a model.**
(True / False)

**13. Django templates can access ORM query results passed in the context.**
(True / False)

---

## **📙 Short Answer Questions (2)**

**14. Explain the difference between `makemigrations` and `migrate`.**

**15. In your own words, what is the purpose of Django ORM?**

---

## **🧾 Answer Key**

**Multiple Choice:**
1 — A
2 — B
3 — B
4 — B
5 — C
6 — B
7 — C
8 — B
9 — B
10 — B

**True / False:**
11 — True
12 — True
13 — True

**Short Answer:**
14 — `makemigrations` creates migration files based on model changes; `migrate` applies those migrations to the database.
15 — Django ORM allows developers to interact with the database using Python objects and methods instead of writing raw SQL.

---

# **🎉 Quiz Complete**

