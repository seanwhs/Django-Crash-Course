# **📋 Day 2 — Trainer Guide**

**Django Crash Course — Models, Admin Panel, and ORM**

---

## **📅 Duration:** ~3 hours

---

## **🎯 Day 2 Learning Objectives**

By the end of Day 2, learners will be able to:

1. Explain Django’s ORM and models
2. Create and migrate models
3. Use the Django Admin interface
4. Perform CRUD operations using ORM
5. Display model data in templates
6. Implement relationships between models

---

## **Lesson Breakdown & Trainer Notes**

---

### **0. Welcome & Recap (5 min)**

* Greet learners and recap Day 1 highlights:

  * Project & app structure
  * Views & URL routing
  * Templates

**Tip:** Ask: “Who remembers how to render a template in Django?”

---

### **1. Introduction to Models (15 min)**

**Talking Points:**

* Models = Python classes for database tables
* Django ORM translates models → SQL automatically
* Benefits of using ORM: abstraction, safety, portability

**Demo:** Show `Post` model example and explain fields

**Question:** “What is the difference between CharField and TextField?”

---

### **2. Making Migrations (15 min)**

**Explain Workflow:**

1. Edit/Create model
2. Run `makemigrations` → generates migration file
3. Run `migrate` → applies to database

**Demo:** Create a model and migrate

**Tip:** Show learners `db.sqlite3` file

---

### **3. Django Admin Panel (30 min)**

**Explain:**

* Admin allows adding/editing/deleting data without coding
* Register models in `admin.py`

**Demo:**

1. Create superuser (`createsuperuser`)
2. Log in at `/admin/`
3. Add Post entries

**Optional:** Show list display customization

**Check:** Ensure learners can log in and add posts

---

### **4. Django ORM Queries (30 min)**

**Explain:**

* `objects.all()` → retrieve all objects
* `objects.get()` → retrieve single object
* `filter()` → query with conditions
* Create, update, delete objects in shell

**Demo:** Use `python manage.py shell` for queries

**Activity:** Have learners fetch posts and update titles in shell

---

### **5. Using Models in Views (25 min)**

**Explain:**

* Context dictionary passes model data to templates
* `render(request, template, context)`

**Demo:** Create `post_list` view with Post.objects.all()

* Show template loop `{% for post in posts %}`

**Activity:** Learners display posts in a styled template

---

### **6. Relationships in Models (30 min)**

**Explain:**

* One-to-Many: `ForeignKey`
* Many-to-Many: `ManyToManyField`
* Demonstrate `Comment` model linked to `Post`

**Activity:**

* Learners create a `Comment` model and migrate
* Display comments under each post in template

---

### **7. Lab Assignment (30–35 min)**

**Task:** Build a small blog structure

1. Create `Post` and `Comment` models
2. Register them in Admin
3. Add posts and comments via Admin
4. Display posts and comments dynamically in template

**Trainer Tip:**

* Walk around to assist debugging
* Encourage testing ORM queries in shell

---

### **8. Checkpoints & Review (15 min)**

* [ ] Models created and migrated
* [ ] Admin panel accessible and functional
* [ ] ORM queries tested
* [ ] Templates display dynamic data
* [ ] Relationships implemented

**Review Questions:**

* Difference between `makemigrations` and `migrate`
* How to fetch all posts using ORM
* How to create a superuser

---

### **9. Quiz / Assessment (10 min)**

* Multiple-choice: Model fields, ORM commands, Admin usage
* Short-answer: Describe One-to-Many relationship
* Practical: Add a post in Admin, display on page

---

### **10. Wrap-Up & Next Steps (5 min)**

* Summarize: Models → Migrations → Admin → ORM → Templates
* Day 3 preview: Forms, User Input, POST requests, Validation

**Tip:** Encourage learners to experiment with different fields and relationships before Day 3.

---

# **Trainer Notes**

* Always demonstrate shell queries — learners find it interactive
* Highlight importance of folder structure (`templates/core/`)
* Encourage learners to explore Admin panel options (filters, search)
* Time checkpoints are approximate; adjust based on learner pace

---


