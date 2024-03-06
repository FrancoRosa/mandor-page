# Mandor mvp web page

## Notes about deploying

`nginx`` is used to deploy this site, this tutorial was used
https://medium.com/@rvisingh1221/serve-multiple-static-websites-with-https-using-nginx-f633d7c2a81a

[![Video Tutorial](https://img.youtube.com/vi/8MSbxjl0r3A/0.jpg)](https://www.youtube.com/watch?v=8MSbxjl0r3A)

the following steps where required to deploy the site:

```bash
sudo apt update
sudo apt install nginx
```

Then, create a config file `mandor.conf` and save on `/etc/nginx/sites-available/`,

```
server {
    listen 80;
    server_name mandor.pe;
    root /var/www/mandor-page;
    index index.html;
    # Other website-specific configurations
}
```

According to this file the `index.html` should be stored on `/var/www/mandor-page`

Create a symbolic link from available to enabled

```bash
sudo ln -s /etc/nginx/sites-available/mandor.conf /etc/nginx/sites-enabled/
```

Remove the default configuration to avoid conflicts

```bash
sudo rm /etc/nginx/sites-enabled/default
```

Test and reload `nginx`

```bash
sudo nginx -t
sudo systemctl reload nginx
```

Set permissions

```bash
sudo chown -R www-data:www-data /var/www/mandor-page
```

### SSL implementation

Install certbot and script to automatically configure `nginx`

```bash
sudo apt update
sudo apt install certbot python3-certbot-nginx
sudo certbot --nginx -d mandor.pe
```
