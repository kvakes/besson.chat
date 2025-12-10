After cloning:

# Step 1

`./download-element-apps.sh`

# Step 2

Add the following to the nginx config on the host, e.g. to `/etc/nginx/sites-enabled/besson.chat.conf` (and then symlink it to sites-enabled)

```
server {
    listen 80;
    server_name besson.chat web.besson.chat synapse.besson.chat;

    location / {
        proxy_pass http://127.0.0.1:18080;
        proxy_set_header Host $host;
        proxy_set_header X-Forwarded-For $remote_addr;
    }
}
```

OR (if Caddy is used as reverse proxy)

Add to `/etc/caddy/Caddyfile`

```
http://besson.chat, http://web.besson.chat, http://synapse.besson.chat {
    reverse_proxy 127.0.0.1:18080
}
```

# Step 3 (if synapse if showing permission errors for `/data/media_store`)

```
mkdir config/synapse/media_store
sudo chown -R 991:991 ./config/synapse
sudo chmod -R u+rwX ./config/synapse
```