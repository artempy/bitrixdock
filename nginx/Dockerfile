FROM nginx:1.18

COPY conf/nginx.conf /etc/nginx/
COPY conf/default.conf /etc/nginx/conf.d/
COPY conf/upstream.conf /etc/nginx/conf.d/

RUN usermod -u 1001 www-data

CMD ["nginx"]

EXPOSE 8080
