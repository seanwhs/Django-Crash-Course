# **🧪 Day 4 — Lab Exercise**

**Django Crash Course — User Authentication: Signup, Login, Logout**

---

## **Lab Title:**

**Building a User Authentication System**

## **Estimated Time:**

~60 minutes

---

## **🎯 Lab Objectives**

By the end of this lab, learners will be able to:

* Implement user registration with `UserCreationForm`
* Authenticate users with `login()` and `authenticate()`
* Implement logout functionality
* Restrict access to specific pages for authenticated users
* Display user-specific content in templates

---

## **📁 Lab Outcome**

* Functional signup page
* Functional login and logout system
* Protected dashboard view accessible only to logged-in users
* Basic template navigation and user feedback

---

## **🧩 Lab Steps**

---

### **Step 1 — Create Signup Form View**

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

* Redirect users to the login page after signup
* Highlight that passwords are hashed automatically

---

### **Step 2 — Create Login View**

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
* `login()` creates a user session

---

### **Step 3 — Create Logout View**

```python
# core/views.py
from django.contrib.auth import logout
from django.shortcuts import redirect

def logout_view(request):
    logout(request)
    return redirect('login')
```

* Logs out the user and redirects to login page

---

### **Step 4 — Create Protected Dashboard**

```python
# core/views.py
from django.contrib.auth.decorators import login_required

@login_required
def dashboard(request):
    return render(request, 'core/dashboard.html', {'user': request.user})
```

* Only logged-in users can access this view
* Displays logged-in user information

---

### **Step 5 — Create Templates**

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

### **Step 6 — Add URL Routes**

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

* Navigate to `/signup/` to register
* Navigate to `/login/` to log in

---

### **Step 7 — Test Authentication**

1. Sign up a new user → should redirect to login page
2. Log in with the new user → should redirect to dashboard
3. Try accessing `/dashboard/` while logged out → should redirect to login
4. Logout → verify session is cleared

---

### **Step 8 — Stretch Goals**

* Add user-friendly messages (e.g., "Welcome, username!") using Django messages framework
* Style forms and pages with Bootstrap or custom CSS
* Add email field and profile page

---

## **✔ Lab Checkpoints**

* [ ] Signup form created and working
* [ ] User can log in successfully
* [ ] Logout clears the session
* [ ] Restricted pages require authentication
* [ ] Templates render correctly with navigation links

---

## **🛠 Troubleshooting Guide**

| Issue                   | Solution                                                 |
| ----------------------- | -------------------------------------------------------- |
| Login fails             | Check username/password and ensure user exists           |
| Cannot access dashboard | Verify `@login_required` decorator and URL configuration |
| CSRF token error        | Ensure `{% csrf_token %}` is in form                     |
| Form not displaying     | Check `{{ form.as_p }}` in template                      |
| Redirect not working    | Check URL names in `redirect()`                          |

---

# **🎉 Lab Complete**

Learners now have a fully functional user authentication system in Django, including signup, login, logout, and protected pages.

