# **📝 Day 4 Quiz**

**Django Crash Course — User Authentication**

**Focus:** `UserCreationForm`, `authenticate()`, `login()`, `logout()`, `login_required`
**Estimated Time:** 15–20 minutes
**Total Questions:** 15

---

## **📘 Multiple-Choice Questions (10)**

**1. Which Django form is used for user registration?**
A. `UserForm`
B. `UserCreationForm`
C. `AuthenticationForm`
D. `ModelForm`

---

**2. What does `authenticate(request, username, password)` do?**
A. Logs in the user automatically
B. Creates a new user
C. Checks if credentials are valid and returns a user object
D. Hashes the password

---

**3. What does the `login(request, user)` function do?**
A. Redirects the user to the login page
B. Starts a session for the authenticated user
C. Logs out the user
D. Validates the password

---

**4. How do you log out a user in Django?**
A. `authenticate()`
B. `login()`
C. `logout()`
D. `end_session()`

---

**5. Which decorator restricts access to a view to logged-in users?**
A. `@authenticated_only`
B. `@login_required`
C. `@user_required`
D. `@auth_only`

---

**6. Where are Django user passwords stored?**
A. Plain text in the database
B. In settings.py
C. Hashed in the database
D. Cookies

---

**7. After signup, why is it recommended to redirect the user to the login page?**
A. To clear the session
B. To confirm account creation
C. To avoid duplicate form submission and allow login
D. To hash the password

---

**8. What happens if a logged-out user tries to access a `@login_required` view?**
A. They are redirected to the login page
B. They can still access it
C. Django throws a 500 error
D. Nothing happens

---

**9. Which of the following is NOT a default field in Django’s User model?**
A. `username`
B. `email`
C. `phone_number`
D. `password`

---

**10. How can you display the currently logged-in user in a template?**
A. `{{ user }}`
B. `{{ request.user }}`
C. Both A and B
D. `{{ current_user }}`

---

## **📗 True / False Questions (3)**

**11. `UserCreationForm` automatically hashes passwords before saving.**
(True / False)

**12. You must write custom code to check passwords during login.**
(True / False)

**13. Using `@login_required` protects views from unauthorized access.**
(True / False)

---

## **📙 Short Answer Questions (2)**

**14. Explain the difference between `authenticate()` and `login()`.**

**15. Why is it important to use hashed passwords in Django?**

---

## **🧾 Answer Key**

**Multiple Choice:**
1 — B
2 — C
3 — B
4 — C
5 — B
6 — C
7 — C
8 — A
9 — C
10 — C

**True / False:**
11 — True
12 — False
13 — True

**Short Answer:**
14 — `authenticate()` checks if the user credentials are valid and returns a user object; `login()` actually logs the user in by creating a session.
15 — Hashed passwords protect user data in case of database compromise; plain text passwords are insecure.

---

# **🎉 Quiz Complete**

