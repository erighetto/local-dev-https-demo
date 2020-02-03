# Nginx as reverse proxy  
In this example we have Nginx as reverse proxy: Nginx load self signed certificates and redirect all traffic to docker service.

## Docker 
The [.env](.env) file, is only used during a pre-processing step when working with [docker-compose.yml](docker-compose.yml)  files. Dollar-notation variables like $PROJECT_NAME are substituted for values contained in an “.env” named file in the same directory.

## Nginx 
Static configurations are in [nginx/nginx.conf](nginx/nginx.conf).  
Note that [certificates](https://github.com/erighetto/local-dev-https-demo/blob/master/nginx-https/nginx/nginx.conf#L23) are the same declared on [docker-compose volumes](https://github.com/erighetto/local-dev-https-demo/blob/master/nginx-https/docker-compose.yml#L30).  
Also note that the [service behind proxy](https://github.com/erighetto/local-dev-https-demo/blob/master/nginx-https/nginx/nginx.conf#L32) has the same name of the [docker-compose service](https://github.com/erighetto/local-dev-https-demo/blob/master/nginx-https/docker-compose.yml#L5).
