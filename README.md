## Installing nginx
1.  go to nginx.org/en/download.html
2.  copy mainline version url
3.  ```# wget <paste url here>```
4.  ```# tar -zxvf nginx-x.x.x.tar.gz```
5.  ```# cd nginx.x.x.x```
6.  ```# apt install build-essential```
7.  ```# ./configure```
8.  Read the output and install missing dependencies these may not be the same as the ones listed below
9.  ```# apt install libpcre3 libpcre3-dev zlib1g zlib1g-dev libssl-dev```
10. For detailed info on configuring nginx build go to nginx.org/en/docs/configure.html 
11. ```# ./configure --sbin-path=/usr/bin/nginx --conf-path=/etc/nginx/nginx.conf --error-log-path=/var/log/nginx/error.log --http-log-path=/var/log/nginx/access.log --with-pcre --pid-path=/var/run/nginx.pid --with-http_ssl_module```
12. ```# make```
13. ```# make install```
14. Check to make sure the above command contains nginx config files
15. ```# ls -l /etc/nginx```
16. Check to make sure nginx is installed properly
17. ```# nginx -V```
18. ```# nginx```
19. ```# ps aux | grep nginx```
20. You should see nginx running in the list of processes
21. ```# ifconfig```
22. Copy ip and paste it into browser url and you should see a loading page
23. ```# touch /lib/systemd/system/nginx.service```
24. ```# nano /lib/systemd/system/nginx.service```
25. Enter the following into the file:
```
[Unit]
Description=The NGINX HTTP and reverse proxy server
After=syslog.target network.target remote-fs.target nss-lookup.target

[Service]
Type=forking
PIDFile=/var/run/nginx.pid
ExecStartPre=/usr/bin/nginx -t
ExecStart=/usr/bin/nginx
ExecReload=/bin/kill -s HUP $MAINPID
ExecStop=/bin/kill -s QUIT $MAINPID
PrivateTmp=true

[Install]
WantedBy=multi-user.target
```
26. ```# nginx -s stop```
27. ```# systemctl start nginx```
28. ```# systemctl enable nginx```
29. ```# reboot```
30. ```# systemctl status nginx```

## Adding dynamic modules:
1.  ```# nginx -V```
2.  Copy "configure arguments"
3.  ```# ./configure <paste arguments> <add other modules to install here>  --modules-path=/etc/nginx/modules```
4.  ```# make```
5.  ```# make install```
6.  ```# nginx -V``` make sure the arguements match the ones above
7.  ```# systemctl reload nginx```
8.  ```# systemctl status nginx```
9.  

## Unnessisarry extra steps for php-fpm:
1.  ```# apt install php-fpm```
2.  ```# systemctl list-units | grep php``` This will show the directory of php-fpm
3.  ```# systemctl status php7.2-fpm``` Shows the status of php-fpm