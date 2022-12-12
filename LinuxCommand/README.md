
# Linux basic and important commands  💚

```
🚀==========================================🚀
🚀==========================================🚀 
🚀 ##      ##  ##     ##  ##   ##  ##    ## 🚀
🚀 ##      ##  ####   ##  ##   ##   ##  ##  🚀
🚀 ##      ##  ##  ## ##  ##   ##    ####   🚀
🚀 ##      ##  ##    ###  ##   ##   ##  ##  🚀
🚀 ######  ##  ##     ##   #####   ##    ## 🚀
🚀==========================================🚀 
🚀==========================================🚀
```

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

--------------
--------------
--------------




# 1. <a href="#Networking">Networking part -------------------------|</a>

-
# How to change [ theme and icons ] 

1. Write the following command in terminal :: to can move files from path to another 

   ``` 
   sudo nautilus
   ```

2. go to the following path to move theme file or icon file ::

   ```
   /usr/share/themes
   /usr/share/icons
   ```


# How to install zsh 

1. from default shell :

   ```
   sudo apt install zsh
   ```

2. from web site :

   ```
   https://ohmyz.sh/#install   
   ```

3.  to enter to zsh 

   ```
   zsh
   ```


# How to open system monitor ::

```
gnome-system-monitor
```

# system monitor on terminal : 
``` 
sudo apt install htop

```
# how to open htop on terminal 👍
```bash 
htop
```

# how to show shells on your device 👍
```
cat /etc/shells
```
# how to use tmux 
 1. write before any command 
    ``` 
    ctrl b 
    ```
## how to split screen 
```
ctrl + b 
shift + %
```
## how to split screen in tmux
```
ctrl + b 
shift + "
```

# how to install Audacity
```
sudo apt install audacity
```
# How to show your disks and check space :+1:
```
df -h 
```
# 🤞 A list of basic troubleshooting commands and their function within Ubuntu Linux
| count | Command                                                        | Function                                                                               |
| ----- | -------------------------------------------------------------- | -------------------------------------------------------------------------------------- |
| 1     | ```sudo```                                                     | Used before a command to run as a root or an administrator                             |
| 2     | ```rm -d dirname``` or ```rmdir dirname```                     | To remove an empty directory => any command remove directory                           |
| 3     | ```rm -r dirname```                                            | To remove non-empty directories and all the files within them                          |
| 4     | ``` man -f ls ```  or ```man --whatis ls``` or ```whatis ls``` | To show info about **ls** command , [-f, --whatis] = whatis ,man = mannual             |
| 5     | ``` ls```                                                      | List directory contents                                                                |
| 6     | ``` man -k fdisk```                                            | list commands to  manipulate disk partition table                                      |
| 7     | ``` info ```                                                   | - read Info documents - readable online documentation                                  |
| 8     | ``` info ls```                                                 | more details than **man -f** or **man** or **man -k**                                  |
| 9     | ```xman```                                                     | Manual page display program for the X Window System                                    |
| 10    | ```xman &```                                                   | show a manual page to help for known information about any command                     |
| 11    | ```ps aux```                                                   | report a snapshot of the current processes                                             |
| 12    | ` ps aux ! grep chrome `                                       | to find a particular process                                                           |
| 13    | ``` kill id_process```                                         | How to kill/stop a particular process                                                  |
| 14    | ```lsof```                                                     | command will show list of all open files                                               |
| 15    | ```top```                                                      | To know about all the running processes ,and their related status about CPU and memory |
| 16    | ```sudo systemctl reboot```                                    | To reboot the system using the systemctl command.                                      |
| 17    | ```sudo systemctl shutdown```                                  | To shutdown the system using the systemctl command.                                    |
| 18    | ```sudo apt-get update```                                      | To update all the package information for the Debian repositories                      |
| 19    | ```sudo apt-get install```                                     | To install any given package from the repository.                                      |
| 20    | ```ssh user@hostname```                                        | ssh command to login to remote computers                                               |
| 21    | ```sudo systemctl status sshd```                               | To know the current status of the service                                              |
| 22    | ```ssh mahney@localhost```                                     | to connect my device using shh                                                         |
| 23    | ```sudo apt install ssh```                                     | to install ssh service                                                                 |
| 24    | ```systemctl status ufw```                                     | to show status of ubuntu firewall                                                      |
| 25    | ```systemctl start ufw```                                      | to run ubuntu firewall                                                                 |
| 26    | ```systemctl stop ufw```                                       | to run ubuntu firewall                                                                 |


----
----
----

# <a id="Networking"> How to Configure Network Connection Using ‘nmcli’ Tool </a> 👍

 1. nmcli (the network manager command-line interface)

 2. To display all the active network interfaces on your Linux system execute the command.
   ```
   ➜  ~ nmcli connection show
   OR
   ➜  ~ nmcli con show
   ```
 3. To display both active and inactive interfaces. 
   ```
   ➜  ~ nmcli dev status
   ``` 
 4. modify a network interface(wlp2s0) to use a static IP address .
   ```
   nmcli device modify wlp2s0 ipv4.address 192.168.1.40/16 ipv4.gateway 192.168.1.1 ipv4.dns 8.8.8.8 ipv4.method manual
   ```
 5. To show ip address of your device 
   ```
   ip address show 
   or
   ip addr
   or 
   nmcli
   ```  
----
----
----

# ??? " -- future plans " ???
- linux course  =>  in ' /media/mahney/hardmahney/administration '
- linux book    =>  in '/media/mahney/hardmahney/libraryBooks/linux-books'
- nginx Master  =>  in 'documantaition'
- nginx book    =>  in '/media/mahney/hardmahney/libraryBooks'
- mak library management system with table borrow and table reservation in **dart lang** **using console** *json and postgre and mysql* 



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

# 5 how to install puthon3 on pop7🚀
```  
sudo apt-get update
``` 
``` 
sudo apt-get install python3.9.7
```
```
sudo apt-get install python3-pip

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