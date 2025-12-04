# **📝 Post-Course Assessment**

**Django Crash Course — Post-Course Assessment**

**Purpose:** To assess the learner’s comprehension and practical application of Django concepts covered throughout the course.
**Format:** Multiple-choice questions, True/False, Short Answer
**Total Questions:** 12
**Estimated Time:** 15–20 minutes

---

## **📘 Multiple-Choice Questions (7)**

**1. Which of the following Django components is responsible for processing HTTP requests and rendering responses?**
A. Model
B. View
C. Template
D. URLconf

---

**2. How does Django’s ORM interact with the database?**
A. It manually executes SQL queries
B. It uses Python classes to generate SQL queries automatically
C. It stores data in JSON files
D. It requires raw SQL commands for database operations

---

**3. Which class-based view (CBV) is used to create new objects in a database?**
A. `CreateView`
B. `ListView`
C. `DetailView`
D. `DeleteView`

---

**4. What is the main advantage of using Class-Based Views (CBVs) over Function-Based Views (FBVs)?**
A. CBVs make code more complex
B. CBVs offer more flexibility and reusability
C. FBVs are more secure than CBVs
D. CBVs are slower than FBVs

---

**5. In Django, where do you define the URL routing for your app?**
A. `urls.py`
B. `settings.py`
C. `views.py`
D. `models.py`

---

**6. Which of the following is NOT a valid file for Django static files?**
A. CSS
B. JavaScript
C. Images
D. Database migrations

---

**7. What function does `messages.success(request, "Message")` serve in Django?**
A. It generates an HTML response
B. It sends a success message to the user, displayed in the template
C. It logs user errors in the backend
D. It adds a user to the database

---

## **📗 True / False Questions (3)**

**8. In Django, `MEDIA_URL` is used to define the base URL for accessing user-uploaded media files.**
(True / False)

---

**9. You can have both function-based views (FBVs) and class-based views (CBVs) within the same Django project.**
(True / False)

---

**10. The `context_object_name` attribute in a `ListView` allows you to change the variable name of the object passed to the template.**
(True / False)

---

## **📙 Short Answer Questions (2)**

**11. Explain the difference between `STATIC_URL` and `MEDIA_URL` in Django.**

**12. Describe the process of deploying a Django project locally (development server).**

---

## **🧾 Answer Key**

**Multiple Choice:**
1 — B
2 — B
3 — A
4 — B
5 — A
6 — D
7 — B

**True / False:**
8 — True
9 — True
10 — True

**Short Answer:**
11 — `STATIC_URL` refers to the URL path used to access static files (CSS, JavaScript, images) stored in the static directory, while `MEDIA_URL` is used for accessing user-uploaded files (like images, PDFs) stored in the media directory.
12 — To deploy a Django project locally, run `python manage.py runserver` from the project directory, which starts the Django development server at `http://127.0.0.1:8000/`. Make sure the database is migrated using `python manage.py migrate`, and static/media files are correctly configured in `settings.py`.

---

# **🎉 Post-Course Quiz Complete**

This assessment  helps evaluate your understanding and practical application of the Django concepts learned throughout the course. If you scored well, you're ready to build your own Django applications! If there were any challenging questions, feel free to review the material and continue practicing.

