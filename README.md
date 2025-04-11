# Task4
Содздание DNS тип А и добвление ssl. <br>
`https://task.kozow.com`
<br>
<br>
Концепция<br>
![Image alt](https://github.com/vazikk/Task4/blob/main/image1.png)
<br>
______________________________________
______________________________________
1) Страничка с контентом 1
   ```
   location /task { 
                alias /var/www/html/;<br>
                index 1.html;<br>
                try_files $uri $uri/ =404;<br>
        }
   ```
   ![Image alt](https://github.com/vazikk/Task4/blob/main/image2.png)

______________________________________
______________________________________
2) Скачивание песни
```
location /music {
                alias /var/www/music/;
                index blue.mp3;
                try_files $uri $uri/ =404;
                add_header Content-Disposition "attachment";
        }
```
   ![Image alt](https://github.com/vazikk/Task4/blob/main/image3.png)
______________________________________
______________________________________
3) Для задания с Apache + php, я открыл порт 8081

   ![Image alt](https://github.com/vazikk/Task4/blob/main/image4.png) <br>
 

  Конфигурация Apache:
  ```
  <VirtualHost *:8081>

        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/php


        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined

  </VirtualHost>
  ```
 
  Конфигурация Nginx:
  ```
  location /apache {
                proxy_pass http://task.kozow.com:8081/;
                proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                proxy_set_header X-Forwarded-Proto $scheme;
        }
  ```

   ![Image alt](https://github.com/vazikk/Task4/blob/main/image5.png) <br>

__________________________________________________
__________________________________________________

4) Респонс с другого сервера
   ```
   location /server {

        return 301 https://av.by/;

        }
   ```

      ![Image alt](https://github.com/vazikk/Task4/blob/main/image6.png) <br>
