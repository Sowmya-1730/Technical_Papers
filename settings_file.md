# Django Settings and Security Concepts

# 1. What is the Settings File in Django?

The settings file (`settings.py`) is the central configuration file of a Django project.

It contains:

* Database configuration
* Installed applications
* Middleware configuration
* Security settings
* Static files configuration
* Templates configuration
* Secret keys
* Internationalization settings

Example:

```python
# settings.py

DEBUG = True

ALLOWED_HOSTS = []

INSTALLED_APPS = [
    ...
]

MIDDLEWARE = [
    ...
]
```

Think of `settings.py` as the control center of your Django application.



# 2. What is SECRET_KEY?

The `SECRET_KEY` is a unique, random string generated when a Django project is created.

Example:

```python
SECRET_KEY = 'django-insecure-abc123xyz'
```

## Why is it important?

Django uses it for:

* Session security
* Password reset tokens
* CSRF protection
* Cryptographic signing
* Authentication-related operations

## Important Rule

Never expose the SECRET_KEY publicly.

Do not:

* Upload it to GitHub
* Share it with others
* Hardcode production keys in public repositories

In production, store it in environment variables.

Example:

```python
import os

SECRET_KEY = os.getenv("SECRET_KEY")
```



# 3. Default Django Apps

When a new project is created, Django automatically includes several built-in apps.

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
]
```



## django.contrib.admin

Provides the Django Admin Panel.

Features:

* Add data
* Update data
* Delete data
* Manage users

Example:

```
http://127.0.0.1:8000/admin
```


## django.contrib.auth

Handles:

* User registration
* Login
* Logout
* Permissions
* Groups

Example:

```python
from django.contrib.auth.models import User
```

## django.contrib.contenttypes

Tracks relationships between models.

Used internally by Django.

Helps generic relationships work.


## django.contrib.sessions

Stores user session information.

Example:

```python
request.session["username"] = "Sri"
```

Allows data to persist between requests.


## django.contrib.messages

Used for displaying temporary messages.

Example:

```python
messages.success(request, "Login Successful")
```

Output:

```
Login Successful
```


## django.contrib.staticfiles

Manages:

* CSS
* JavaScript
* Images

Example:

```html
<link rel="stylesheet" href="style.css">
```

### Are There More Django Apps?

Yes.

Common built-in apps:

```python
django.contrib.sites
django.contrib.humanize
django.contrib.sitemaps
django.contrib.flatpages
django.contrib.redirects
```

You can also create your own apps:

```bash
python manage.py startapp blog
```


# 4. What is Middleware?

Middleware is software that sits between:

```
Request → Middleware → View
Response ← Middleware ← View
```

It processes requests before they reach views and processes responses before they reach the browser.


## Real Life Example

Airport Security

```
Passenger
    ↓
Security Check
    ↓
Boarding Gate
```

Similarly:

```
User Request
    ↓
Middleware
    ↓
Django View
```

## Default Middleware in Django

```python
MIDDLEWARE = [
    'django.middleware.security.SecurityMiddleware',
    'django.contrib.sessions.middleware.SessionMiddleware',
    'django.middleware.common.CommonMiddleware',
    'django.middleware.csrf.CsrfViewMiddleware',
    'django.contrib.auth.middleware.AuthenticationMiddleware',
    'django.contrib.messages.middleware.MessageMiddleware',
    'django.middleware.clickjacking.XFrameOptionsMiddleware',
]
```

#### SecurityMiddleware

```python
'django.middleware.security.SecurityMiddleware'
```

Purpose:

* Adds security headers
* Forces HTTPS
* Prevents some attacks

Features:

* HTTPS redirect
* HSTS support
* Secure cookies

Protects against:

* Man-in-the-middle attacks
* Insecure HTTP communication


#### SessionMiddleware

```python
'django.contrib.sessions.middleware.SessionMiddleware'
```

Purpose:

Manages user sessions.

Example:

```python
request.session["user_id"] = 101
```

Allows users to stay logged in.


#### CommonMiddleware

```python
'django.middleware.common.CommonMiddleware'
```

Purpose:

Handles common operations such as:

* URL normalization
* APPEND_SLASH
* Content length headers

Example:

```
/about

becomes

/about/
```


#### CSRF Middleware

```python
'django.middleware.csrf.CsrfViewMiddleware'
```

Protects against CSRF attacks.



# 5. What is CSRF?

CSRF = Cross Site Request Forgery

An attacker tricks a logged-in user into performing an action without permission.

Example:

You are logged into your bank account.

Attacker creates:

```html
<form action="bank.com/transfer">
```

If submitted automatically:

```
Money transferred
```

without your knowledge.


## Django Protection

Forms contain:

```html
{% csrf_token %}
```

Django verifies the token before accepting requests.



# 6. What is Clickjacking?

Attacker places your website inside an invisible iframe.

Example:

User thinks:

```
Click Here To Win Prize
```

Actually clicking:

```
Delete Account
```

button hidden underneath.


## Django Protection

Adds header:

```http
X-Frame-Options: DENY
```

Prevents websites from being loaded in iframes.


# 7. What is XSS?

XSS = Cross Site Scripting

An attacker injects malicious JavaScript into a webpage.

Example:

```html
<script>
alert("Hacked")
</script>
```

If executed:

* Cookies can be stolen
* Sessions can be hijacked
* User data can be accessed

## Django Protection Against XSS

Django automatically escapes HTML.

Example:

User enters:

```html
<script>alert('hack')</script>
```

Django displays:

```html
&lt;script&gt;alert('hack')&lt;/script&gt;
```

instead of executing it.



# 8. SQL Injection

Attack:

```sql
' OR 1=1 --
```

can manipulate database queries.

Example:

```sql
SELECT * FROM users
WHERE username=''
OR 1=1
```

returns all users.



## Django Protection

Using ORM:

```python
User.objects.filter(username=name)
```

Django safely escapes input.



# 9. Session Hijacking

Attacker steals session cookies.

Result:

* User impersonation
* Unauthorized access

Protection:

```python
SESSION_COOKIE_SECURE = True
```

Use HTTPS.



# 10. Other Useful Middleware

## LocaleMiddleware

```python
django.middleware.locale.LocaleMiddleware
```

Supports multiple languages.


## GZipMiddleware

```python
django.middleware.gzip.GZipMiddleware
```

Compresses responses.

Benefits:

* Faster websites
* Less bandwidth usage


## ConditionalGetMiddleware

```python
django.middleware.http.ConditionalGetMiddleware
```

Improves browser caching.

Benefits:

* Faster page loads
* Reduced server load


# 11. What is WSGI?

WSGI = Web Server Gateway Interface

It is a standard that allows communication between:

```
Web Server
        ↔
Python Application
```


## Why Do We Need WSGI?

Browsers cannot directly talk to Django.

A web server is needed.

Example:

```
Browser
    ↓
Nginx
    ↓
WSGI
    ↓
Django
```

WSGI acts as a bridge between the web server and Django.


## Django WSGI File

Django creates:

```python
wsgi.py
```

Example:

```python
from django.core.wsgi import get_wsgi_application

application = get_wsgi_application()
```

This file exposes Django to web servers such as:

* Gunicorn
* uWSGI
* Apache
* Nginx


# Request Flow in Django

```
Browser
    ↓
Web Server
    ↓
WSGI
    ↓
Middleware
    ↓
URL Routing
    ↓
View
    ↓
Template
    ↓
Response
```

This is the complete path followed by a request in a Django application.


