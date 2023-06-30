# nginx.conf
global context defines
- the user (nginx installs a nginx user),
- how many worker processes (docs recommend the number of cores)
- where the errors are logged. This contains both access logs and error logs
- pid file. No reason to change that.

The http block is where you can configure most of the behavior of the server. The include statement at the bottom brings in the conf files for all the individual sites being served. Those are located in /etc/nginx/conf.d

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
