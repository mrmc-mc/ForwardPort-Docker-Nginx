# ForwardPort-Docker-Nginx
Forward port with nginx container to another container

## Nginx config:

### 1.remove default Nginx config file:

``` rm /etc/nginx/conf.d/default.conf ```


### 2. creat new config file ``` nano /etc/nginx/conf.d/my_conf.conf ``` then Add this lines:
```
server
{
    listen 80;

    location / {
        proxy_pass http://<YOUR Container Target Name>:<PORT>; # like my_con:8080
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
```
### 3. then reload nginx:

``` nginx -s reload ```
