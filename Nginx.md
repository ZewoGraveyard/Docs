# Nginx

Let's see how to configure Nginx to securize transactions between client and server.

##Preamble

- Tested on an Ubuntu 15.10 instance hosted by Digital Ocean.
- We suggest you to securized your server before any operations. You should read : [7 security measures to protect your servers](https://www.digitalocean.com/community/tutorials/7-security-measures-to-protect-your-servers)
- We will use self signed certificate that can be self trusted in an iOS application for exemple. If you need to deploy your server for web usage you should avoid it.

##Implementation

You can follow the really good Digital Ocean's [tutorial](https://www.digitalocean.com/community/tutorials/how-to-create-a-ssl-certificate-on-nginx-for-ubuntu-12-04)

- You normaly created a folder that represents your domain. Let's edit the Nginx configuration file :

```
 sudo nano /etc/nginx/sites-available/yourdomain
```
- You can now write (by default your app is running on **8080**) : 

```
server {
    listen 443;
    server_name yourdomain.com;
    access_log /var/log/nginx/my-domain.access.log;
    location / {
        proxy_pass    http://127.0.0.1:8080/;
    }

    ssl on;
    ssl_certificate /etc/nginx/ssl/server.crt;
    ssl_certificate_key /etc/nginx/ssl/server.key;
}
```

- Save, quit and restart Nginx :
``` 
sudo service nginx restart
```
- Run your Zewo app 👏