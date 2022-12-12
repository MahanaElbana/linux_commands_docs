
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

# A List of Basic Troubleshooting Commands and their function within Ubuntu Linux

 - Used before a command to run as a root or an administrator ☄️
 
   ```
   sudo 
   ```  
 - To remove an empty directory => any command remove directory ☄️                                                     
   
   ```
   rm -d dirname
     or 
   rmdir dirname
   ```
 - To remove non-empty directories and all the files within them ☄️     

   ```
   rm -r dirname
   ```   

 - To show info about **ls** command , [-f, --whatis] = whatis ,man = mannual ☄️
   
   ```
   man -f ls 
   ``` 
   ```
   man --whatis ls
   ```
   ```
   whatis ls
   ``` 
 
```ls```                                                       | List directory contents                                                                |
```man -k fdisk```                                             | list commands to  manipulate disk partition table                                      |
```info    ```                                                 | read Info documents - readable online documentation                                    |
```info ls   ```                                               | more details than **man -f** or **man** or **man -k**                                  |
```xman  ```                                                   | Manual page display program for the X Window System                                    |
```xman & ```                                                  | show a manual page to help for known information about any command                     |
```ps aux```                                                   | report a snapshot of the current processes                                             |
```ps aux ! grep chrome ```                                    | to find a particular process                                                           |
```kill id_process```                                          | How to kill/stop a particular process                                                  |
```lsof```                                                     | command will show list of all open files                                               |
```top```                                                      | To know about all the running processes ,and their related status about CPU and memory |
```sudo systemctl reboot```                                    | To reboot the system using the systemctl command.                                      |
```sudo systemctl shutdown```                                  | To shutdown the system using the systemctl command.                                    |
```sudo apt-get update```                                      | To update all the package information for the Debian repositories                      |
```sudo apt-get install```                                     | To install any given package from the repository.                                      |
```ssh user@hostname```                                        | ssh command to login to remote computers                                               |
```sudo systemctl status sshd```                               | To know the current status of the service                                              |
```ssh mahney@localhost```                                     | to connect my device using shh                                                         |
```sudo apt install ssh```                                     | to install ssh service                                                                 |
```systemctl status ufw```                                     | to show status of ubuntu firewall                                                      |
```systemctl start ufw```                                      | to run ubuntu firewall                                                                 |
```systemctl stop ufw```                                       | to run ubuntu firewall                                                                 |


------------------------
------------------------
------------------------ 


##  How to Configure Network Connection Using **nmcli** Tool  👍

  - nmcli (the network manager command-line interface)

  - To display all the active network interfaces on your Linux system execute the command ☄️
    ```
    nmcli connection show
    OR
    nmcli con show 
    ```
 
  - To display both active and inactive interfaces ☄️
    ```
    nmcli dev status
    ``` 
 
  - To show ip address of your device ☄️
    ```
    ip address show 
    ip addr
    nmcli
    ```  

------------------------
------------------------
------------------------ 


# How to change [ Theme and icons ] 

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


# how to install Audacity
```
sudo apt install audacity
```
# How to show your disks and check space :+1:
```
df -h 
```
