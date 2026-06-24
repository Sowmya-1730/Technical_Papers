# AMA June 24th

## 1. What happens if we keep `*` in `ALLOWED_HOSTS`?

**Answer:**

`ALLOWED_HOSTS` is a Django security setting that specifies which host/domain names the application can serve.

```python
ALLOWED_HOSTS = ["*"]
```

If `*` is used:

- Django accepts requests from any host header.
- It disables host header validation.
- Useful during development and testing.
- Not recommended in production because it can expose the application to Host Header Attacks.

**Best Practice:**

```python
ALLOWED_HOSTS = ["example.com", "www.example.com"]
```


## 2. What happens if apps are not added in `INSTALLED_APPS`?

**Answer:**

If an app is not added to `INSTALLED_APPS`:

- Django will not recognize the app.
- Models from that app will not be included in migrations.
- Admin configurations will not work.
- Templates and static files may not be discovered properly.
- Signals may not be loaded.

Example:

```python
INSTALLED_APPS = [
    "myapp",
]
```

Without adding `myapp`, Django ignores it.



## 3. What is XSS?

**Answer:**

XSS (Cross-Site Scripting) is a web security vulnerability where an attacker injects malicious JavaScript into a webpage.

Example:

```html
<script>alert("Hacked");</script>
```

Types:

1. Stored XSS
2. Reflected XSS
3. DOM-Based XSS

Prevention:

- Escape user input.
- Validate input.
- Use Content Security Policy (CSP).
- Avoid rendering untrusted HTML.



## 4. How do we connect a web service to PostgreSQL?

**Answer:**

A web service connects to PostgreSQL using a database driver or ORM.

Django Example:

Install:

```bash
pip install psycopg2-binary
```

Configure:

```python
DATABASES = {
    "default": {
        "ENGINE": "django.db.backends.postgresql",
        "NAME": "mydb",
        "USER": "postgres",
        "PASSWORD": "password",
        "HOST": "localhost",
        "PORT": "5432",
    }
}
```

Then use Django ORM to perform database operations.


## 5. How do you connect PostgreSQL as a host?

**Answer:**

Specify the PostgreSQL host details in the database configuration.

Example:

```python
DATABASES = {
    "default": {
        "ENGINE": "django.db.backends.postgresql",
        "HOST": "localhost",
        "PORT": "5432",
    }
}
```

For remote databases:

```python
"HOST": "192.168.1.100"
```

or

```python
"HOST": "database.example.com"
```

The application connects using the provided host, port, username, and password.


## 6. Difference between Authentication and Authorization

**Answer:**

| Authentication | Authorization |
|---------------|---------------|
| Verifies who the user is | Determines what the user can access |
| Happens first | Happens after authentication |
| Uses username/password, OTP, etc. | Uses roles and permissions |
| Example: Login | Example: Access Admin Panel |

Example:

- Authentication: Logging into Gmail.
- Authorization: Being allowed to access only your inbox.


## 7. How do you add a table in the Admin Panel?

**Answer:**

Create a model:

```python
class Student(models.Model):
    name = models.CharField(max_length=100)
```

Register it in `admin.py`:

```python
from django.contrib import admin
from .models import Student

admin.site.register(Student)
```

Run migrations and create a superuser.

The model will appear as a table in the Django Admin Panel.

## 8. How do you inherit a template inside another template?

**Answer:**

Django uses template inheritance.

### Base Template

```html
<!-- base.html -->
<html>
<body>
{% block content %}
{% endblock %}
</body>
</html>
```

### Child Template

```html
{% extends "base.html" %}

{% block content %}
<h1>Home Page</h1>
{% endblock %}
```

The child template inherits the structure from the base template.


## 9. Give some template tags

**Answer:**

Common Django Template Tags:

### if

```html
{% if user.is_authenticated %}
    Welcome
{% endif %}
```

### for

```html
{% for item in items %}
    {{ item }}
{% endfor %}
```

### block

```html
{% block content %}
{% endblock %}
```

### extends

```html
{% extends "base.html" %}
```

### include

```html
{% include "navbar.html" %}
```

### csrf_token

```html
<form method="post">
    {% csrf_token %}
</form>
```


## 10. What is the Pillow library?

**Answer:**

Pillow is a Python imaging library used for:

- Opening images
- Editing images
- Resizing images
- Cropping images
- Image format conversion

Install:

```bash
pip install pillow
```

Example:

```python
from PIL import Image

img = Image.open("photo.jpg")
img.resize((200, 200))
```

Django uses Pillow for handling `ImageField` uploads.


## 11. What is the PRG Pattern?

**Answer:**

PRG stands for:

**Post → Redirect → Get**

It is a web development pattern used to prevent duplicate form submissions.

Flow:

1. User submits a form (POST).
2. Server processes the request.
3. Server redirects to another page.
4. Browser makes a GET request.

Example:

```python
def submit_form(request):
    if request.method == "POST":
        # Save data
        return redirect("success")
```

Benefits:

- Prevents duplicate submissions.
- Avoids accidental refresh issues.
- Improves user experience.
