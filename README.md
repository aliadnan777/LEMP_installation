## LEMP installation on ubuntu 14.04

### Install NGINX 

### Install MYSQL

###Install PHP for Processing

* `sudo apt-get install php5-fpm php5-mysql`

### Configure the PHP Processor

* `sudo vi /etc/php5/fpm/php.ini`
* What we are looking for in this file is the parameter that sets `cgi.fix_pathinfo`. This will be commented out with   a semi-colon (;) and set to "1" by default.
* We will change both of these conditions by uncommenting the line and setting it to "0" like this:
  `cgi.fix_pathinfo=0`
* Save and close the file when you are finished.
* Now, we just need to restart our PHP processor by typing:
* `sudo service php5-fpm restart`
* Step Four — Configure Nginx to Use our PHP Processor
* `sudo vi  /etc/nginx/sites-available/default`


* Currently, with the comments removed, the Nginx default server block file looks like this:

``` 
server {
   *  listen 80 default_server;
    * listen [::]:80 default_server ipv6only=on;

    * root /usr/share/nginx/html;
    * index index.html index.htm;

    * server_name localhost;

    * location / {
        try_files $uri $uri/ =404;
    }
}
```
* The changes that you need to make are in red in the text below:
* replace above code with below one
```
 server {
  *  listen 80 default_server;
  *  listen [::]:80 default_server ipv6only=on;

  *  root /usr/share/nginx/html;
  *  index index.php index.html index.htm;

  *  server_name localhost;

  *  location / {
    *     try_files $uri $uri/ =404;
  *   }

    * error_page 404 /404.html;
    * error_page 500 502 503 504 /50x.html;
    * location = /50x.html {
    *    root /usr/share/nginx/html;
    * }

   * location ~ \.php$ {
    *    try_files $uri =404;
    *    fastcgi_split_path_info ^(.+\.php)(/.+)$;
    *    fastcgi_pass unix:/var/run/php5-fpm.sock;
    *    fastcgi_index index.php;
    *    fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    *    include fastcgi_params;
    * }
* } 
```


