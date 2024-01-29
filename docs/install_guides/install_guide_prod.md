# Installation Guide for Production Environment
## Step by Step Guide

1. Digital ocean droplet  
<small><a href="https://docs.digitalocean.com/products/droplets/how-to/create/" target="_blank">https://docs.digitalocean.com/products/droplets/how-to/create/</a></small>

2. Connect to droplet and initial setup
<small><a href="https://docs.digitalocean.com/products/droplets/how-to/connect-with-ssh/" target="_blank">https://docs.digitalocean.com/products/droplets/how-to/connect-with-ssh/</a></small>  
    - Logging in as root
    ```
    ssh root@your_server_ip
    ```
    - Creating a New User
    ```
    adduser rocket
    ```
    - Granting Admin Rights
    ```
    usermod -aG sudo rocket
    ```
    - setup ssh keys  
    <small><a href="https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent" target="_blank">https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent</a>
    <a href="https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account/" target="_blank">https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account/</a></small>
    - connect to droplet
    ```bash
    ssh -i /home/justtim/.ssh/digital_ocean_iris rocket@164.90.133.49
    ```
    - or create an alias  
    To create an alias for the SSH command, you can add the following line to your shell profile file (e.g., ~/.bashrc for Bash or ~/.zshrc for Zsh):
    ```
    alias remote="ssh -i /home/justtim/.ssh/digital_ocean_iris rocket@164.90.133.49"
    ```
    ```bash title="alias"
    remote
    ```

3. Setup new machine  
<small><a href="https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-22-04" target="_blank">https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-22-04</a>  
<a href="https://gist.github.com/bradtraversy/cfa565b879ff1458dba08f423cb01d71" target="_blank">https://gist.github.com/bradtraversy/cfa565b879ff1458dba08f423cb01d71</a>
</small>
    - setup firewall
    - Enable access for new user
    - disable root user
    - add ssh-key for local-machine to access remote 

4. Make Pretty and More Better <small>\*optional</small>  
    <small>This droplet should be around for awhile.  When your confident it will be you can add some things to make it nicer.</small>
    - <a href="https://starship.rs/" target="_blank">starship.rs ![starship](../assets/icons/starship.png){: width="2%"}</a> 
    - <a href="https://micro-editor.github.io/" target="_blank">micro ![micro](../assets/icons/micro_editor.png){: width="2%"}</a>

5. Setup new machine with Django, Postgres, Nginx & Gunicorn
    - https://www.digitalocean.com/community/tutorials/how-to-set-up-django-with-postgres-nginx-and-gunicorn-on-ubuntu-22-04

    - install python3.12 (https://www.linuxtuto.com/how-to-install-python-3-12-on-ubuntu-22-04/)
    - Update & install packages (python3.12)
    ```bash
    sudo apt update
    sudo apt install python3.12-venv python3.12-dev libpq-dev postgresql postgresql-contrib nginx curl
    ```
    - Create the PostgreSQL DB & User
    - add ssh-key for remote to access github


6. Clone Repo
    - clone repo to /home/rocket/beats
    - Create & activate Virtual Env 
    ```
    python3.12 -m venv _env
    ```
    - switch to production branch
    - update .env file (DB_HOST=127.0.0.1)

7. Setup Django
    - Run migrations
    - create superuser
    - collectstatic

8. Test Server
    - sudo ufw allow 8000
    - python manage.py runserver 0.0.0.0:8000
    - view server @ http://ip_or_url:8000/
    - sudo ufw delete allow 8000

9. Gunicorn Setup
    - pip install gunicorn 
    - TODO: how to deal with this and other production only dependencies
    - Open gunicorn.socket file and add this code to the file
    ```bash
    sudo micro /etc/systemd/system/gunicorn.socket
    ```
    ``` title="code to be added to gunicorn.socket"
    [Unit]
    Description=gunicorn socket

    [Socket]
    ListenStream=/run/gunicorn.sock

    [Install]
    WantedBy=sockets.target
    ```
    - Open gunicorn.service file and this code to the file
    ```bash
    sudo micro /etc/systemd/system/gunicorn.service
    ```
    ``` title="code to be added to gunicorn.service" hl_lines="7 9-10 15" linenums="1"  
    [Unit]
    Description=gunicorn daemon
    Requires=gunicorn.socket
    After=network.target

    [Service]
    User=rocket
    Group=www-data
    WorkingDirectory=/home/rocket/beats
    ExecStart=/home/rocket/beats/_env/bin/gunicorn \
                    --access-logfile /var/log/gunicorn/access.log \
                    --log-file /var/log/gunicorn/error.log \
                    --workers=3 \
                    --bind unix:/run/gunicorn.sock \
                    project.core.wsgi:application

    [Install]
    WantedBy=multi-user.target
    ```
    <small>pay close attention to lines 7, 9-10, & 15.</small>

    - Start and enable Gunicorn socket
    ```bash
    sudo systemctl start gunicorn.socket
    sudo systemctl enable gunicorn.socket
    ```
    - Check status of guinicorn
    ```bash
    sudo systemctl status gunicorn.socket
    ```
    - Check the existence of gunicorn.sock
    ```bash
    file /run/gunicorn.sock
    ```
    
10. Nginx Setup
    - Create project file and add this code to it.
    ```bash
    sudo micro /etc/nginx/sites-available/beats
    ```
    ``` title="code to be added to beats" hl_lines="3 7 11" linenums="1"
    server {
        listen 80;
        server_name 159.65.189.23;

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
    <small>pay close attention to lines 3, 7, & 11.</small>

    - Enable the file by linking to the sites-enabled dir
    ```bash
    sudo ln -s /etc/nginx/sites-available/beats /etc/nginx/sites-enabled
    ```
    - Test NGINX config
    ```bash
    sudo nginx -t
    ```
    - Restart NGINX
    ``` bash
    sudo systemctl restart nginx
    ```
    - Setup Firewall for Nginx (and remove port 8000 if you haven't already)
    ```bash
    sudo ufw delete allow 8000
    sudo ufw allow 'Nginx Full'
    sudo ufw status
    ```
    - You will probably need to up the max upload size to be able to create listings with images
        - Open up the nginx conf file
        ```bash
        sudo micro /etc/nginx/nginx.conf
        ```
        - Add this to the http{} area  
        ```client_max_body_size 20M;
        ```  
    - Reload NGINX
    ```bash
    sudo systemctl restart nginx
    ```
    - Possible issues with media files not showing up.  Try this 
    ```bash
    sudo rm -rf media/photos
    ```

11. Spend three days troubleshooting the 502 Bad Gateway Errors and issues with 
serving static files :scream:
    - Error in wsgi.py.  
    ```py title="wsgi.py" hl_lines="5-8"
    import os

    from django.core.wsgi import get_wsgi_application

    # it was 
    # os.environ.setdefault("DJANGO_SETTINGS_MODULE", "core.settings")
    # it was changed to:
    os.environ.setdefault("DJANGO_SETTINGS_MODULE", "project.core.settings")

    application = get_wsgi_application()
    ``` 
    - Issues with permissions for the www-data user and the media & static directories.  
        - The www-data user needs read and possible? write permissions to static.  
        - The www-data user needs read/write permissions to media.  
        - The www-data user needs execute permission to the entire project directory (allows access to directory without accessing individual files)

    - Add enctype="mutipart/form" to any forms saving files to media (e.g., profile avatars in profile forms)
    ```html
    <form method="post" enctype="multipart/form">
    ```


## Sources for the Step by Step Guide:    
  - <a href="https://docs.digitalocean.com/products/droplets/how-to/create/">https://docs.digitalocean.com/products/droplets/how-to/create/ :link:</a>  

  - <a href="https://docs.digitalocean.com/products/droplets/how-to/connect-with-ssh/" target="_blank">https://docs.digitalocean.com/products/droplets/how-to/connect-with-ssh/ :link:</a>  

  - <a href="https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-22-04" target="_blank">https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-22-04  :link:</a>  

  - <a href="https://www.digitalocean.com/community/tutorials-how-to-set-up-django-with-postgres-nginx-and-gunicorn-on-ubuntu-22-04" target="_blank">https://www.digitalocean.com/community/tutorials-how-to-set-up-django-with-postgres-nginx-and-gunicorn-on-ubuntu-22-04  :link:</a> 

  - <a href="https://gist.github.com/bradtraversy/cfa565b879ff1458dba08f423cb01d71" target="_blank">https://gist.github.com/bradtraversy/cfa565b879ff1458dba08f423cb01d71   :link:</a>  

## Commands
### Start / Stop / Status
```bash title="restart nginx & gunicorn"
sudo systemctl restart gunicorn
sudo systemctl restart nginx
```
```bash title="start & enable gunicorn.socket"
sudo systemctl start gunicorn.socket
sudo systemctl enable gunicorn.socket
sudo systemctl status gunicorn.socket
```
```bash title="restart gunicorn"
sudo systemctl restart gunicorn
sudo systemctl status gunicorn
```
```bash title="restart nginx"
sudo systemctl restart nginx
sudo systemctl status nginx
```
### View Logs
```bash title="nginx access.log"
sudo tail -f /var/log/nginx/access.log
```
```bash title="nginx error.log"
sudo tail -f /var/log/nginx/error.log
```
```bash title="gunicorn error.log"
sudo tail -f /var/log/gunicorn/error.log
```
### Edit Commands
```bash title="edit nginx site config"
sudo micro /etc/nginx/sites-available/beats
```
```bash title="edit gunicorn.socket"
sudo micro /etc/systemd/system/gunicorn.socket
```
```bash title="edit gunicorn.service"
sudo micro /etc/systemd/system/gunicorn.service
``` 
### Misc 
```bash title="reload daemon"
sudo systemctl daemon-reload
```
```bash title="Permission denied (publickey)"
 eval "$(ssh-agent -s)"
 ssh-add ~/.ssh/github_droplet
 ssh-add -l
```