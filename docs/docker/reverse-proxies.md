# Reverse Proxies

## Traefik
add this labels to your Docker Compose File 
```   
labels:
      - "traefik.enable=true"
      - "traefik.http.routers.routename-rtr-ui.rule=Host(`domain.de`)"
      - "traefik.http.routers.routename-rtr-ui.entrypoints=https"
      - "traefik.http.routers.routename-rtr-ui.tls=true"
      - "traefik.http.routers.routename-rtr-ui.tls.certresolver=le"
      - "traefik.http.routers.routename-rtr-ui.middlewares=routename-ui-header,default@file"
      - "traefik.http.middlewares.routename-ui-header.headers.customrequestheaders.X-Forwarded-Proto=https"
      - "traefik.http.middlewares.routename-ui-header.headers.customResponseHeaders.X-Robots-Tag=none"
      - "traefik.http.middlewares.routename-ui-header.headers.customResponseHeaders.Strict-Transport-Security=max-age=63072000"
      - "traefik.http.middlewares.routename-ui-header.headers.stsSeconds=31536000"
      - "traefik.http.middlewares.routename-ui-header.headers.accesscontrolalloworiginlist=*"
      - "traefik.docker.network=traefik_web"
```
Start your Docker Compose and navigate to your "persistent storage" and change the .env 
search for FORCE_HTTPS=false (line 85) and set this to "true