# **📘 Day 4 — Learner Guide**

**Django Crash Course — User Authentication**

---

## **📍 Day 4 Goal**

By the end of Day 4, learners will be able to:

* Create a user signup form
* Implement login and logout functionality
* Restrict access to pages for authenticated users
* Customize authentication templates
* Understand Django’s built-in authentication system

---

## **1. Recap**

* Day 3: Forms, POST requests, validation, ModelForms
* Learners can now handle user input and save it to the database
* Today’s focus: handling users, authentication, and access control

---

## **2. Django Authentication Overview**

* Django includes a built-in authentication system
* Features:

  * Users (`django.contrib.auth.models.User`)
  * Login and logout
  * Password hashing and validation
  * Permissions and groups

**Why use Django auth:**

* Secure handling of passwords
* Session management
* Easy integration with forms and views

---

## **3. User Model**

* Default fields:

  * `username`, `email`, `password` (hashed)
  * `first_name`, `last_name`
  * `is_staff`, `is_superuser`, `is_active`
* Can be extended using `AbstractUser` or `AbstractBaseUser`

---

## **4. Creating Signup Form**

**Use Django’s built-in `UserCreationForm`:**

```python
# core/views.py
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

**Notes:**

* `form.save()` hashes the password automatically
* Redirect to login page after successful signup

---

## **5. Login Functionality**

```python
# core/views.py
from django.contrib.auth import authenticate, login
from django.shortcuts import render, redirect

def login_view(request):
    if request.method == 'POST':
        username = request.POST['username']
        password = request.POST['password']
        user = authenticate(request, username=username, password=password)
        if user is not None:
            login(request, user)
            return redirect('dashboard')
    return render(request, 'core/login.html')
```

* `authenticate()` checks credentials
* `login()` sets the user session

---

## **6. Logout Functionality**

```python
# core/views.py
from django.contrib.auth import logout
from django.shortcuts import redirect

def logout_view(request):
    logout(request)
    return redirect('login')
```

* Clears session and logs the user out
* Redirect users after logout for better UX

---

## **7. Restricting Access**

* Use `login_required` decorator:

```python
from django.contrib.auth.decorators import login_required

@login_required
def dashboard(request):
    return render(request, 'core/dashboard.html')
```

* Only logged-in users can access the `dashboard` view
* Redirects unauthenticated users to login page

---

## **8. Authentication Templates**

**Signup template (`signup.html`)**

```html
<h1>Sign Up</h1>
<form method="POST">
    {% csrf_token %}
    {{ form.as_p }}
    <button type="submit">Sign Up</button>
</form>
<a href="{% url 'login' %}">Already have an account? Login</a>
```

**Login template (`login.html`)**

```html
<h1>Login</h1>
<form method="POST">
    {% csrf_token %}
    <input type="text" name="username" placeholder="Username" required>
    <input type="password" name="password" placeholder="Password" required>
    <button type="submit">Login</button>
</form>
<a href="{% url 'signup' %}">Don't have an account? Sign Up</a>
```

**Dashboard template (`dashboard.html`)**

```html
<h1>Welcome, {{ user.username }}</h1>
<a href="{% url 'logout' %}">Logout</a>
```

---

## **9. URL Configuration**

```python
# core/urls.py
from django.urls import path
from .views import signup_view, login_view, logout_view, dashboard

urlpatterns = [
    path('signup/', signup_view, name='signup'),
    path('login/', login_view, name='login'),
    path('logout/', logout_view, name='logout'),
    path('dashboard/', dashboard, name='dashboard'),
]
```

* Routes for signup, login, logout, and dashboard

---

## **10. Password Validation**

* Configured in `settings.py`:

```python
AUTH_PASSWORD_VALIDATORS = [
    {'NAME': 'django.contrib.auth.password_validation.UserAttributeSimilarityValidator'},
    {'NAME': 'django.contrib.auth.password_validation.MinimumLengthValidator'},
    {'NAME': 'django.contrib.auth.password_validation.CommonPasswordValidator'},
    {'NAME': 'django.contrib.auth.password_validation.NumericPasswordValidator'},
]
```

* Ensures strong passwords

---

## **11. Lab Activity (Day 4)**

**Objective:** Build a complete authentication system

**Steps:**

1. Implement user signup using `UserCreationForm`
2. Implement login view using `authenticate()` and `login()`
3. Implement logout view
4. Protect pages with `login_required`
5. Test registration, login, logout, and restricted page access

**Stretch Goals:**

* Add login/logout messages
* Style templates with CSS
* Allow users to update their profile

---

## **12. Checkpoints**

* [ ] Signup form created and working
* [ ] User can login successfully
* [ ] Logout clears session
* [ ] Restricted pages require authentication
* [ ] Templates render correctly with links and forms

---

## **13. Resources**

* [Django Authentication Documentation](https://docs.djangoproject.com/en/stable/topics/auth/)
* [UserCreationForm Docs](https://docs.djangoproject.com/en/stable/topics/auth/default/#usercreationform)
* [Login & Logout Docs](https://docs.djangoproject.com/en/stable/topics/auth/default/#how-to-log-a-user-in)

---

# **🎉 Day 4 Complete**

Learners now have a fully functional user authentication system in Django, including signup, login, logout, and restricted pages.

