
# Linux basic and important commands  💚


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




