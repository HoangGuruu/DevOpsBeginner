![Alt texts](../Images/p1.png)

# Day 10 | 

```sh


sudo apt-get update // Update package list
sudo apt-get install nginx // Install Nginx


sudo nano /etc/nginx/sites-available/my-next-app // Create NGINX config file

server {
    listen 80;
    listen [::]:80;

    root /var/www/html;
    index index.html index.htm index.nginx-debian.html;

    server_name your-domain.com;

    location / {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}


sudo ln -s /etc/nginx/sites-available/my-next-app /etc/nginx/sites-enabled // Enable NGINX site
sudo nginx -t // Verify NGINX configuration syntax
sudo systemctl restart nginx // Restart NGINX
```