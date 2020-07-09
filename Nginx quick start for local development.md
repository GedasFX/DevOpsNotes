# Nginx quick start for local development

### Installation

1. `sudo apt update && sudo apt install nginx`
2. `sudo service nginx restart`

### Adding a service to proxy

1. Create file `/etc/nginx/sites-available/localhost` [[source]](https://docs.microsoft.com/en-us/aspnet/core/host-and-deploy/linux-nginx#configure-nginx)
```
server {
  listen        80;
  server_name   localhost *.localhost;
  location / {
    proxy_pass         http://localhost:4200;
    proxy_http_version 1.1;
    proxy_set_header   Upgrade $http_upgrade;
    proxy_set_header   Connection keep-alive;
    proxy_set_header   Host $host;
    proxy_cache_bypass $http_upgrade;
    proxy_set_header   X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header   X-Forwarded-Proto $scheme;
  }
}
```

2. `sudo ln -s /etc/nginx/sites-available/localhost /etc/nginx/sites-enabled/`
3. `sudo systemctl restart nginx`

