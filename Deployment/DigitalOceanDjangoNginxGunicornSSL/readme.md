
<h1 align="center"> How to deploy your Django application on DigitalOcean for production or release mode</h1>

## 🚀 Content
  
 - 💙 python(Django) 
 - 💙 Gunicorn
 - 💙 DigitalOcean(ubuntu)
 - 💙 Nginx

<p align="center">
  <code><img height="48" src="../../pictures/python.png"      /></code>
  <code><img height="48" src="../../pictures/django.png"      /></code>
  <code><img height="48" src="../../pictures/gunicorn.png"    /></code>
  <code><img height="48" src="../../pictures/digitalocean.png"/></code>
  <code><img height="48" src="../../pictures/ubuntu.png"      /></code> 
  <code><img height="48" src="../../pictures/nginx.png"       /></code> 
</p>

## What is the first step 🧐 ?

  - Enter to the DigitalOcean Ubuntu machine ☄️
    
    ```
    ssh root@ip_address
    ```
  - Install and update package ☄️ 

    - **(update ubuntu) && (upgrade ubuntu) && (python3.10) && (pip) && (virtualenv)**
      ```
      sudo apt update 
      sudo apt upgrade 
      suddo apt install python3.10
      sudo apt-get install python3-pip
      pip3 install virtualenv
      python3 -m pip install --upgrade pip
      ```
## What is the second step 🧐 ?

  - Upload your **django project** on **your github** ☄️ 

  - Create a directory ```/home/project``` on DigitalOcean Ubuntu machine ☄️ 
    - To pull your **django project** from github
    - To Create **virtualenv**
    - active virtualenv 
    - enter to django project in the path of **requirements.txt**
    - install python packages 


    ```
    root@ubuntu-platrain-v2:~# cd /home
    root@ubuntu-platrain-v2:/home# mkdir project
    root@ubuntu-platrain-v2:/home# cd project 
    root@ubuntu-platrain-v2:/home/project# git pull your_django_repository_name
    root@ubuntu-platrain-v2:/home/project# virtualenv env 
    root@ubuntu-platrain-v2:/home/project# ls
    platrain-v2   env
    root@ubuntu-platrain-v2:/home/project# source env/bin/activate
    (env) root@ubuntu-platrain-v2:/home/project# cd platrain-v2
    (env) root@ubuntu-platrain-v2:/home/project/platrain-v2# ls
     about       db.sqlite3  manage.py  project    requirements.txt  studyclass
     accounts    Dockerfile  media      quizv4     settings          templates
     assignment  emptyhall   presence   README.md  static            usermanager
    (env) root@ubuntu-platrain-v2:/home/project/platrain-v2# pip install -r requirements.txt
    ```
  - if ```gunicorn``` is not exist in ```requirements.txt``` 
    ```
    pip install gunicorn
    ```
    ```
    (env) root@ubuntu-platrain-v2:/home/project/platrain-v2# pip install gunicorn
    ```
## What is the third step 🧐 ?
  
  -  Once you set up a new Machine on **Digital Ocean** add 👇 
     ```
     sudo ufw enable 
     sudo ufw allow ssh && sudo ufw allow 80 && sudo allow 443
     sudo ufw allow OpenSSH
     sudo ufw allow 20
     sudo ufw status
     sudo ufw disable
     ```

## Test on first ,second && third steps 🧐 ?
   - Determine whether or not packages exist . 
     ```
     pip --version && python3 --version  && virtualenv --version
     ``` 
     ```
     root@ubuntu-platrain-v2:~# pip --version && python3 --version  && virtualenv --version 
     pip 22.0.2 from /usr/lib/python3/dist-packages/pip (python 3.10)
     Python 3.10.6
     virtualenv 20.13.0+ds from /usr/lib/python3/dist-packages/virtualenv/__init__.py
     ```
   - Test runing django project status 
     
     ```
     root@ubuntu-platrain-v2:~# cd /home/project
     root@ubuntu-platrain-v2:/home/project# source env/bin/activate
     (env) root@ubuntu-platrain-v2:/home/project# cd platrain-v2
     (env) root@ubuntu-platrain-v2:/home/project/platrain-v2# gunicorn -b 0.0.0.0:80 project.wsgi
     ``` 
   - eventually , deactivate virtual environment **env**  

   - **(Django project Structure)** ☄️ 
  
      ```
      root@ubuntu-platrain-v2:/home/project#
         - env
         - platrain-v2 
            - project
              - settings.py
            - about
            - db.sqlite3  
            - manage.py  
            - requirements.txt  
            - studyclass
            - accounts    
            - Dockerfile  
            - media  
            - static                 
            - quizv4     
            - settings          
            - templates
            - assignment  
            - emptyhall   
            - presence   
            - README.md  
            - usermanager
      ```
      ```
      root@ubuntu-platrain-v2:~# cd /home/project
      root@ubuntu-platrain-v2:/home/project# ls
      platrain-v2   env
      ```

## What is the fourth step 🧐 ?

<h3 align="center">First step</h3> 

 - DigitalOcean Ubuntu has ```www-data```
 - Create group on linux ```www-data``` if is not exist 
 
   ``` 
   groupadd [OPTIONS] GROUPNAME 
   ```
   ```
   sudo groupadd www-data
   ```

 - Change the user and/or group ownership of a given file, directory, or symbolic link.     
   
   ```
   sudo chown mahney:www-data /home/project/platrain-v2/
   ```

<h3 align="center">Second step</h3> 

 - Create a Gunicorn systemd Socket File (*gunicorn.socket*)

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
<h3 align="center">Third step</h3> 

 - Create a Gunicorn systemd Service File (*gunicorn.service*)
   
   ```
   sudo nano /etc/systemd/system/gunicorn.service
   ```

   ```
   [Unit]
   Description=gunicorn daemon
   Requires=gunicorn.socket
   After=network.target
   [Service]
   User=root
   Group=www-data
   WorkingDirectory=/home/project/platrain-v2
   ExecStart=/home/project/env/bin/gunicorn \
             --access-logfile - \
             --workers 3 \
             --bind unix:/run/gunicorn.sock \
             project.wsgi:application
   [Install]
   WantedBy=multi-user.target
   ```
<h3 align="center">Fourth step</h3> 

- start gunicorn and enable service 
   ```
   sudo systemctl start gunicorn
   sudo systemctl enable gunicorn
   sudo systemctl status gunicorn.socket
   ```
<h3 align="center">Fifth step</h3> 
  
- check for the existence of the **gunicorn.sock** file within the **/run** directory
  ```
  file /run/gunicorn.sock
  ```
  
  ```output
  /run/gunicorn.sock: socket
  ```

<h3 align="center">Sixth step</h3> 

- this step is used if you make update on your project and you want to reload a server , to reach to new update

  ```
  systemctl daemon-reload
  sudo systemctl start gunicorn
  sudo nano gunicorn.service
  ```

## What is the Fifth step 🧐 ?  
 
 - The configuration for Nginx  
 - Nginx configyration in the following path 

   ```
   /etc/nginx/sites-available/default
   ```
   
   ```
   server {
       
       listen       80;
       listen  [::]:80;
       server_name  localhost;
   
       location = /favicon.ico { access_log off; log_not_found off; }
       
       location /static/ {
           autoindex on;
           alias /home/project/platrain-v2/static/;
       }
   
       location /media/ {
           autoindex on;
           alias /home/project/platrain-v2/media/;
       }
   
     
       location / {
           include proxy_params;
           proxy_pass http://unix:/run/gunicorn.sock ;
           proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
           proxy_set_header Host $host;
           proxy_redirect off;
       }
   
   ```

## What is the sixth step 🧐 ?  
  
  - Django settings file 👇
  
  - Commands to enter **settings.py** and activate environment 👇 
    ```
    root@ubuntu-platrain-v2:~#  cd /home/project/ && sourec /env/bin/activate  
    (env) root@ubuntu-platrain-v2:/home/project#  cd platrain-v2
    (env) root@ubuntu-platrain-v2:/home/project/platrain-v2#  sudo nano project/settings.py
    ```
  - In the path : **/home/project/platrain-v2/project/settings.py** add 👇
    ```python

    # add the allowed hosts for example ['*' ,'www.platrain.online' , 'platrain.online'] 
    ALLOWED_HOSTS = ['*' , "IPOrDomainNmae"]
    
    # Static file should be in the same method 
    STATIC_URL = '/static/'
    STATIC_ROOT = os.path.join(BASE_DIR, 'static')


    # Media  file should be in the same method  
    MEDIA_URL = "/media/"
    MEDIA_ROOT = os.path.join(BASE_DIR, 'media')

    # The following settings should be exist for cross origin error
    # CSRF TRUSTED ORIGINS = ['*' , 'https://*.platrain.online']
    CSRF_TRUSTED_ORIGINS = ['*','https://*.IpOrDomainName']
    SECURE_CROSS_ORIGIN_OPENER_POLICY = ['IpOrDomainName','*']
    ```
  - Collect static files , run the following commands 👇
    
    ```
    python manage.py collectstatic
    ```
    ```
    (env) root@ubuntu-platrain-v2:/home/project/platrain-v2# python manage.py collectstatic
    ```  
  - Reload gunicorn server to read new update 👇  

    ```
    sudo systemctl restart gunicorn
    sudo systemctl status gunicorn 
    ```

  - The content of **/home/project/platrain-v2/project/settings.py**

    ```python
    # imports package
    from pathlib import Path
    import os
    
    BASE_DIR = Path(__file__).resolve().parent.parent
    
    # security key and Debug 
    SECRET_KEY = "Password"
    DEBUG = False
    
    
    ALLOWED_HOSTS = ['*' , "IPOrDomainNmae"]
    
    X_FRAME_OPTIONS = 'SAMEORIGIN'
    
    # Application definition
    
    INSTALLED_APPS = [
        
       'installed app added here'
    ]
    
    AUTH_USER_MODEL ='accounts.User'
    MIDDLEWARE = [
       'middleware is added here'
    ]
    
    
    
    ROOT_URLCONF = 'project.urls'
    
    TEMPLATES = [
        {
            'BACKEND': 'django.template.backends.django.DjangoTemplates',
            'DIRS': [BASE_DIR/'templates'],
            'APP_DIRS': True,
            'OPTIONS': {
                'context_processors': [
                    'django.template.context_processors.debug',
                    'django.template.context_processors.request',
                    'django.contrib.auth.context_processors.auth',
                    'django.contrib.messages.context_processors.messages',
                ],
            },
        },
    ]
    
    WSGI_APPLICATION = 'project.wsgi.application'
    
    
    
    # DATABASES = {
    #     'default': {
    #         'ENGINE': 'django.db.backends.mysql',
    #         'NAME': 'platrain',
    #         'USER': 'platrain',
    #         'PASSWORD': 'withALLAH',
    #         'HOST': '127.0.0.1',
    #         'PORT': '',
    #     }
    # }
    
    DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.sqlite3',
            'NAME': BASE_DIR / 'db.sqlite3',
        }
    }
    
    
    AUTH_PASSWORD_VALIDATORS = [
        {
            'NAME': 'django.contrib.auth.password_validation.UserAttributeSimilarityValidator',
        },
        {
            'NAME': 'django.contrib.auth.password_validation.MinimumLengthValidator',
        },
        {
            'NAME': 'django.contrib.auth.password_validation.CommonPasswordValidator',
        },
        {
            'NAME': 'django.contrib.auth.password_validation.NumericPasswordValidator',
        },
    ]
    
    
    LANGUAGE_CODE = 'en-us'
    
    
    TIME_ZONE = 'Africa/Cairo'
    
    USE_I18N = True
    
    USE_TZ = True
    
    
    # Static file should be in the same method 
    STATIC_URL = '/static/'
    STATIC_ROOT = os.path.join(BASE_DIR, 'static')
    
    
    # Media  file should be in the same method  
    MEDIA_URL = "/media/"
    MEDIA_ROOT = os.path.join(BASE_DIR, 'media')
    
    
    DEFAULT_AUTO_FIELD = 'django.db.models.BigAutoField'
    
    # django crispy forms
    CRISPY_ALLOWED_TEMPLATE_PACKS = "bootstrap5"
    CRISPY_TEMPLATE_PACK = "bootstrap5"
    
    
    # SMTP Configuration
    EMAIL_BACKEND = 'django.core.mail.backends.smtp.EmailBackend'
    EMAIL_HOST = 'smtp.gmail.com'
    EMAIL_PORT = 587
    EMAIL_USE_TLS = True
    EMAIL_HOST_USER = 'host user'
    EMAIL_HOST_PASSWORD = 'password fro google settings'
    
    # The following settings should be exist for cross origin error
    CSRF_TRUSTED_ORIGINS = ['*','https://*.IpOrDomainName']
    SECURE_CROSS_ORIGIN_OPENER_POLICY = ['IpOrDomainName','*']
    ```

## What is the seventh step 🧐 ?  

  -  DigitalOcean **Nginx settings SSL** with **Django Project**

   - Your Django project path : ```/home/project/platrain-v2``` ☄️

      ```
      root@ubuntu-platrain-v2:~# cd /home/project
      root@ubuntu-platrain-v2:/home/project# ls
      env  platrain-v2
      ```

   - path of Nginx configuration file : ```/etc/nginx/sites-available/default``` ☄️
   
   - After accessing to your DigitalOcean machine (**ubuntu-platrain-v2**) ☄️
       - enter to ```/etc/nginx/sites-available/default``` 
         ```
         root@ubuntu-platrain-v2:/etc/nginx/sites-available# sudo nano default  
         ```  
       - write the following configurations 
         
         ```conf
       
         server { 
                
	          # listen 80 default_server;
	          # listen [::]:80 default_server;
         
              #########   configuration By : Mahney Elbana  #################
              server_name www.platrain.online platrain.online 143.110.168.90 ;
             
              location = /favicon.ico { access_log off; log_not_found off; }

               location /static/ {
                 autoindex on;
                 alias /home/project/platrain-v2/static/;
               }

               location /media/ {
                   autoindex on;
                   alias /home/project/platrain-v2/media/;
               }

               location / {
                  #include proxy_params;
                  proxy_pass http://unix:/run/gunicorn.sock ;
                  # proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                  # proxy_set_header Host $host;
                  # proxy_redirect off;
                }

               ###############   configuration By : Mahney Elbana  #################

               # SSL configuration

	           # listen 443 ssl default_server;
	           # listen [::]:443 ssl default_server;
	           #
	           # Note: You should disable gzip for SSL traffic.
	           # See: https://bugs.debian.org/773332
	           #
	           # Read up on ssl_ciphers to ensure a secure configuration.
	           # See: https://bugs.debian.org/765782
	           #
	           # Self signed certs generated by the ssl-cert package
	           # Don't use them in a production server!
	           #
	           # include snippets/snakeoil.conf;

	           root /var/www/html;

	           # Add index.php to the list if you are using PHP
	           index index.html index.htm index.nginx-debian.html;

	           server_name _;

               #	location / {
               #		# First attempt to serve request as file, then
               #		# as directory, then fall back to displaying a 404.
               #		try_files $uri $uri/ =404;
               #	}

	           # pass PHP scripts to FastCGI server
	           #
	           #location ~ \.php$ {
	           #	include snippets/fastcgi-php.conf;
	           #
	           #	# With php-fpm (or other unix sockets):
	           #	fastcgi_pass unix:/run/php/php7.4-fpm.sock;
	           #	# With php-cgi (or other tcp sockets):
	           #	fastcgi_pass 127.0.0.1:9000;
	           #}

	           # deny access to .htaccess files, if Apache's document root
	           # concurs with nginx's one
	           #
	           #location ~ /\.ht {
	           #	deny all;
	           #}

               # Managed By :Certbot 
               listen [::]:443 ssl ipv6only=on; # managed by Certbot
               listen 443 ssl; # managed by Certbot
               ssl_certificate /etc/letsencrypt/live/www.platrain.online/fullchain.pem; # managed by Certbot
               ssl_certificate_key /etc/letsencrypt/live/www.platrain.online/privkey.pem; # managed by Certbot
               include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot
               ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem; # managed by Certbot


          }
            

              # Virtual Host configuration for example.com
              #
              # You can move that to a different file under sites-available/ and symlink that
              # to sites-enabled/ to enable it.
              #
              #server {
              #	listen 80;
              #	listen [::]:80;
              #
              #	server_name example.com;
              #
              #	root /var/www/example.com;
              #	index index.html;
              #
              #	location / {
              #		try_files $uri $uri/ =404;
              #	}
              #}
              
              server {
                  if ($host = platrain.online) {
                      return 301 https://$host$request_uri;
                  } # managed by Certbot
              
              
                  if ($host = www.platrain.online) {
                      return 301 https://$host$request_uri;
                  } # managed by Certbot
              
                    
                           listen       80 default_server;
                           listen  [::]:80 default_server;
                           server_name www.platrain.online platrain.online 143.110.168.90 ;
              
              	server_name _;
                  return 404; # managed by Certbot
              
              
             }

         ```

   - How to add ssl to your website ☄️
     ```
     root@ubuntu-platrain-v2:~# sudo apt install certbot python3-certbot-nginx
     root@ubuntu-platrain-v2:~# sudo ufw allow 'Nginx Full'
     root@ubuntu-platrain-v2:~# sudo ufw delete allow 'Nginx HTTP'
     root@ubuntu-platrain-v2:~# sudo certbot --nginx -d www.platrain.online -d platrain.online
     ``` 
   - The result from the : ``` sudo certbot --nginx -d www.platrain.online -d platrain.online ``` && action ☄️
     
     ```
     Saving debug log to /var/log/letsencrypt/letsencrypt.log
     Enter email address (used for urgent renewal and security notices)
      (Enter 'c' to cancel): cbmbbmj@gmail.com
     
     - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
     Please read the Terms of Service at
     https://letsencrypt.org/documents/LE-SA-v1.3-September-21-2022.pdf. You must
     agree in order to register with the ACME server. Do you agree?
     - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
     (Y)es/(N)o: y
     
     - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
     Would you be willing, once your first certificate is successfully issued, to
     share your email address with the Electronic Frontier Foundation, a founding
     partner of the Let's Encrypt project and the non-profit organization that
     develops Certbot? We'd like to send you email about our work encrypting the web,
     EFF news, campaigns, and ways to support digital freedom.
     - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
     (Y)es/(N)o: n
     Account registered.
     Requesting a certificate for www.platrain.online and platrain.online
     
     Successfully received certificate.
     Certificate is saved at: /etc/letsencrypt/live/www.platrain.online/fullchain.pem
     Key is saved at:         /etc/letsencrypt/live/www.platrain.online/privkey.pem
     This certificate expires on 2023-03-13.
     These files will be updated when the certificate renews.
     Certbot has set up a scheduled task to automatically renew this certificate in the background.
     
     Deploying certificate
     Successfully deployed certificate for www.platrain.online to /etc/nginx/sites-enabled/default
     Successfully deployed certificate for platrain.online to /etc/nginx/sites-enabled/default
     Congratulations! You have successfully enabled HTTPS on https://www.platrain.online and https://platrain.online
     
     - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
     If you like Certbot, please consider supporting our work by:
      * Donating to ISRG / Let's Encrypt:   https://letsencrypt.org/donate
      * Donating to EFF:                    https://eff.org/donate-le
     - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
     
     ```


   - All NGINX DIGITALOCEAN COMMANDS STEP BY STEP ☄️
     ```
     sudo nano /etc/nginx/sites-available/default
     ```
     ```
     #########   configuration By : Mahney Elbana  #################
              server_name www.platrain.online platrain.online 143.110.168.90 ;
             
              location = /favicon.ico { access_log off; log_not_found off; }

               location /static/ {
                 autoindex on;
                 alias /home/project/platrain-v2/static/;
               }

               location /media/ {
                   autoindex on;
                   alias /home/project/platrain-v2/media/;
               }

               location / {
                  #include proxy_params;
                  proxy_pass http://unix:/run/gunicorn.sock ;
                  # proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                  # proxy_set_header Host $host;
                  # proxy_redirect off;
                }

               # location ~* \.(css|js|jpg)$ {
               #    access_log off;
               #    add_header Cache-Control public;
               #    add_header Pragma public;
               #    add_header Vary Accept-Encoding;
               #    expires 1M;
               #  }

     ###############   configuration By : Mahney Elbana  #################
     ```
     ```
     sudo apt install certbot python3-certbot-nginx
     sudo ufw allow 'Nginx Full'
     sudo ufw delete allow 'Nginx HTTP'
     sudo certbot --nginx -d www.platrain.online -d platrain.online
     ```


# ALL BASH COMMANDS 💻
 
  ```
  ssh root@ip_address
  sudo apt update 
  sudo apt upgrade 
  suddo apt install python3.10
  sudo apt-get install python3-pip
  pip3 install virtualenv
  python3 -m pip install --upgrade pip
  cd /home
  mkdir project
  cd project 
  git pull your_django_repository_name
  virtualenv env 
  ls
  source env/bin/activate
  platrain-v2
  pip install -r requirements.txt
  pip install gunicorn
  pip install gunicorn
  sudo ufw enable 
  sudo ufw allow ssh && sudo ufw allow 80 && sudo allow 443
  sudo ufw allow OpenSSH
  sudo ufw allow 20
  sudo ufw status
  sudo ufw disable
  pip --version && python3 --version  && virtualenv --version
  gunicorn -b 0.0.0.0:80 project.wsgi
  sudo nano /etc/systemd/system/gunicorn.socket
  sudo nano /etc/systemd/system/gunicorn.service
  systemctl daemon-reload
  sudo systemctl start gunicorn
  sudo nano gunicorn.service
  systemctl daemon-reload
  sudo systemctl start gunicorn
  sudo nano /etc/nginx/sites-available/default
  sudo apt install certbot python3-certbot-nginx
  sudo ufw allow 'Nginx Full'
  sudo ufw delete allow 'Nginx HTTP'
  sudo certbot --nginx -d www.platrain.online -d platrain.online
  ```
# LINKS 🔗

  - [How To Secure Nginx with Let's Encrypt on Ubuntu 20.04](https://www.digitalocean.com/community/tutorials/how-to-secure-nginx-with-let-s-encrypt-on-ubuntu-20-04)
  - [Deploy Django app with Nginx and Gunicorn](https://hiteshmishra708.medium.com/deploy-django-app-with-nginx-and-gunicorn-37916ede7db)
  - [How To Set Up Django with Postgres, Nginx, and Gunicorn on Ubuntu 16.04](https://www.digitalocean.com/community/tutorials/how-to-set-up-django-with-postgres-nginx-and-gunicorn-on-ubuntu-16-04#create-and-configure-a-new-django-project)