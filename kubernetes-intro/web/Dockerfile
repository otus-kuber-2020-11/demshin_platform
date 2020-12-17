FROM nginx:1.19.5-alpine

ENV USER=nginx
ENV UID=1001
ENV GID=1001

RUN apk add --no-cache shadow=4.8.1-r0 && \
    usermod -u $UID nginx && groupmod -g $GID nginx

COPY ./homework.html /app/
COPY ./default.conf /etc/nginx/conf.d/default.conf

CMD ["nginx", "-g", "daemon off; error_log /dev/stdout debug;"]
EXPOSE 8000
