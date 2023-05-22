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