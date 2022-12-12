
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