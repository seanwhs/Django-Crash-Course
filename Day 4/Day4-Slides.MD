# **📊 Day 4 — Slides Outline**

**Topic:** User Authentication — Login, Logout, Signup

---

## **Slide 1: Title Slide**

**Title:** Django Crash Course — Day 4
**Subtitle:** User Authentication: Login, Logout, Signup
**Speaker Notes:**

* Welcome learners to Day 4
* Recap Day 3: Forms and POST requests
* Introduce the goal of today: enabling users to securely register and log in

---

## **Slide 2: Day 4 Goals**

By the end of Day 4, learners will be able to:

* Understand Django’s built-in authentication system
* Create a user signup form
* Implement login and logout functionality
* Restrict access to pages for authenticated users
* Customize authentication templates

---

## **Slide 3: Django Authentication Overview**

**Content:**

* Django provides a built-in authentication system
* Key features:

  * Users (`django.contrib.auth.models.User`)
  * Authentication (`authenticate`, `login`, `logout`)
  * Permissions and groups
  * Password hashing and security

**Speaker Notes:**

* Explain why authentication is essential
* Mention security best practices (never store plain passwords)

---

## **Slide 4: User Model**

**Content:**

* Django default `User` fields:

  * username
  * email
  * password (hashed)
  * first_name, last_name
  * is_staff, is_superuser, is_active
* Can extend with `AbstractUser` or `AbstractBaseUser`

**Visual:** Diagram showing `User` model with fields

---

## **Slide 5: Creating Signup Form**

**Content:**

* Use Django’s `UserCreationForm` for signup
* Example:

```python
from django.contrib.auth.forms import UserCreationForm
from django.shortcuts import render, redirect

def signup_view(request):
    if request.method == 'POST':
        form = UserCreationForm(request.POST)
        if form.is_valid():
            form.save()
            return redirect('login')
    else:
        form = UserCreationForm()
    return render(request, 'core/signup.html', {'form': form})
```

**Speaker Notes:**

* Highlight `form.save()` automatically hashes the password
* Redirect user to login page after signup

---

## **Slide 6: Login Functionality**

**Content:**

* Django provides `authenticate()` and `login()` functions

```python
from django.contrib.auth import authenticate, login
from django.shortcuts import render, redirect

def login_view(request):
    if request.method == 'POST':
        username = request.POST['username']
        password = request.POST['password']
        user = authenticate(request, username=username, password=password)
        if user is not None:
            login(request, user)
            return redirect('home')
    return render(request, 'core/login.html')
```

**Speaker Notes:**

* `authenticate()` checks credentials
* `login()` sets session for authenticated user

---

## **Slide 7: Logout Functionality**

**Content:**

* Django provides `logout()` to log users out

```python
from django.contrib.auth import logout
from django.shortcuts import redirect

def logout_view(request):
    logout(request)
    return redirect('login')
```

* Redirect users after logout

---

## **Slide 8: Restricting Access**

**Content:**

* Use `login_required` decorator to protect views

```python
from django.contrib.auth.decorators import login_required

@login_required
def dashboard(request):
    return render(request, 'core/dashboard.html')
```

* Users must log in to access protected pages

---

## **Slide 9: Authentication Templates**

**Content:**

* Create simple HTML templates for signup, login, logout
* Use `{{ form.as_p }}` to render form fields
* Include links: “Don’t have an account? Sign up”

**Speaker Notes:**

* Encourage basic styling with CSS for usability

---

## **Slide 10: Password Validation**

**Content:**

* Django provides password validators:

  * Minimum length
  * Common password checks
  * Numeric passwords
* Configured in `settings.py`

---

## **Slide 11: Lab Activity (Day 4)**

**Objective:** Build a complete user authentication system

**Steps:**

1. Implement user signup using `UserCreationForm`
2. Implement login view using `authenticate()` and `login()`
3. Implement logout view
4. Protect pages with `login_required`
5. Test user registration, login, and restricted pages

---

## **Slide 12: Key Tips**

* Always redirect after login/logout/signup
* Never store plain text passwords
* Use Django messages to show login success/failure
* Test with multiple users

---

## **Slide 13: Resources**

* [Django Authentication Docs](https://docs.djangoproject.com/en/stable/topics/auth/)
* [UserCreationForm Docs](https://docs.djangoproject.com/en/stable/topics/auth/default/#usercreationform)
* [Login/Logout Docs](https://docs.djangoproject.com/en/stable/topics/auth/default/#how-to-log-a-user-in)

---

## **Slide 14: Wrap-Up**

* Summary: Signup → Login → Logout → Access control
* Preview: Day 5 — Advanced Django Features & Project Integration

