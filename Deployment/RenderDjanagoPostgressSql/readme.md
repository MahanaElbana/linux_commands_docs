
<h1 align="center"> How to Deploy django project on Render (Cloud server) 🌩️</h1>

## 🚀 Content
  
 - 💙 python(Django) 
 - 💙 Gunicorn
 - 💙 Render(ubuntu)
 - 💙 Nginx

<p align="center">
  <code><img height="48" src="../../pictures/python.png"      /></code>
  <code><img height="48" src="../../pictures/django.png"      /></code>
  <code><img height="48" src="../../pictures/gunicorn.png"    /></code>
  <code><img height="48" src="../../pictures/Render-cloud.png"/></code>
  <code><img height="48" src="../../pictures/ubuntu.png"      /></code> 
  <code><img height="48" src="../../pictures/nginx.png"       /></code> 
</p>

## 

  - project 
     - urls.py 
        ```python
        from django.contrib.staticfiles.urls import staticfiles_urlpatterns

        urlpatterns+=staticfiles_urlpatterns()
        ``` 
  - pip install dj-database-url 
  - project 
     - settings.py 
       ```python
        import dj_database_url

        DATABASES = {
              'default': dj_database_url.parse(os.environ.get("DATABASE_URL"))
              }
       ```
  - export *write the external database url*  
  - python manage.py migrate
  - python manage.py collectstatic   
  - pip install gunicorn
  - pip install psycopg2-binary
  - in the render site add the following commands
     - PYTHON_VERSION  = python --version
     - DATATBASE_URL = Internal datatbase_url
  - gunicorn project.wsgi:application