# **📘 Day 3 — Learner Guide**

**Django Crash Course — Forms, User Input, and POST Requests**

---

## **📍 Day 3 Goal**

By the end of Day 3, learners will be able to:

* Create and use Django forms (`forms.Form` and `forms.ModelForm`)
* Handle GET and POST requests in views
* Validate user input
* Save form data to the database
* Display form errors and success messages in templates

---

## **1. Recap of Day 2**

* Models, migrations, and relationships
* Admin panel usage
* Displaying database content in templates
* ORM queries

---

## **2. Introduction to Forms**

**What is a Form?**

* A form allows users to submit data to your application.
* Django provides two main types:

  * **`forms.Form`** — standalone form
  * **`forms.ModelForm`** — automatically linked to a model

**Benefits of Django forms:**

* Automatically generate HTML fields
* Built-in validation
* Clean integration with views and models

---

## **3. Creating a Simple Form**

**Example — Contact Form using `forms.Form`:**

```python
from django import forms

class ContactForm(forms.Form):
    name = forms.CharField(max_length=100)
    email = forms.EmailField()
    message = forms.CharField(widget=forms.Textarea)
```

* `CharField` → short text
* `EmailField` → email validation
* `TextArea` → multiline input

---

## **4. Handling Forms in Views**

```python
from django.shortcuts import render
from .forms import ContactForm

def contact_view(request):
    if request.method == 'POST':
        form = ContactForm(request.POST)
        if form.is_valid():
            # Access validated data
            name = form.cleaned_data['name']
            email = form.cleaned_data['email']
            message = form.cleaned_data['message']
            # Example: save to database or send email
    else:
        form = ContactForm()
    return render(request, 'core/contact.html', {'form': form})
```

* `request.method` distinguishes GET vs POST
* `form.is_valid()` checks validation
* `form.cleaned_data` contains safe data

---

## **5. HTML Template for Form**

```html
<h1>Contact Us</h1>
<form method="POST">
    {% csrf_token %}
    {{ form.as_p }}
    <button type="submit">Send</button>
</form>
```

* `{% csrf_token %}` prevents cross-site request forgery
* `{{ form.as_p }}` renders fields in `<p>` tags automatically

---

## **6. Using ModelForm**

**Example — Post Creation Form:**

```python
from django.forms import ModelForm
from .models import Post

class PostForm(ModelForm):
    class Meta:
        model = Post
        fields = ['title', 'content']
```

* Automatically generates form fields based on model
* Saves data to database using `form.save()`

---

## **7. Handling ModelForm in Views**

```python
from django.shortcuts import render, redirect
from .forms import PostForm

def create_post(request):
    if request.method == 'POST':
        form = PostForm(request.POST)
        if form.is_valid():
            form.save()
            return redirect('post_list')
    else:
        form = PostForm()
    return render(request, 'core/create_post.html', {'form': form})
```

* `redirect()` ensures user sees updated list after submission
* Validated data is automatically saved to the model

---

## **8. Form Validation**

* Built-in validation: required fields, max length, email format
* Custom validation: define `clean_<field>()` methods

```python
def clean_title(self):
    data = self.cleaned_data['title']
    if "django" not in data.lower():
        raise forms.ValidationError("Title must contain 'django'.")
    return data
```

---

## **9. Displaying Form Errors**

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

* Always show users which fields are invalid

---

## **10. POST vs GET**

| Method | Use Case      | Security                  |
| ------ | ------------- | ------------------------- |
| GET    | Retrieve data | Data visible in URL       |
| POST   | Submit data   | Data sent in request body |

* Forms that change the database should use POST

---

## **11. Lab Activity (Day 3)**

**Objective:** Create a form to add new blog posts

**Steps:**

1. Create `PostForm` as a `ModelForm`
2. Create view `create_post` to handle GET and POST
3. Create template `create_post.html` to render the form
4. Validate user input
5. Save valid form submissions to database
6. Redirect to post list on success

**Stretch Goals:**

* Add custom validation (e.g., title must include "Django")
* Display error messages for invalid input
* Style the form with CSS

---

## **12. Checkpoints**

* [ ] Form created using `forms.Form` or `ModelForm`
* [ ] POST requests handled correctly
* [ ] Validation works and errors are displayed
* [ ] Data saved to database
* [ ] User redirected after successful submission

---

## **13. Key Tips**

* Always use `{% csrf_token %}` in templates
* Keep validation in forms, not in templates or views
* Test forms in both GET and POST methods
* Use `cleaned_data` instead of `request.POST` directly

---

## **14. Resources**

* [Django Forms Documentation](https://docs.djangoproject.com/en/stable/topics/forms/)
* [ModelForm Documentation](https://docs.djangoproject.com/en/stable/topics/forms/modelforms/)
* [Form Validation](https://docs.djangoproject.com/en/stable/ref/forms/validation/)

---

# **🎉 Day 3 Complete**

Learners can now handle user input safely, validate forms, and save data using Django forms and ModelForms.

---

