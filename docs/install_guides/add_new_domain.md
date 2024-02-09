# Installation Guide - Production Environment - Addendum

## Adding a New Domain to the Server

#### Configure Nginx  
You need or update the Nginx server block (sometimes called a "virtual host") for your domain. 

- You can start by editing the new configuration file:
```bash
sudo micro /etc/nginx/sites-available/beats
```
- Then, update the server configuration. 
```text title="beats"
server {
    listen 80;
    server_name 159.65.189.23 newdomain.com, www.newdomain.com;

    location = /favicon.ico { access_log off; log_not_found off; }
    location /static/ {
        alias /home/rocket/beats/project/static/;
    }

    location /media/ {
        alias /home/rocket/beats/project/media/;
    }

    location / {
        include proxy_params;
        proxy_pass http://unix:/run/gunicorn.sock;
    }
}
```
- Test the Configuration: Always test your Nginx configuration for syntax errors after making changes:
```bash
sudo nginx -t
```
```title="expected output"
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
```
- Reload Nginx: If the configuration test passes, reload Nginx to apply the changes without stopping the server:
```bash title="Alias to restart both nginx & gunicorn"
restart
```
-- or --
```bash
sudo systemctl reload nginx
```
