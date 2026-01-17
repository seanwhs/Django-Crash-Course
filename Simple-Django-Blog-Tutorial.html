<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Expanded Django Blog Tutorial</title>
  <style>
    body { font-family: Arial, sans-serif; line-height: 1.6; margin: 2rem; }
    h1 { border-bottom: 2px solid #444; padding-bottom: 0.3rem; }
    pre { background: #f4f4f4; padding: 1rem; overflow-x: auto; }
    code { font-family: monospace; }
    ul { margin-top: 0; }
  </style>
</head>
<body>
  <h1>Django Blog Tutorial</h1>
  <p>This step-by-step guide walks you through installing Django, creating a blog app, defining models, adding views, templates, static files, and finally deploying the project.</p>

  <h2>1. Install Django</h2>
  <p>==Use pip to install the latest Django release==</p>
  <pre><code>$ pip install django
</code></pre>
  <p>If you already have Python and pip set up, this command fetches the framework and its dependencies.:cite[Page 604d]{ln=3}</p>

  <h2>2. Create a New Project</h2>
  <p>==Scaffold a fresh site named <code>myblog</code>==</p>
  <pre><code>$ django-admin startproject myblog
</code></pre>
  <p>Inside the newly created <code>myblog/</code> folder you’ll find the global <code>settings.py</code> and <code>urls.py</code> files.:cite[Page 604d]{ln=4}</p>

  <h2>3. Run the Built-In Server</h2>
  <p>==Verify the setup by launching the development server==</p>
  <pre><code>$ cd myblog
$ python manage.py runserver
</code></pre>
  <p>Open <code>http://localhost:8000/</code> in your browser; you should see the Django welcome page.:cite[Page 604d]{ln=5}</p>

  <h2>4. Create a New App</h2>
  <p>==Isolate blog functionality inside a dedicated app==</p>
  <pre><code>$ python manage.py startapp blog
</code></pre>
  <p>After this, add <code>&#39;blog&#39;</code> to the <code>INSTALLED_APPS</code> list in <code>settings.py</code> so Django knows about it.:cite[Page 604d]{ln=6}</p>

  <h2>5. Define the <code>Post</code> Model</h2>
  <p>==Map blog posts to database fields==</p>
  <pre><code>from django.db import models

class Post(models.Model):
    # Title of the blog post (max 100 characters)
    title = models.CharField(max_length=100)
    # Main content of the post
    content = models.TextField()
    # Timestamp added automatically at creation
    pub_date = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return self.title
</code></pre>
  <p>Run migrations to create the corresponding table:</p>
  <pre><code>$ python manage.py makemigrations
$ python manage.py migrate
</code></pre>
  <p>Migrations translate your Python model into SQL commands for the database.:cite[Page 6f8e]{ln=1}, :cite[Page 1a0a]{ln=7}</p>

  <h2>6. Register the Model with Admin</h2>
  <p>==Leverage Django&#39;s auto-generated admin panel for CRUD operations==</p>
  <pre><code>$ python manage.py createsuperuser
# Follow prompts for username, email, and password
</code></pre>
  <p>In <code>blog/admin.py</code>, add:</p>
  <pre><code>from django.contrib import admin
from .models import Post

admin.site.register(Post)
</code></pre>
  <p>Navigate to <code>http://localhost:8000/admin/</code>, log in with your superuser, and you can add, edit, or delete posts without writing any extra UI.:cite[Page 604d]{ln=7}</p>

  <h2>7. Create a View and URL Route</h2>
  <p>==Show all posts on the home page==</p>
  <pre><code>from django.shortcuts import render
from .models import Post

def home(request):
    posts = Post.objects.all()
    return render(request, &#39;home.html&#39;, {&#39;posts&#39;: posts})
</code></pre>
  <p>In <code>blog/urls.py</code>:</p>
  <pre><code>from django.urls import path
from . import views

urlpatterns = [
    path(&#39;&#39;, views.home, name=&#39;home&#39;),
]
</code></pre>
  <p>Then include this in the project-level <code>urls.py</code>:</p>
  <pre><code>from django.urls import include, path

urlpatterns = [
    path(&#39;&#39;, include(&#39;blog.urls&#39;)),
    # other routes
]
</code></pre>
  <p>Requests to <code>http://localhost:8000/</code> are now dispatched to the <code>home</code> view.:cite[Page 604d]{ln=8}</p>

  <h2>8. Build the Template</h2>
  <p>==Render posts using Django&#39;s template language==</p>
  <pre><code>{% for post in posts %}
    &lt;h2&gt;{{ post.title }}&lt;/h2&gt;
    &lt;p&gt;{{ post.content }}&lt;/p&gt;
    &lt;small&gt;Published {{ post.pub_date }}&lt;/small&gt;
{% endfor %}
</code></pre>
  <p>Save this as <code>blog/templates/home.html</code>. Ensure <code>TEMPLATES&#39; DIRS</code> in <code>settings.py</code> includes the templates folder so Django can find it.:cite[Page 604d]{ln=9}</p>

  <h2>9. Add Static and Media Files</h2>
  <p>==Serve CSS, JavaScript, and user-uploaded images==</p>
  <pre><code>STATIC_URL = &#39;/static/&#39;
MEDIA_URL = &#39;/media/&#39;
MEDIA_ROOT = BASE_DIR / &#39;media&#39;
</code></pre>
  <p>Place CSS in <code>static/</code> and reference them in templates with:</p>
  <pre><code>{% load static %}
&lt;link rel=&quot;stylesheet&quot; href=&quot;{% static &#39;style.css&#39; %}&quot;&gt;
</code></pre>
  <p>Before deployment, collect all static assets:</p>
  <pre><code>$ python manage.py collectstatic
</code></pre>
  <p>This gathers CSS, JS, and images into a single location for efficient serving.:cite[Page 604d]{ln=10}</p>

  <h2>10. Deploy the Site</h2>
  <p>==Move from local development to production==</p>
  <p>Freeze dependencies:</p>
  <pre><code>$ pip freeze &gt; requirements.txt
</code></pre>
  <p>Adjust <code>DATABASES</code> in <code>settings.py</code> (e.g., switch to PostgreSQL) and follow your chosen host’s Django deployment guide (Heroku, AWS, DigitalOcean, etc.).:cite[Page 604d]{ln=11}</p>

  <h2>Summary</h2>
  <p>By following these ten steps, you now have a fully functional blog application with models, views, templates, styling, and an admin interface. Explore pagination, search, user authentication, or the Django REST Framework to extend functionality.</p>
</body>
</html>
