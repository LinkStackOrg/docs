# Reverse Proxies

## Traefik
add this labels to your Docker Compose File 
```   
labels:
      - "traefik.enable=true"
      - "traefik.http.routers.name-ui.rule=Host(`domain.de`)"
      - "traefik.http.routers.name-ui.entrypoints=https"
      - "traefik.http.routers.name-ui.tls=true"
      - "traefik.http.routers.name-ui.tls.certresolver=le"
      - "traefik.http.routers.name-ui.service=yrtree-ui"
      - "traefik.http.services.name-ui.loadBalancer.server.port=443"
      - "traefik.http.services.name-ui.loadbalancer.server.scheme=https"
      - "traefik.http.routers.name-ui.middlewares=name-head,default@file"
      - "traefik.http.middlewares.name-head.headers.customrequestheaders.X-Forwarded-Proto=https"
      - "traefik.http.middlewares.name-head.headers.customResponseHeaders.X-Robots-Tag=none"
      - "traefik.http.middlewares.name-head.headers.customResponseHeaders.Strict-Transport-Security=max-age=63072000"
      - "traefik.http.middlewares.name-head.headers.stsSeconds=31536000"
      - "traefik.http.middlewares.name-head.headers.accesscontrolalloworiginlist=*"
      - "traefik.docker.network=traefik_web"
```
Start your Docker Compose and navigate to your "persistent storage" and 
change the .env search for FORCE_HTTPS=false (line 85) and set this to "true"

For this to work, the following must be set in the Traefik Config (static config) 
```
serversTransport:
  insecureSkipVerify: true
```

## Nginx 
Make sure to use HTTPS to access your container to avoid mixed content errors
```
server {
  listen        443 ssl;
  listen        [::]:443 ssl;
  listen        80;
  listen        [::]:80;
  server_name   your.domain.name;

  location / {
    # Replace with the IP address and port number of your Docker container.
    proxy_pass                          https://127.0.0.1:443;
    proxy_set_header Host               $host;
    proxy_set_header X-Real-IP          $remote_addr;

    proxy_set_header X-Forwarded-For    $proxy_add_x_forwarded_for;
    proxy_set_header X-Forwarded-Proto  https;
    proxy_set_header X-VerifiedViaNginx yes;
    proxy_read_timeout                  60;
    proxy_connect_timeout               60;
    proxy_redirect                      off;

    # Specific for websockets: force the use of HTTP/1.1 and set the Upgrade header
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection 'upgrade';
    proxy_cache_bypass $http_upgrade;
    proxy_set_header X-Forwarded-Proto $scheme;
    
    # Fixes Mixed Content errors.
    add_header 'Content-Security-Policy' 'upgrade-insecure-requests';
  }
}
```
