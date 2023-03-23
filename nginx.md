# nginx deploy static websites

Install nginx:

```bash
sudo apt-get update
sudo apt-get install nginx
sudo nginx -v
```

Start or stop nginx:

```bash
# systemctl
sudo systemctl start nginx
sudo systemctl status nginx

# service
sudo service nginx {start|stop|restart|reload|force-reload|status|configtest|rotate|upgrade}
```

Reload nginx:

```bash
sudo nginx -s reload -t
```

Default website directory: `/var/www/html`

- `/etc/nginx/sites-available`: all configuration files of possible websites
- `/etc/nginx/sites-enabled`: links to configuration files of running websites

Create a configuration file `test` for website `test`:

```nginx
server {
    listen PORT;
    listen [::]:PORT;
    server_name _; # domain name
    root /folder/path/to/html;
    index index.html index.htm;
    location / {
        try_files $uri $uri/ =404;
    }
}
```

Link the configuration file to `sites-enabled`:

```bash
ln -s /etc/nginx/sites-available/test /etc/nginx/sites-enabled/test
```

Now restart nginx.
