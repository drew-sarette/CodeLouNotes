# nginx.conf
main context defines
- the user (nginx installs a nginx user),
- how many worker processes (docs recommend the number of cores)
- where the errors are logged. This contains both access logs and error logs
- pid file. No reason to change that.

The http block is where you can configure most of the behavior of the server. The include statement at the bottom brings in the conf files for all the individual sites being served. Those are located in /etc/nginx/conf.d

# Controlling Nginx
- use ```sudo nginx -t``` to test the current configuration
- use ```sudo systemctl reload``` to reload the config files while keeping it running


# Server block
Ther server block, located in an individual .conf file in /etc/nginx/conf.d, configures the how nginx serves a given site. There may be several sites being served on the same machine. For example: 
```
server {
  listen    80;
  server_name example.com www.example.com;
# The server_name should list all the domains that should get the site

  location / {
    root /usr/share/nginx/html;
    index index.html index.htm;
  }
# There can be multiple location blocks that serve differn pages for the sam domain.
  location /blog/ {
    root /usr/share/nginx/blog;
    index  index.html index.htm;
  }

# serve a static error page 
  error_page 500 502 503 504  /50x.html
}
```

# Reverse Proxy
You can place apps or services behind a proxy like Nginx to encrypt the connection through https. You can even proxy multiple services on the same server. The server block for a reverse proxy could look like: 
```
server {
  listen 80;
  listen [::]:80;

  server_name example.com;

  location / {
    proxy_pass http://localhost:3000/;
  }

}
```