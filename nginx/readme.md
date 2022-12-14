 
 # First Traning on Nginx 

 - the path of configuration file
    ```
    /etc/nginx/nginx.conf
    ```
 - configuration file
    ```
    events {}
   
    http{

     server{
        listen 80 ;
        server_name localhost 0.0.0.0 127.0.0.1 ;
        return 200 "first your web server using Nginx" ;
       }
   
    }
    ```
 - test and reload nginx 
   ```
   sudo nginx -t && sudo nginx -s reload
   ```
 # Second Traning on Nginx from directory 
   ```s
   /etc/nginx/mahney_website
    html.index
   ```  
   ```html
   <html>

    <head>
    <h1 align="center"> this is index.html</h1>
    </head>
    <bood>
    <p align="center"> nginx serves html file </p>
    </body>

   </html>
   ```
   ```nginx

    events {}

    http{

    server{
       listen 80 ; 
       server_name localhost 0.0.0.0 127.0.0.1 ;
       root /etc/nginx/mahney_website ;
     }
 
   }

   ```

# 
```css
h1 {
    background-color: blue;
}

```
```html
<!DOCTYPE html>
<html>
<head>
    <meta charset='utf-8'>
    <title>Page Title</title>
    <link rel='stylesheet' type='text/css' media='screen' href='./styles.css'>
   
</head>
<body>
    <h1> html with css files are serverd by : Nginx </h1>
</body>
</html>
```
```Nginx

events {}

 http{
   types {
      text/html html ;
      text/css css ;
   }

  server{
     listen 80 ; 
     server_name localhost 0.0.0.0 127.0.0.1 ;
     root /etc/nginx/mahney_website ;
    }
 
 }
```

#

```conf
events {}

 http{

   # types {
   #    text/html html ;
   #    text/css css ;
   # }
   include  mime.types;

  server{
     listen 80 ; 
     server_name localhost 0.0.0.0 127.0.0.1 ;
   
     root /etc/nginx/mahney_website ;

     location /second {
       alias /etc/nginx/mahney_website/mahney ;
     }
     
   #   location /mahney {
   #    root  /etc/nginx/mahney_website;
   #   }


      location /mahney {
      root  /etc/nginx/mahney_website;
      try_files /mahney/mahney.html /index.html = 404 ;
     }

    }
 
 }

```

```
```
```
```
```


cp -r /etc/nginx/mahney_website /home/mahney/Documents