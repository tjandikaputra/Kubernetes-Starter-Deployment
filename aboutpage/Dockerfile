FROM alpine:3.21.0

LABEL MAINTAINER="Andika Putra <andika.putra@iconpln.co.id>"

WORKDIR /usr/share/nginx/html/about

COPY ./index.html .

RUN apk update && apk upgrade --no-cache && \
  apk add --no-cache tzdata && \
  cp /usr/share/zoneinfo/Asia/Jakarta /etc/localtime && \
  echo "Asia/Jakarta" > /etc/timezone && \
  apk add nginx && \
  apk add nginx-mod-http-headers-more && \
  sed -i "s#/var/log/nginx/error.log#/dev/stderr#g" /etc/nginx/nginx.conf && \
  sed -i "s#/var/log/nginx/access.log#/dev/stdout#g" /etc/nginx/nginx.conf && \
  sed -i "s/user nginx/#user nginx/g" /etc/nginx/nginx.conf && \
  sed -i "s#return 404;#root   /usr/share/nginx/html;#g" /etc/nginx/http.d/default.conf && \
  sed -i '3i more_clear_headers Server;' /etc/nginx/http.d/default.conf && \
  sed -i '12i \ \t\t index index.html;' /etc/nginx/http.d/default.conf && \
  chown -R nginx:nginx /etc/nginx/ /usr/share/nginx/html && \
  rm -rf /var/cache/apk/*

USER nginx

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
