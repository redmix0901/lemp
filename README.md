# lemp
Install Lemp For Ubuntu.
STEP 1: UPDATE UBUNTU SERVER.
  sudo apt update && sudo apt dist-upgrade && sudo apt autoremove
STEP 2: INSTALL NGINX HTTP SERVER.
	sudo apt install nginx
STEP 3: INSTALLING PHP-FPM ON UBUNTU
	sudo apt install php-fpm
STEP 4: CONFIGURE NGINX TO USE PHP-FPM
	edit  www.conf  
	listen = 127.0.0.1:9000
STEP 5: CONFIGURE FILE VITRUAL HOST
	server {
   listen 80 ;

   root /var/www/html/cms/public;

   server_name  cms.news.vn;
   client_max_body_size 10M;
   large_client_header_buffers 4 16k;


   location / {
       index index.php index.html index.htm index.nginx-debian.html;
       try_files $uri $uri/ /index.php?$args;
   }

   location ~ \.php$ {
       try_files $uri =404;
       fastcgi_split_path_info ^(.+\.php)(/.+)$;
       fastcgi_pass localhost:9000;
       fastcgi_index index.php;
       include fastcgi_params;
       fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
   }

}
