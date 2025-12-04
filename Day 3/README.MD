# **Django Crash Course — Day 3**

**Topic:** Forms, User Input, and POST Requests

---

## **📍 Day 3 Goal**

By the end of Day 3, learners will be able to:

* Create and use Django forms (`forms.Form` and `forms.ModelForm`)
* Handle GET and POST requests in views
* Validate user input
* Save form data to the database
* Display form errors and success messages in templates

---

## **1. Recap**

* Models, migrations, and relationships
* Admin panel usage
* Displaying database content in templates
* ORM queries

---

## **2. Forms Overview**

* `forms.Form` → standalone form
* `forms.ModelForm` → linked to a model and saves data automatically
* Forms provide validation, security, and integration with templates and views

---

## **3. Example: Contact Form**

```python
# core/forms.py
from django import forms

class ContactForm(forms.Form):
    name = forms.CharField(max_length=100)
    email = forms.EmailField()
    message = forms.CharField(widget=forms.Textarea)
```

---

## **4. Handling Forms in Views**

```python
# core/views.py
from django.shortcuts import render
from .forms import ContactForm

def contact_view(request):
    if request.method == 'POST':
        form = ContactForm(request.POST)
        if form.is_valid():
            name = form.cleaned_data['name']
            email = form.cleaned_data['email']
            message = form.cleaned_data['message']
            # Process form data
    else:
        form = ContactForm()
    return render(request, 'core/contact.html', {'form': form})
```

---

## **5. Template Example**

```html
<h1>Contact Us</h1>
<form method="POST">
    {% csrf_token %}
    {{ form.as_p }}
    <button type="submit">Send</button>
</form>
```

* `{% csrf_token %}` is required for POST forms
* `{{ form.as_p }}` renders fields as paragraphs

---

## **6. ModelForm Example**

```python
# core/forms.py
from django.forms import ModelForm
from .models import Post

class PostForm(ModelForm):
    class Meta:
        model = Post
        fields = ['title', 'content']
```

* Automatically maps form fields to model fields
* Use `form.save()` to save data to the database

---

## **7. Handling ModelForm in Views**

```python
# core/views.py
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

---

## **8. Form Validation**

* Built-in validation: required fields, max length, email format
* Custom validation example:

```python
def clean_title(self):
    data = self.cleaned_data['title']
    if "django" not in data.lower():
        raise forms.ValidationError("Title must contain 'django'.")
    return data
```

* Display errors in templates:

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

---

## **9. POST vs GET**

| Method | Use Case      | Security                  |
| ------ | ------------- | ------------------------- |
| GET    | Retrieve data | Data visible in URL       |
| POST   | Submit data   | Data sent in request body |

* Forms that modify data should use POST

---

## **10. Lab Exercise: Create a Post Submission Form**

**Steps:**

1. Create `PostForm` as a `ModelForm`
2. Create `create_post` view to handle GET/POST
3. Create `create_post.html` template
4. Validate user input
5. Save valid data to database
6. Redirect to post list

**Stretch Goals:**

* Add custom validation
* Display error messages
* Style the form with CSS

**URL Example:**

```python
# core/urls.py
path('create/', create_post, name='create_post')
```

---

## **11. Checkpoints**

* Form created (`forms.Form` or `ModelForm`)
* POST requests handled correctly
* Validation works and errors displayed
* Data saved in database
* Redirection after successful submission

---

## **12. Resources**

* [Django Forms Documentation](https://docs.djangoproject.com/en/stable/topics/forms/)
* [ModelForm Documentation](https://docs.djangoproject.com/en/stable/topics/forms/modelforms/)
* [Form Validation](https://docs.djangoproject.com/en/stable/ref/forms/validation/)

---

# **🎉 Day 3 Complete**

Learners can now handle user input safely, validate forms, and save data using Django forms and ModelForms.

---

