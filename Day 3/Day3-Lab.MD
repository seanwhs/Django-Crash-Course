# **🧪 Day 3 — Lab Exercise**

**Django Crash Course — Forms, User Input, and POST Requests**

---

## **Lab Title:**

**Creating a Post Submission Form**

## **Estimated Time:**

~45–60 minutes

---

## **🎯 Lab Objectives**

By the end of this lab, learners will be able to:

* Create a `ModelForm` for the `Post` model
* Handle GET and POST requests in a view
* Validate user input (built-in and custom)
* Save form data to the database
* Display success or error messages in templates
* Redirect after successful submission

---

## **📁 Lab Outcome**

* A functional page to submit new blog posts
* Form validation prevents invalid submissions
* Data saved to database and displayed in post list

---

## **🧩 Lab Steps**

---

### **Step 1 — Create PostForm**

Create `core/forms.py`:

```python
from django.forms import ModelForm
from .models import Post

class PostForm(ModelForm):
    class Meta:
        model = Post
        fields = ['title', 'content']
```

**Tip:** This automatically generates form fields based on the `Post` model.

---

### **Step 2 — Add Custom Validation (Optional)**

```python
from django.core.exceptions import ValidationError

def clean_title(self):
    title = self.cleaned_data['title']
    if "django" not in title.lower():
        raise ValidationError("Title must contain the word 'Django'.")
    return title
```

* Place inside `PostForm` class

---

### **Step 3 — Create View for Form**

Edit `core/views.py`:

```python
from django.shortcuts import render, redirect
from .forms import PostForm

def create_post(request):
    if request.method == 'POST':
        form = PostForm(request.POST)
        if form.is_valid():
            form.save()
            return redirect('post_list')  # Redirect after successful submission
    else:
        form = PostForm()
    return render(request, 'core/create_post.html', {'form': form})
```

* Explain GET vs POST
* Show how `form.is_valid()` ensures proper validation

---

### **Step 4 — Create Template**

Create `core/templates/core/create_post.html`:

```html
<h1>Create a New Post</h1>

<form method="POST">
    {% csrf_token %}
    {{ form.as_p }}
    <button type="submit">Submit Post</button>
</form>

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

* `{% csrf_token %}` ensures security
* Errors displayed under form

---

### **Step 5 — Add URL Route**

Edit `core/urls.py`:

```python
from django.urls import path
from .views import create_post, post_list

urlpatterns = [
    path('', post_list, name='post_list'),
    path('create/', create_post, name='create_post'),
]
```

* Navigate to `http://127.0.0.1:8000/create/` to access form

---

### **Step 6 — Test Form Submission**

1. Fill in valid data → redirect to post list
2. Leave fields blank → observe validation errors
3. Try invalid title (if custom validation added) → error displays

---

### **Step 7 — Stretch Goals**

1. Add a `published_date` field to `PostForm`
2. Limit title length and display friendly error messages
3. Add a textarea placeholder for better UX
4. Style form with CSS (Bootstrap or custom)

---

## **✔ Lab Checkpoints**

* [ ] `PostForm` created and linked to `Post` model
* [ ] GET and POST requests handled correctly
* [ ] Form validation working (built-in + custom)
* [ ] Errors displayed properly in template
* [ ] Valid submissions saved to database
* [ ] Redirection after submission works

---

## **🛠 Troubleshooting Guide**

| Issue                         | Solution                                                |
| ----------------------------- | ------------------------------------------------------- |
| Form not rendering            | Check `{{ form.as_p }}` and template path               |
| CSRF token missing error      | Ensure `{% csrf_token %}` is in form                    |
| Validation errors not showing | Ensure template iterates through `form.errors`          |
| Form data not saving          | Check `form.is_valid()` and `form.save()`               |
| Redirect not working          | Verify `redirect('post_list')` and URL name correctness |

---

# **🎉 Lab Complete**

Learners now have a fully functional form to submit new blog posts, including validation and redirection.

