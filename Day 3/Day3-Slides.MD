# **Day 3 — Django Crash Course**

**Focus:** Forms, User Input, POST Requests, and Validation

---

# **📊 Day 3 Slides Outline**

---

### **Slide 1 — Title Slide**

**Title:** Django Crash Course — Day 3
**Subtitle:** Forms, User Input, and POST Requests
**Speaker Notes:** “Welcome to Day 3! Today we will learn how to handle user input, validate it, and process forms in Django.”

---

### **Slide 2 — Day 3 Learning Objectives**

By the end of the session, learners will be able to:

* Understand Django forms (built-in and model forms)
* Create HTML forms and handle POST requests
* Validate user input
* Save form data to the database
* Display success or error messages

---

### **Slide 3 — Recap: Day 2**

* Models and ORM
* Admin panel usage
* Displaying dynamic data in templates
* Relationships (One-to-Many, Many-to-Many)

---

### **Slide 4 — What Are Forms?**

* Forms allow users to input data
* Django provides two main ways:

  * **`forms.Form`** — for custom forms not directly tied to models
  * **`forms.ModelForm`** — automatically maps a model to a form

**Speaker Notes:** “Forms are the bridge between user input and the backend database.”

---

### **Slide 5 — Creating a Simple Form**

**Example: Contact Form using `forms.Form`**

```python
from django import forms

class ContactForm(forms.Form):
    name = forms.CharField(max_length=100)
    email = forms.EmailField()
    message = forms.CharField(widget=forms.Textarea)
```

* Explain `CharField`, `EmailField`, `TextArea` widget

---

### **Slide 6 — Handling Form in Views**

```python
from django.shortcuts import render
from .forms import ContactForm

def contact_view(request):
    if request.method == 'POST':
        form = ContactForm(request.POST)
        if form.is_valid():
            # Process form data
            name = form.cleaned_data['name']
            email = form.cleaned_data['email']
            message = form.cleaned_data['message']
            # Example: save to database or send email
    else:
        form = ContactForm()
    return render(request, 'core/contact.html', {'form': form})
```

* Explain `request.method`
* Highlight `form.is_valid()` and `cleaned_data`

---

### **Slide 7 — Creating HTML Template for Form**

```html
<h1>Contact Us</h1>
<form method="POST">
    {% csrf_token %}
    {{ form.as_p }}
    <button type="submit">Send</button>
</form>
```

* Explain importance of `{% csrf_token %}`
* `{{ form.as_p }}` renders fields automatically

---

### **Slide 8 — ModelForm Overview**

* Links a form to a model
* Saves data directly to the database
* Example:

```python
from django.forms import ModelForm
from .models import Post

class PostForm(ModelForm):
    class Meta:
        model = Post
        fields = ['title', 'content']
```

* Benefits: reduces boilerplate code

---

### **Slide 9 — Handling ModelForm in Views**

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

* Explain `form.save()`
* Explain `redirect()` after successful POST

---

### **Slide 10 — Form Validation**

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

### **Slide 11 — Displaying Form Errors**

* Errors can be displayed in template:

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

* Speaker Note: “Always give users feedback on invalid input.”

---

### **Slide 12 — POST vs GET**

* GET: data sent in URL (not secure for sensitive data)
* POST: data sent in request body (secure)
* Forms should generally use POST

---

### **Slide 13 — Integrating Forms with Templates**

* Example: Create Post form
* Render form in template
* Show errors and success messages

---

### **Slide 14 — Lab / Practical**

**Objective:** Add a form to create new blog posts

* Use `ModelForm` for `Post` model
* Render form in template
* Save post to database on submit
* Redirect to post list after creation

---

### **Slide 15 — Checkpoints / Summary**

By the end of Day 3:

* Learners can create custom forms (`forms.Form`)
* Learners can create `ModelForm` linked to models
* Handle POST requests
* Validate user input and display errors
* Save data to the database

---

### **Slide 16 — Next Steps**

* Day 4: User Authentication (Login, Logout, Signup)
* Day 4 builds on forms and POST requests to handle user accounts

