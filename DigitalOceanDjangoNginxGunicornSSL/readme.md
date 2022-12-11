
# commands to create project && Deploy on DigitalOcean 🔭

- on server should install python and update ubuntu machine and install pip 
  ```
  sudo apt update 
  sudo apt upgrade 
  suddo apt install python3.10
  sudo apt-get install python3-pip
  ```

- **(Django project Structure)** or **git clone the project from gitHub and create virtual environment**
  
  - create django project 
    
    ```
     DigitalOceanDjangoNginxGunicornSSL
         - venv
         - PlatRain 
            - anyApp
            - project
              - settings.py
    ```
  - ![django project structure](./project_django_structure.png) 




```
cd /media/hardmahney/E_Conclusion/django_gunicorn_example

virtualenv venv

source ./venv/bin/activate

python3 -m pip install --upgrade pip

pip install gunicorn

```
 - copy PlatRain project to */media/hardmahney/E_Conclusion/django_gunicorn_example* then 

```
cd PlatRain/

pip install -r requirements.txt

# gunicorn --bind  0.0.0.0:8888  project.wsgi # for test

cd /media/hardmahney/E_Conclusion/django_gunicorn_example/PlatRain

docker build -t djangogunicorn .

```

 - Run djangogunicorn image 
   
   ```
   docker run --name djpro -itd -p 88:8000 -v /media/hardmahney/E_Conclusion/django_gunicorn_example/PlatRain:/code djangogunicorn
   ```

# Note can be make error for you check that **PlatRain/project/settings.py**   
 - True settings 
```
import os
STATIC_URL = '/static/'
STATIC_ROOT = os.path.join(BASE_DIR, 'static/')

```
 - False settings

```
STATIC_URL = '/static/'
STATICFILES_DIRS = [
   BASE_DIR / "static",

]
```
 - BASE_DIR is equal */media/hardmahney/E_Conclusion/django_gunicorn_example/PlatRain*

# Another notes if settings.py is : 

```
STATIC_URL = '/static/'
STATICFILES_DIRS = [
   BASE_DIR / "static",

]
```
 - convert to : 
```
STATIC_URL = '/static/'

STATIC_ROOT = os.path.join(BASE_DIR, 'static/')

STATICFILES_DIRS = [
   BASE_DIR / "static",

]
```
 - then apply the following command
 
  ```
  python3 manage.py collect static 
  ```
    - to get out static files to become in the root path

# the following command for test 

```
gunicorn -b 0.0.0.0:9898 project.wsgi
```



# how to run  nginx as a revers proxey 🔭

```
docker run --name  cert1 -p 80:80 -itd  -v  /media/hardmahney/E_Conclusion/django_gunicorn_example/PlatRain/static:/opt/services/platrain/static   -v  /media/hardmahney/E_Conclusion/django_gunicorn_example/PlatRain/media:/opt/services/platrain/media mahney/nginx-certbot:v1
```

```
######################################################

# first we declare our upstream server, which is our Gunicorn application
upstream platrain_app {
    # docker will automatically resolve this to the correct address
    # because we use the same name as the service: "djangoapp"
    server 172.17.0.2:8000;
}

#######################################################

server {
    listen       80;
    listen  [::]:80;
    server_name  localhost;



   # update track 
    location / {
        # everything is passed to Gunicorn
        proxy_pass http://platrain_app ;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Host $host;
        proxy_redirect off;
    }



   location /static/ {
        autoindex on;
        alias /opt/services/platrain/static/;
    }


    location /media/ {
        autoindex on;
        alias /opt/services/platrain/media/;
    }


          location ~* \.(css|js|jpg)$ {
            access_log off;
            
            add_header Cache-Control public;
            add_header Pragma public;
            add_header Vary Accept-Encoding;
            expires 1M;
        }
####################################
```

# command to run server django in bacground 

```
nohup gunicorn -b 0.0.0.0:2356 project.wsgi &
nohup python manage.py runserver '0.0.0.0:8000' &

```

---------------------------------------------------------
---------------------------------------------------------
---------------------------------------------------------

# step zero : How to create group on linux
``` 
groupadd [OPTIONS] GROUPNAME 
```
```
sudo groupadd www-data
```
# step zero :  /home/platrainproject/PlatRain
```
 sudo chown mahney:www-data /media/hardmahney/E_Conclusion/django_gunicorn_example/PlatRain/
```
# step one : Create a Gunicorn systemd Socket File (*gunicorn.socket*)

```
sudo nano /etc/systemd/system/gunicorn.socket
```

```gunicorn.socket
[Unit]
Description=gunicorn socket

[Socket]
ListenStream=/run/gunicorn.sock

[Install]
WantedBy=sockets.target
```

# step two : Create a Gunicorn systemd Service File (*gunicorn.service*)

```
sudo nano /etc/systemd/system/gunicorn.service
```

```
[Unit]
Description=gunicorn daemon
Requires=gunicorn.socket
After=network.target
[Service]
User=mahney
Group=www-data
WorkingDirectory=/media/hardmahney/E_Conclusion/django_gunicorn_example/PlatRain
ExecStart=/media/hardmahney/E_Conclusion/django_gunicorn_example/venv/bin/gunicorn \
          --access-logfile - \
          --workers 3 \
          --bind unix:/run/gunicorn.sock \
          project.wsgi:application
[Install]
WantedBy=multi-user.target
```

# Step three  

```
sudo systemctl start gunicorn
sudo systemctl enable gunicorn
sudo systemctl status gunicorn.socket
```

# step four : check for the existence of the gunicorn.sock file within the /run directory:
```
file /run/gunicorn.sock
```

```output
/run/gunicorn.sock: socket
```

# step five  nginx

```


server {
    listen       80;
    listen  [::]:80;
    server_name  localhost;

    location = /favicon.ico { access_log off; log_not_found off; }
    
    location /static/ {
        autoindex on;
        alias /media/hardmahney/E_Conclusion/django_gunicorn_example/PlatRain/static/;
    }

    location /media/ {
        autoindex on;
        alias /media/hardmahney/E_Conclusion/django_gunicorn_example/PlatRain/media/;
    }

  
    location / {
        include proxy_params;
        proxy_pass http://unix:/run/gunicorn.sock ;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Host $host;
        proxy_redirect off;
    }


     location ~* \.(css|js|jpg)$ {
        access_log off;
            
        add_header Cache-Control public;
        add_header Pragma public;
        add_header Vary Accept-Encoding;
        expires 1M;
        }

```

# default in *nginx.conf*

# commands you need to use

```
systemctl daemon-reload
sudo systemctl start gunicorn
sudo nano gunicorn.service
```

# url 
[first url](https://hiteshmishra708.medium.com/deploy-django-app-with-nginx-and-gunicorn-37916ede7db)
[second url](https://www.digitalocean.com/community/tutorials/how-to-set-up-django-with-postgres-nginx-and-gunicorn-on-ubuntu-16-04#create-and-configure-a-new-django-project)



---------------digital ocien----------------
ssh root@188.166.73.85
```password
b$GDC&HuCU7zd9n
```

sudo ufw delete allow 80

/home/platrainproject/PlatRain

-------------------------
-------------------------
-------------------------