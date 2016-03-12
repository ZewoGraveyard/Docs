# Nginx

The following tutorial shows how to configure nginx as a reverse proxy for a Zewo app.

## Preamble

- Tested on an Ubuntu 15.10 instance hosted by Digital Ocean.
- We suggest you to secure your server before any operations. You should read [7 security measures to protect your servers](https://www.digitalocean.com/community/tutorials/7-security-measures-to-protect-your-servers).
- In this example, we will use self-signed certificate that can be trusted in an iOS application. Keep in mind that this is completely *unsafe*. If you need to deploy your server for web usage, you should avoid this.

## Implementation

You can follow [Digital Ocean's tutorial](https://www.digitalocean.com/community/tutorials/how-to-create-a-ssl-certificate-on-nginx-for-ubuntu-12-04) (steps 1-4) to create a SSL certificate on nginx.

Now, to set up the virtual host, you need to create new virtual host file (substitute `example` with your project name).
```sh
sudo touch /etc/nginx/sites-available/example
```

Open this file using `nano` or your favorite text editor.
```sh
sudo nano /etc/nginx/sites-available/example
```

Configure your virtual host by writing next (by default your app is running on port **8080**):
```
server {
    listen 443;
    server_name example.com;
    access_log /var/log/nginx/example.access.log;
    location / {
        proxy_pass    http://127.0.0.1:8080/;
    }

    ssl on;
    ssl_certificate /etc/nginx/ssl/server.crt;
    ssl_certificate_key /etc/nginx/ssl/server.key;
}
```

Save the file and restart nginx.
``` 
sudo service nginx restart
```

Run your Zewo app 👏
