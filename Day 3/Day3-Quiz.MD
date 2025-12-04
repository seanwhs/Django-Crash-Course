# **📝 Day 3 Quiz**

**Django Crash Course — Forms & POST Requests**

**Focus:** `forms.Form`, `ModelForm`, validation, POST/GET, and templates
**Estimated Time:** 15–20 minutes
**Total Questions:** 15

---

## **📘 Multiple-Choice Questions (10)**

**1. Which class is used to create a form directly tied to a model?**
A. `forms.Form`
B. `forms.ModelForm`
C. `forms.Model`
D. `forms.ModelView`

---

**2. How do you check if a submitted form is valid in Django?**
A. `form.cleaned_data`
B. `form.valid()`
C. `form.is_valid()`
D. `form.check()`

---

**3. What does `form.cleaned_data` contain?**
A. Raw POST data
B. Validated and cleaned form input
C. HTML form structure
D. Error messages only

---

**4. Which template tag is required in every POST form to prevent CSRF attacks?**
A. `{% csrf_token %}`
B. `{% form_token %}`
C. `{% post_token %}`
D. `{% csrf_field %}`

---

**5. Which HTTP method is generally used to submit forms that modify data?**
A. GET
B. POST
C. PUT
D. DELETE

---

**6. How do you render a form in a template using paragraph tags?**
A. `{{ form.as_div }}`
B. `{{ form.as_table }}`
C. `{{ form.as_p }}`
D. `{{ form.render }}`

---

**7. Where should custom form validation logic be added?**
A. In `views.py`
B. In `forms.py` as `clean_<field>()`
C. In `urls.py`
D. In `models.py`

---

**8. What does `form.save()` do in a `ModelForm`?**
A. Validates the form
B. Saves form data to the database
C. Resets the form
D. Redirects the user

---

**9. Which of the following statements is true about GET and POST methods?**
A. GET is more secure than POST
B. POST data is sent in the URL
C. POST is used to modify data; GET retrieves data
D. GET should always be used for forms that submit passwords

---

**10. In the PRG (Post-Redirect-Get) pattern, what happens after a successful POST?**
A. Form is redisplayed
B. User is redirected to another page to prevent duplicate submission
C. Data is deleted
D. Browser refreshes automatically

---

## **📗 True / False Questions (3)**

**11. `forms.Form` is always tied to a database model.**
(True / False)

**12. Validation errors can be displayed in the template using `form.errors`.**
(True / False)

**13. CSRF protection is optional for POST forms.**
(True / False)

---

## **📙 Short Answer Questions (2)**

**14. Explain the difference between `forms.Form` and `forms.ModelForm`.**

**15. Why is `form.is_valid()` important before saving form data?**

---

## **🧾 Answer Key**

**Multiple Choice:**
1 — B
2 — C
3 — B
4 — A
5 — B
6 — C
7 — B
8 — B
9 — C
10 — B

**True / False:**
11 — False
12 — True
13 — False

**Short Answer:**
14 — `forms.Form` is a standalone form not tied to any database model; `forms.ModelForm` is linked to a Django model and can save data directly.
15 — `form.is_valid()` ensures the submitted data passes validation checks; only validated data should be saved to prevent errors or malicious input.

---

# **🎉 Quiz Complete**

Next step would be **Day 4**: User Authentication (Login, Logout, Signup).

