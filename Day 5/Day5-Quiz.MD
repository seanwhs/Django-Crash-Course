# **📝 Day 5 Quiz**

**Django Crash Course — Advanced Features & Project Integration**

**Focus:** CBVs, CRUD, messages framework, static/media files, project structure, integration
**Estimated Time:** 20–25 minutes
**Total Questions:** 15

---

## **📘 Multiple-Choice Questions (10)**

**1. Which of the following is a class-based view that displays a list of objects?**
A. `TemplateView`
B. `ListView`
C. `DetailView`
D. `CreateView`

---

**2. What is the purpose of `LoginRequiredMixin`?**
A. Protects CBVs so only authenticated users can access them
B. Automatically logs in a user
C. Redirects users to the home page
D. Provides form validation

---

**3. Which method in `CreateView` is overridden to attach the currently logged-in user to a new object?**
A. `form_valid()`
B. `get_context_data()`
C. `dispatch()`
D. `get_queryset()`

---

**4. How do you render messages in a Django template?**
A. `{% render messages %}`
B. `{% if messages %} ... {% for message in messages %} ... {% endfor %}`
C. `{{ messages.all }}`
D. `{{ request.messages }}`

---

**5. What is the purpose of `STATIC_URL` in Django?**
A. Store uploaded media files
B. Define the URL path for serving static files like CSS/JS
C. Configure database connection
D. Set admin login URL

---

**6. Where are media files uploaded by users stored?**
A. `STATIC_ROOT`
B. `MEDIA_ROOT`
C. `BASE_DIR`
D. `MEDIA_URL`

---

**7. What is the default name of the template variable in `ListView` for the list of objects?**
A. `object_list`
B. `items`
C. `list_objects`
D. `queryset_list`

---

**8. Which CBV is used to delete an object?**
A. `DetailView`
B. `DeleteView`
C. `UpdateView`
D. `TemplateView`

---

**9. Why is it recommended to include `enctype="multipart/form-data"` in forms?**
A. For CSRF protection
B. To allow file uploads
C. To prevent form submission errors
D. To make the form POST-only

---

**10. What is the recommended way to organize templates in a multi-app Django project?**
A. All templates in the root project folder
B. Separate templates folder per app, optionally a global templates folder
C. Only in `settings.py` folder
D. Inside static files

---

## **📗 True / False Questions (3)**

**11. Class-based views reduce repetitive code compared to function-based views.**
(True / False)

**12. Messages framework allows temporary feedback that persists across page redirects.**
(True / False)

**13. Media files can be served in production without additional configuration.**
(True / False)

---

## **📙 Short Answer Questions (2)**

**14. Explain the difference between `ListView` and `DetailView`.**

**15. Why is it important to structure a Django project with separate templates and static folders for each app?**

---

## **🧾 Answer Key**

**Multiple Choice:**
1 — B
2 — A
3 — A
4 — B
5 — B
6 — B
7 — A
8 — B
9 — B
10 — B

**True / False:**
11 — True
12 — True
13 — False

**Short Answer:**
14 — `ListView` displays a list of multiple objects; `DetailView` displays a single object’s details.
15 — Separating templates/static per app improves organization, avoids conflicts, and makes the project scalable.

---

# **🎉 Quiz Complete**

Learners are now ready to apply **advanced Django features** in a complete project and understand best practices for structuring Django apps.

