# **👨‍🏫 Day 4 — Trainer Guide**

**Django Crash Course — User Authentication (Signup, Login, Logout, Protected Pages)**

---

## **📍 Trainer’s Objectives for Day 4**

* Ensure learners understand how to implement user authentication (signup, login, logout).
* Help learners create login-required views to restrict access to certain pages.
* Walk learners through the implementation of Django's authentication system and how to protect views using `LoginRequiredMixin`.
* Guide learners in applying the authentication system to a project (e.g., blog app) during the lab session.

---

## **1. Course Overview for the Day**

### **Topic:**

**User Authentication — Signup, Login, Logout, Protected Pages**

### **Learning Goals:**

* **Signup and Login:** Use Django's built-in authentication views (`LoginView`, `LogoutView`) and forms for user registration and login.
* **Protected Pages:** Implement the `LoginRequiredMixin` to restrict access to views that require user authentication.
* **Session Management:** Understand how Django manages user sessions and keeps track of logged-in users.

### **Time Breakdown:**

1. **Introduction & Recap (10–15 minutes)**

   * Quick review of Day 3 concepts (CBVs, URLs, templates).
   * Transition to User Authentication topic.

2. **Django Authentication Overview (15–20 minutes)**

   * Discuss built-in authentication views (`LoginView`, `LogoutView`).
   * Explain Django’s session management.
   * Introduce `LoginRequiredMixin` to protect views.

3. **Lab: Implement Authentication in Blog App (30–40 minutes)**

   * Guide learners through creating a signup page, login page, and logout functionality.
   * Demonstrate how to protect the post creation page using `LoginRequiredMixin`.
   * Walk through verifying that users cannot access protected pages without logging in.

4. **Q&A / Troubleshooting (15 minutes)**

   * Address common questions and potential issues learners face (e.g., session management, redirects).
   * Assist learners with any difficulties related to the lab exercises.

---

## **2. Introduction & Recap (10–15 Minutes)**

* **Goal:** Set the stage for today’s lesson by reviewing previous concepts and introducing the new topic.

  * Ask learners what they already know about user authentication (e.g., what’s a login system, why is authentication necessary?).
  * Recap of **Day 3**: Quick review of CBVs, `ListView`, and `DetailView` (to make sure learners understand how views work before diving into user management).

---

## **3. Django Authentication System (15–20 Minutes)**

### **Explanation of Authentication Views and Methods:**

1. **LoginView & LogoutView**

   * Django provides built-in views to handle login and logout processes.
   * **LoginView** handles user login, validates credentials, and redirects the user upon successful login.
   * **LogoutView** handles logging out users by clearing their session data.

2. **Session Management**

   * When a user logs in, Django stores their session ID in the browser’s cookies, allowing them to remain logged in until they log out or their session expires.
   * Django’s session management system handles storing the user’s session, ensuring they stay authenticated across multiple requests.

3. **LoginRequiredMixin**

   * This mixin restricts access to a view unless the user is authenticated. It can be applied to CBVs (Class-Based Views) to protect certain pages that require the user to be logged in.

4. **Demo Implementation**

   * **`LoginView` Example:**

     ```python
     from django.contrib.auth.views import LoginView

     class CustomLoginView(LoginView):
         template_name = 'login.html'
     ```
   * **`LogoutView` Example:**

     ```python
     from django.contrib.auth.views import LogoutView
     ```
   * **Protecting Views with `LoginRequiredMixin`:**

     ```python
     from django.contrib.auth.mixins import LoginRequiredMixin
     from django.views.generic import ListView

     class ProtectedPostListView(LoginRequiredMixin, ListView):
         model = Post
         template_name = 'blog/post_list.html'
     ```

---

## **4. Lab: Implement Authentication in Blog App (30–40 Minutes)**

### **Lab Objective:**

Learners will integrate the user authentication system into the blog application they’ve been building, including signup, login, logout, and page protection.

### **Steps for the Lab:**

1. **Creating the Signup Page:**

   * Demonstrate how to create a simple signup form using Django's `UserCreationForm`:

     ```python
     from django.contrib.auth.forms import UserCreationForm
     from django.shortcuts import render, redirect

     def signup(request):
         if request.method == 'POST':
             form = UserCreationForm(request.POST)
             if form.is_valid():
                 form.save()
                 return redirect('login')
         else:
             form = UserCreationForm()
         return render(request, 'signup.html', {'form': form})
     ```

2. **Creating the Login Page:**

   * Show how to set up the login page using Django's built-in `LoginView`:

     ```python
     from django.contrib.auth.views import LoginView

     class CustomLoginView(LoginView):
         template_name = 'login.html'
     ```

3. **Creating the Logout Page:**

   * Demonstrate how to implement the logout functionality using Django’s `LogoutView`:

     ```python
     from django.contrib.auth.views import LogoutView

     urlpatterns = [
         path('logout/', LogoutView.as_view(), name='logout'),
     ]
     ```

4. **Protecting Post Creation Page:**

   * Show how to add the `LoginRequiredMixin` to a view to protect access to the post creation page:

     ```python
     from django.contrib.auth.mixins import LoginRequiredMixin
     from django.views.generic import CreateView
     from .models import Post

     class PostCreateView(LoginRequiredMixin, CreateView):
         model = Post
         fields = ['title', 'content']
         template_name = 'blog/post_create.html'
         success_url = '/posts/'
     ```

5. **Testing the Implementation:**

   * Have learners test the signup/login functionality and confirm that they cannot access the post creation page without being logged in.
   * Make sure learners are able to log out and verify the system’s behavior.

---

## **5. Troubleshooting & Q&A (15 Minutes)**

### **Common Issues to Watch for:**

* **Login Redirect Issues:**
  Ensure learners are aware of where to redirect users after login (e.g., using `LOGIN_REDIRECT_URL` in `settings.py`).

  ```python
  LOGIN_REDIRECT_URL = '/'
  ```

* **Session Handling:**
  If the user is logged in, ensure that the session is being stored and managed correctly by checking that the `request.user` is properly set in views.

* **Form Validation Errors:**
  If learners encounter issues with form validation (e.g., username already exists), ensure they understand how to check form errors and display appropriate messages in templates:

  ```html
  {% if form.errors %}
    <ul>
      {% for field in form %}
        {% for error in field.errors %}
          <li>{{ error }}</li>
        {% endfor %}
      {% endfor %}
    </ul>
  {% endif %}
  ```

* **Protection of Views:**
  Ensure that only logged-in users can access pages that require authentication by testing the `LoginRequiredMixin` and checking the behavior for unauthenticated users.

---

## **6. Key Takeaways for Learners:**

* **Django Authentication Views** (`LoginView`, `LogoutView`) simplify user authentication processes.
* **`LoginRequiredMixin`** is an efficient way to protect class-based views.
* **Session management** is handled automatically by Django, making it easier to track logged-in users.

---

## **7. Additional Resources**

* [Django Authentication Docs](https://docs.djangoproject.com/en/stable/topics/auth/)
* [User Authentication in Django — Official Guide](https://docs.djangoproject.com/en/stable/topics/auth/default/)
* [Django Class-Based Views Documentation](https://docs.djangoproject.com/en/stable/topics/class-based-views/)

---

# **🎉 Day 4 Complete!**

* Learners have now implemented **user authentication** in their Django applications.
* They've gained experience with **protecting views** and **session management**.
