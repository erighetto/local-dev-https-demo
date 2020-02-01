# Using locally trusted certificates for local development with Docker and Traefik  
An easy way of having trusted self signed certs for local development needs.  
We’re assuming you work on a Mac OS machine and you use Docker.  
Tool used:  
 - mkcert 
 - dnsmasq

  
## mkcert
A simple zero-config tool to make locally trusted development certificates with any names you'd like  
https://github.com/FiloSottile/mkcert  
  
## dnsmasq
Wildcard DNS in localhost development  
https://gist.github.com/eloypnd/5efc3b590e7c738630fdcf0c10b68072  
  
## Docker 
The [.env](.env) file, is only used during a pre-processing step when working with [docker-compose.yml](docker-compose.yml)  files. Dollar-notation variables like $HI are substituted for values contained in an “.env” named file in the same directory.
All the magic is in [label](https://github.com/erighetto/traefik-https-demo/blob/master/docker-compose.yml#L15) section of **php** service. We set up a middleweare that redirect http to https.

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
