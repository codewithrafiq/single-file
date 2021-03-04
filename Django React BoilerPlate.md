# Django React BoilerPlate
---

# [CodeWithRafiq](https://www.youtube.com/c/CodeWithRafiq/)

---
## Reactjs

---

---

```javascript
npx create-react-app .
npm i axios
npm i js-cookie
npm i react-router-dom
npm run start
npm run build
```

### Create src/env.js

```javascript
import Cookies from "js-cookie";

export const domain = "http://127.0.0.1:8000";
// export const domain = "";

/*
    window.localStorage.setItem('myCat', 'Tom');
    window.localStorage.removeItem('myCat');
    window.localStorage.clear();
    window.localStorage.getItem("token");
    */
const token = "";
const csrftoken = Cookies.get("csrftoken");
export const getheader = {
  Authorization: `token ${token}`,
};

export const postheader = {
  "X-CSRFToken": csrftoken,
};

export const posttokenheader = {
  Authorization: `token ${token}`,
  "X-CSRFToken": csrftoken,
};
```

# Django

---

---

```python
python -m venv venv
source venv/Scripts/activate

python -m pip install --upgrade pip
pip install autopep8

pip install django
pip install djangorestframework
pip install django-cors-headers
pip install Pillow

django-admin startproject main .
```

### Edit Django Setting.py file

```python
# Import
from pathlib import Path
import os

# INSTALLED_APPS
'rest_framework',
'rest_framework.authtoken',
'corsheaders',

# MIDDLEWARE
'corsheaders.middleware.CorsMiddleware',

 # TEMPLATES
'DIRS': [os.path.join(BASE_DIR, 'build')],

# Static files (CSS, JavaScript, Images)
STATIC_URL = '/static/'
MEDIA_URL = '/media/'
STATICFILES_DIRS = [os.path.join(BASE_DIR, 'build/','static')]
STATIC_ROOT = os.path.join(BASE_DIR,'build/', 'staticroot/')
MEDIA_ROOT = os.path.join(BASE_DIR, 'media')



CORS_ORIGIN_WHITELIST = (
    'http://localhost:3000',
)
CORS_ALLOWED_ORIGINS = [
    'http://localhost:3000',
]
CORS_URLS_REGEX = r'^/api.*'
```

### Edit Django urls.py file

```python
from django.contrib import admin
from django.urls import path, include, re_path
from django.views.generic import TemplateView
from rest_framework.authtoken.views import obtain_auth_token
from django.conf import settings
from django.conf.urls.static import static


urlpatterns = [
    path('admin/', admin.site.urls),
]

if settings.DEBUG:
    urlpatterns += static(settings.MEDIA_URL,
                          document_root=settings.MEDIA_ROOT)
    urlpatterns += static(settings.STATIC_URL,
                          document_root=settings.STATIC_ROOT)
    urlpatterns += [
        re_path(r'^.*', TemplateView.as_view(template_name='index.html')),
    ]

if not settings.DEBUG:
    urlpatterns += [
        re_path(r'^.*', TemplateView.as_view(template_name='index.html')),
    ]
```

# Run Server

```
python manage.py runserver
http://127.0.0.1:8000/
```
