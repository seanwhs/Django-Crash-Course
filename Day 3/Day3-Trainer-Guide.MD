# **📋 Day 3 — Trainer Guide**

**Django Crash Course — Forms, User Input, and POST Requests**

**Duration:** ~3 hours

---

## **🎯 Day 3 Learning Objectives**

By the end of Day 3, learners will be able to:

1. Explain the difference between `forms.Form` and `forms.ModelForm`
2. Create and handle forms in views
3. Validate user input and display errors
4. Save data to the database using ModelForms
5. Handle GET and POST requests
6. Redirect users after successful submissions

---

## **Lesson Breakdown & Trainer Notes**

---

### **0. Welcome & Recap (5 min)**

* Recap Day 2: Models, ORM, Admin Panel, displaying data
* Ask learners:
  *“Who can explain how to display posts dynamically in a template?”*

---

### **1. Introduction to Forms (10 min)**

**Talking Points:**

* Forms allow user input in web apps
* Django provides `forms.Form` and `forms.ModelForm`
* Benefits: validation, reduced boilerplate, integration with models

**Demo:** Show simple `ContactForm` example

**Question:**
“What’s the main difference between Form and ModelForm?”

---

### **2. Handling Forms in Views (20 min)**

**Explain:**

* `request.method` distinguishes GET vs POST
* `form.is_valid()` validates input
* `form.cleaned_data` accesses safe data

**Demo:** Implement contact form view

* Show GET request → empty form
* Show POST request → form validation and processing

---

### **3. Rendering Forms in Templates (15 min)**

**Explain:**

* Use `{{ form.as_p }}` to render fields
* Always include `{% csrf_token %}`

**Demo:** Template for contact form

* Show browser rendering
* Demonstrate submission errors

---

### **4. ModelForm Overview (20 min)**

**Explain:**

* Automatically generates fields from model
* Saves data directly with `form.save()`
* Reduces repetitive code

**Demo:** Create `PostForm` ModelForm for `Post` model

---

### **5. Handling ModelForm in Views (25 min)**

**Explain:**

* GET request: show empty form
* POST request: validate → save → redirect
* Discuss importance of redirect after POST (PRG pattern)

**Demo:** `create_post` view

* Add a new post
* Redirect to post list

---

### **6. Form Validation (20 min)**

**Explain:**

* Built-in: required fields, max length, email
* Custom: define `clean_<field>()` methods
* Display errors in template

**Demo:** Custom validation for post title

**Activity:** Ask learners to implement a rule:
*Title must contain the word “Django”*

---

### **7. POST vs GET (10 min)**

**Explain:**

* GET: retrieve data, parameters in URL
* POST: submit data, parameters in request body
* Forms that alter the database must use POST

**Quick Quiz:** “What happens if we submit a form using GET for sensitive data?”

---

### **8. Lab Assignment (45–50 min)**

**Objective:** Build a Post creation form

**Steps:**

1. Create `PostForm` as a ModelForm
2. Create `create_post` view to handle GET/POST
3. Create template `create_post.html`
4. Validate input and display errors
5. Save valid data to database
6. Redirect to post list on success

**Trainer Tips:**

* Walk around to check form submissions
* Encourage learners to test validation rules
* Show browser developer console for debugging POST requests

---

### **9. Checkpoints & Review (10 min)**

* [ ] Form created using `forms.Form` or `ModelForm`
* [ ] POST request handled correctly
* [ ] Validation works and errors displayed
* [ ] Data saved in database
* [ ] Redirection after POST implemented

**Review Questions:**

* Difference between Form and ModelForm
* What is `cleaned_data`?
* Why must forms use `{% csrf_token %}`?

---

### **10. Quiz / Assessment (10 min)**

* Multiple choice: Form types, validation, POST/GET
* Short-answer: Explain PRG (Post-Redirect-Get) pattern
* Practical: Create a ModelForm and submit a new post

---

### **11. Wrap-Up & Next Steps (5 min)**

* Summary: Forms → Validation → POST → Save → Redirect
* Day 4 Preview: User Authentication — Login, Logout, Signup
* Tip: Encourage learners to experiment with custom validations and different form fields

---

# **Trainer Notes**

* Demonstrate both success and error flows in forms
* Emphasize the importance of validation and security (`csrf_token`)
* Encourage frequent testing in browser and Django shell
* Keep lab tasks incremental; ensure everyone can submit at least one post

