# What is Soft Link And Hard Link In Linux? 🔭
 
 - **A symbolic or soft link** is an actual link to the original file 🏆
 - whereas **a hard link** is a mirror copy of the original file 🏆 
 - Any change in **the Origin life** affects **the hard or soft link** 🏆
 - Any change in **the hard or soft link** affects **the Origin life** 🏆
 
 - the difference betwwen *soft and hard link* 🏆

   - **A symbolic or soft link** 🔦
      - If you delete the original file, the soft link has no value, because it points to a non-existent file.
   
   - **hard link** 🔦
      - But in the case of **hard link**, it is entirely opposite. 
      - Even if you delete the original file, the hard link will still has the data of the original file.
      - Because hard link acts as a mirror copy of the original file.

 - <H2 align="center"> 🔦 Part 1 : Soft Link 🔦 </H2> 
 
 - How to create a soft link ☄️ 
   ```
   ln -s origin_file_path  linked_file_path_name
   ```  
 - How to create a soft link on an existing file (overwrite) ☄️
   ```
   ln -sf origin_file_path  linked_file_path_name
   ```  
 - <H2 align="center"> 🔦 Part 2 : Hard Link 🔦 </H2> 
 
 - How to create a Hard link ☄️  
   ```
   ln  origin_file_path  linked_file_path_name
   ```
-------------
-------------
-------------

# Firewall with **UFW** *Uncomplicated Firewall* on Ubuntu 🔭

   - **Defination** : **ufw** is The default firewall configuration tool for Ubuntu .

   - <H2 align="center"> 🔦 Part 1 : enable ufw 🔦 </H2>  
     
     
     ```
     sudo ufw enable
     
     ```
    
   - <H2 align="center"> 🔦 Part 2 : add rule to firewall 🔦 </H2>   

     ```
     sudo ufw allow 22 && sudo ufw allow 80 && sudo ufw allow 8000
     sudo ufw allow 443
     sudo ufw allow http
     sudo ufw allow https
     sudo ufw delete allow 80
     ```

   - <H2 align="center"> 🔦 Part 3 : allow rule  🔦 </H2>  

   - How to enable **(https)** = **port(443)**  ☄️
     ```
     sudo ufw allow https
     sudo ufw allow 443
     ``` 
   - How to enable **(http)** = **port(80)**  ☄️
     ```
     sudo ufw allow http
     sudo ufw allow 80
     ```   
   - How to enable **(ssh)**  ☄️
     ```
     sudo ufw allow ssh
     ```  
   - How to enable **port(22)**  ☄️
     ```
     sudo ufw allow 22
     ```  
   -  <H2 align="center"> 🔦 Part 4 : Deleting a Rule 🔦 </H2>       
        
   - How to delete **port(22)** ☄️
     ```
     sudo ufw delete allow 22/tcp
     ``` 
   - How to delete **https** = **port(443)** ☄️
     ```
     sudo ufw delete allow https
     sudo ufw delete allow 443

     ```      
   - How to delete **http** **port(80)** ☄️
     ```
     sudo ufw delete allow http
     sudo ufw delete allow 80
     ``` 
   -  <H2 align="center"> 🔦 Part 5 : disable ufw  🔦 </H2>
      ```
      sudo ufw disable
      ```    
   -  <H2 align="center"> 🔦 Note for DigitalOcean 🔦 </H2>

   - important steps to can access on your server again ☄️

      -  Once you set up a new Machine on **Digital Ocean** add 👇 
         ```
         sudo ufw enable 
         sudo ufw allow ssh && sudo ufw allow 80 && sudo allow 443
         sudo ufw allow OpenSSH
         sudo ufw allow 20
         sudo ufw status
         sudo ufw disable
         ```  
      - Don't forget to disable **ufw**  ⚠️
   
--------------
--------------
--------------
# commands to create project 🔭

 - first step execute the following commands 

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

# SSH : *Secure Shell* 💎

 - The *Secure Shell Protocol (SSH)* 
 - is a cryptographic network protocol .
 - for operating network services securely over an unsecured network .
 - to access on other machine using *password*
     - using the following command 

       ```
       ssh root_machine_name@machine_ip
       ```
     - then enter password 

# ubuntu-platrain-v2 on DigitalOcean 
```ssh
ssh root@143.110.168.90
```
```password
with010*#ALLAH
```

# Firewall with **UFW** *Uncomplicated Firewall* on Ubuntu 🔭

   - **Defination** : **ufw** is The default firewall configuration tool for Ubuntu .

   - <H2 align="center"> 🔦 Part 1 : enable ufw 🔦 </H2>  
     
     ```
     sudo ufw enable
     ```
    
   - <H2 align="center"> 🔦 Part 2 : add rule to firewall 🔦 </H2>   

     ```
     sudo ufw allow 22 && sudo ufw allow 80 && sudo ufw allow 8000
     sudo ufw allow 443
     sudo ufw allow http
     sudo ufw allow https
     sudo ufw delete allow 80
     ```

   - <H2 align="center"> 🔦 Part 3 : allow rule  🔦 </H2>  

   - How to enable **(https)** = **port(443)**  ☄️
     ```
     sudo ufw allow https
     sudo ufw allow 443
     ``` 
   - How to enable **(http)** = **port(80)**  ☄️
     ```
     sudo ufw allow http
     sudo ufw allow 80
     ```   
   - How to enable **(ssh)**  ☄️
     ```
     sudo ufw allow ssh
     ```  
   - How to enable **port(22)**  ☄️
     ```
     sudo ufw allow 22
     ```  
   -  <H2 align="center"> 🔦 Part 4 : Deleting a Rule 🔦 </H2>       
        
   - How to delete **port(22)** ☄️
     ```
     sudo ufw delete allow 22/tcp
     ``` 
   - How to delete **https** = **port(443)** ☄️
     ```
     sudo ufw delete allow https
     sudo ufw delete allow 443

     ```      
   - How to delete **http** **port(80)** ☄️
     ```
     sudo ufw delete allow http
     sudo ufw delete allow 80
     ``` 
   -  <H2 align="center"> 🔦 Part 5 : disable ufw  🔦 </H2>
      ```
      sudo ufw disable
      ```    
   -  <H2 align="center"> 🔦 Note for DigitalOcean 🔦 </H2>

   - important steps to can access on your server again ☄️

      -  Once you set up a new Machine on **Digital Ocean** add 👇 
         ```
         sudo ufw enable 
         sudo ufw allow ssh && sudo ufw allow 80 && sudo allow 443
         sudo ufw allow OpenSSH
         sudo ufw allow 20
         sudo ufw status
         sudo ufw disable
         ```  
      - Don't forget to disable **ufw**  ⚠️
   

-------------
-------------
-------------

# What is Soft Link And Hard Link In Linux? 🔭
 
 - **A symbolic or soft link** is an actual link to the original file 🏆
 - whereas **a hard link** is a mirror copy of the original file 🏆 
 - Any change in **the Origin life** affects **the hard or soft link** 🏆
 - Any change in **the hard or soft link** affects **the Origin life** 🏆
 
 - the difference betwwen *soft and hard link* 🏆

   - **A symbolic or soft link** 🔦
      - If you delete the original file, the soft link has no value, because it points to a non-existent file.
   
   - **hard link** 🔦
      - But in the case of **hard link**, it is entirely opposite. 
      - Even if you delete the original file, the hard link will still has the data of the original file.
      - Because hard link acts as a mirror copy of the original file.

 - <H2 align="center"> 🔦 Part 1 : Soft Link 🔦 </H2> 
 
 - How to create a soft link ☄️ 
   ```
   ln -s origin_file_path  linked_file_path_name
   ```  
 - How to create a soft link on an existing file (overwrite) ☄️
   ```
   ln -sf origin_file_path  linked_file_path_name
   ```  
 - <H2 align="center"> 🔦 Part 2 : Hard Link 🔦 </H2> 
 
 - How to create a Hard link ☄️  
   ```
   ln  origin_file_path  linked_file_path_name
   ```
--------------
--------------
--------------
pkill gunicorn
-------------
-------------
-------------

|type|username|password|
|-|-|-|
|admin|admin|123456admin|
|student|student1|123456studentMG|
|student|student2|123456studentMG|
|student|student3|123456studentMG|
|student|student4|123456studentMG|
|student|student5|123456studentMG|
|student|student6|123456studentMG|
|student|student7|123456studentMG|
|student|student8|123456studentMG|
|student|student9|123456studentMG|
|student|student10|123456studentMG|
|doctor|doctor1|123456doctorMG|
|doctor|doctor2|123456doctorMG|
|doctor|doctor3|123456doctorMG|
|doctor|doctor4|123456doctorMG|
|doctor|doctor5|123456doctorMG|
|doctor|doctor6|123456doctorMG|
|doctor|doctor7|123456doctorMG|
|doctor|doctor8|123456doctorMG|
|doctor|doctor9|123456doctorMG|
|doctor|doctor10|123456doctorMG|


# PlatRain Problems 🔭

pkill gunicorn




