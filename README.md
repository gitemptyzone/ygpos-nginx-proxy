# ygpos-nginx-proxy
Running nginx-proxy docker container based on [jwilder/nginx-proxy](https://github.com/jwilder/nginx-proxy).
Even though this project is currenlty forcused on running ygpos-backend application, you can used it for common web application project.

All service containers, which is running under the nginx-proxy service, should be running under the same network.

Following part should be added to docker-compose.yml of each service:
```
networks:
  default:
    external:
      name: ${NGINX_PROXY_NETWROK}
```
NGINX_PROXY_NETWROK environment variable can be set on .env file or run following command:
```
$ export NGINX_PROXY_NETWROK=<network name>
```

## Usage
- Clone or pull the latest version of this project
- Create user-defined network which is used by each service containers
```
$ docker network create --driver bridge <name of network>
```
- Copy .env.example to .env, then enter the name of created user-defined network
- Execute "docker-composer up" command to create a service container
- You need to create a SSL certificate ./certs directory if it is required
- You can put configuration for pre-defined VIRTUAL HOST configuration under ./vhost.d


## Referrences
- [Automated Nginx Reverse Proxy for Docker](http://jasonwilder.com/blog/2014/03/25/automated-nginx-reverse-proxy-for-docker/)
- [jwilder/nginx-proxy](https://github.com/jwilder/nginx-proxy)
- [Using nginx-proxy](https://wiki.ssdt-ohio.org/display/rtd/Using+nginx-proxy)
- [Work with network commands](https://docs.docker.com/engine/userguide/networking/work-with-networks/)
- [Networking in Compose](https://docs.docker.com/compose/networking/)
