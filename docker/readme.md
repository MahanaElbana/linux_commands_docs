
# 1 how to create and run database server using postgresSQL server 🚀
``` 
docker run --name platrain -itd -p 5431:5432 -e POSTGRES_NAME=admin -e POSTGRES_USER=admin -e POSTGRES_PASSWORD=123456 postgres
```
# 2 docker settings🚀 
``` 
ps -ef | grep docker
```
```
 edit /lib/systemd/system/docker.service
```
``` 
ExecStart=/usr/bin/dockerd -H fd:// -H=tcp://0.0.0.0:2389
```
```
systemctl daemon-reload
```
```
sudo service docker restart
```
# 3 to test docker APIs🚀
```cmd
curl "http://0.0.0.0:2389/containers/json"
```
```cmd
 curl "http://0.0.0.0:2389/images/json"  
```
# 4 docker  management🚀  
``` 
docker ps                             
``` 

```
docker ps -a                            
``` 

```
docker start **containe_name**       
``` 

```
docker rm **container_name** --force     
``` 

```
docker inspect **container_name**   
``` 
```
sudo chmod 666 /var/run/docker.sock  
```


``` 

```
# 5 settings of pgadmin **[ password ]** 🚀
master password is added it for the first time 
```
123456
```

# 6 How to install zsh on Pop7  🚀
```
sudo apt-get install zsh
```

```
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```


sudo -i -u postgres
psql

# 6 how to copy file from path on device to another path on another device   🚀
```
scp pathDevice1 username@IPdevice2:pathDevice2
```
## for example 🚀
```  
scp /home/mahney/Downloads/project_v_one.zip platrain@192.168.1.25:/home/platrain/Documents
```
## how to partation :
/root
swap
/boot
/home 

sudo dpkg -i  '/media/mahney/hardmahney/linux_programs/balena-etcher-electron_1.5.109_amd64.deb'


pkill gunicorn

# ubuntu-platrain-v2 on DigitalOcean 
```ssh
ssh root@143.110.168.90
```
```password
with010*#ALLAH
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
------------
------------
------------     
# PlatRain Machine : digital ocien 
```
ssh root@188.166.73.85
```
```password
b$GDC&HuCU7zd9n
```

sudo ufw delete allow 80

/home/platrainproject/PlatRain 