After cloning:

# Step 1

`./download-element-apps.sh`

# Step 2

Add the following to the nginx config on the host, e.g. to `/etc/nginx/sites-enabled/besson.chat.conf`

```
server {
    listen 80;
    server_name besson.chat web.besson.chat synapse.besson.chat;

    location / {
        proxy_pass http://127.0.0.1:8080;
        proxy_set_header Host $host;
        proxy_set_header X-Forwarded-For $remote_addr;
    }
}
```