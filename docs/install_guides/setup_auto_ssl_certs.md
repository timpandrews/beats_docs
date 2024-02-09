# Installation Guide - Production Environment - Addendum

## Setting up automatic SSL certificates for a new domain using Let's Encrypt and Certbot

Certbot is a free, open-source software tool for automatically using Let's Encrypt certificates on manually-administrated websites to enable HTTPS.

- Follow this How to from Digital Ocean  
<a href="https://www.digitalocean.com/community/tutorials/how-to-use-certbot-standalone-mode-to-retrieve-let-s-encrypt-ssl-certificates-on-ubuntu-22-04" target="_blank">![DigitalOcean](../assets/icons/digitalocean1a.png){: width="12%"} How To Use Certbot Standalone Mode to Retrieve Let's Encrypt SSL Certificates on Ubuntu 22.04</a>
- Note you need to get certs for both newdomain.com & www.newdomain.com.  This changes the command in step 2 of the above how-to.
```bash
sudo certbot --nginx -d yourdomain.com -d www.yourdomain.com
```

#### More

```bash title="Check Auto-Renew Timer"
sudo systemctl status snap.certbot.renew.service
```
```bash title="Dry Run"
sudo certbot renew --dry-run
sudo certbot renew --nginx --dry-run  # remove --dry-run for actual renewal
```
<a href="https://www.digitalocean.com/community/tutorials/how-to-secure-nginx-with-let-s-encrypt-on-ubuntu-22-04" target="_blank">![DigitalOcean](../assets/icons/digitalocean1a.png){: width="12%"} How To Secure Nginx with Let's Encrypt on Ubuntu 22.04</a>
