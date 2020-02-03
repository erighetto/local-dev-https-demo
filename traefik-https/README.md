# Traefik as router  
In this example we have Traefik as router: Traefik load self signed certificates and redirect all traffic to docker service.

## Docker 
The [.env](.env) file, is only used during a pre-processing step when working with [docker-compose.yml](docker-compose.yml)  files. Dollar-notation variables like $PROJECT_NAME are substituted for values contained in an “.env” named file in the same directory.
All the magic is in [label](https://github.com/erighetto/local-dev-https-demo/blob/master/traefik-https/docker-compose.yml#L15) section of **php** service. We set up a middleweare that redirect http to https.

      - "traefik.enable=true"  
      - "traefik.http.middlewares.${PROJECT_NAME}-redirect-websecure.redirectscheme.scheme=https"  
      - "traefik.http.routers.${PROJECT_NAME}-web.middlewares=${PROJECT_NAME}-redirect-websecure"  
      - "traefik.http.routers.${PROJECT_NAME}-web.rule=Host(`${PROJECT_BASE_URL}`)"  
      - "traefik.http.routers.${PROJECT_NAME}-web.entrypoints=web"  
      - "traefik.http.routers.${PROJECT_NAME}-websecure.rule=Host(`${PROJECT_BASE_URL}`)"  
      - "traefik.http.routers.${PROJECT_NAME}-websecure.tls=true"  
      - "traefik.http.routers.${PROJECT_NAME}-websecure.entrypoints=websecure"

  
## Traefik  
Static configurations are in [traefik/traefik.toml](traefik/traefik.toml).  
Dynamic configurations are in [traefik/dyn.toml](traefik/dyn.toml), here you can set what certificates Traefik have to load.
