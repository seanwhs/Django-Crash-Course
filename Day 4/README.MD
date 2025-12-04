# **Django Crash Course — Day 4**

**Topic:** User Authentication — Signup, Login, Logout

---

## **📍 Day 4 Goal**

By the end of Day 4, learners will be able to:

* Implement user registration using `UserCreationForm`
* Log in and log out users using Django’s authentication system
* Restrict access to pages using `login_required`
* Display user-specific content in templates
* Understand password hashing and validation

---

## **1. Recap**

* Day 3: Forms, POST requests, validation, ModelForms
* Today: User authentication and access control

---

## **2. Key Concepts**

* **UserCreationForm** → Django’s built-in form for creating users
* **authenticate()** → Checks credentials
* **login()** → Logs in user and creates a session
* **logout()** → Logs out user and clears session
* **login_required** → Decorator to restrict access to authenticated users
* **Password hashing** → Secure storage of passwords

---

## **3. Example Views**

**Signup View**

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

**Login View**

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
            return redirect('dashboard')
    return render(request, 'core/login.html')
```

**Logout View**

```python
from django.contrib.auth import logout
from django.shortcuts import redirect

def logout_view(request):
    logout(request)
    return redirect('login')
```

**Protected Dashboard**

```python
from django.contrib.auth.decorators import login_required

@login_required
def dashboard(request):
    return render(request, 'core/dashboard.html')
```

---

## **4. Templates**

**Signup (`signup.html`)**

```html
<h1>Sign Up</h1>
<form method="POST">
    {% csrf_token %}
    {{ form.as_p }}
    <button type="submit">Sign Up</button>
</form>
<a href="{% url 'login' %}">Already have an account? Login</a>
```

**Login (`login.html`)**

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

**Dashboard (`dashboard.html`)**

```html
<h1>Welcome, {{ user.username }}</h1>
<a href="{% url 'logout' %}">Logout</a>
```

---

## **5. URL Configuration**

```python
from django.urls import path
from .views import signup_view, login_view, logout_view, dashboard

urlpatterns = [
    path('signup/', signup_view, name='signup'),
    path('login/', login_view, name='login'),
    path('logout/', logout_view, name='logout'),
    path('dashboard/', dashboard, name='dashboard'),
]
```

---

## **6. Lab Exercise**

**Objective:** Build a full authentication system
**Steps:**

1. Implement user signup
2. Implement login and logout
3. Protect dashboard with `login_required`
4. Test registration, login, logout, and protected page access

**Stretch Goals:**

* Add login/logout messages
* Style templates with CSS
* Create profile update page

---

## **7. Quiz**

**Topics Covered:**

* `UserCreationForm`
* `authenticate()`, `login()`, `logout()`
* `login_required` decorator
* Password hashing and validation

**Format:** Multiple choice, True/False, short answer

**Resources:**

* [Django Authentication Documentation](https://docs.djangoproject.com/en/stable/topics/auth/)
* [UserCreationForm Docs](https://docs.djangoproject.com/en/stable/topics/auth/default/#usercreationform)

---

# **🎉 Day 4 Complete**

Learners now have a functional Django authentication system with signup, login, logout, and protected pages.

