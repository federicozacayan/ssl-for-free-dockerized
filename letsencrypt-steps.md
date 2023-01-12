

# step 1
```
docker run --detach \
    --name nginx-proxy \
    --publish 80:80 \
    --publish 443:443 \
    --volume certs:/etc/nginx/certs \
    --volume vhost:/etc/nginx/vhost.d \
    --volume html:/usr/share/nginx/html \
    --volume /var/run/docker.sock:/tmp/docker.sock:ro \
    nginxproxy/nginx-proxy
```

# step 2

```
docker run --detach \
    --name nginx-proxy-acme \
    --volumes-from nginx-proxy \
    --volume /var/run/docker.sock:/var/run/docker.sock:ro \
    --volume acme:/etc/acme.sh \
    --env "DEFAULT_EMAIL=ssl@samutips.com" \
    nginxproxy/acme-companion
```
# step 3

```
docker run --detach \
    --name your-proxyed-app \
    --env "VIRTUAL_HOST=www.samutips.com,samutips.com" \
    --env "LETSENCRYPT_HOST=www.samutips.com,samutips.com" \
    --volume $(pwd)/client:/usr/share/nginx/html:ro \
    nginx
```
