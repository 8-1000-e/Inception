FROM debian:bookworm

ARG USER_ID=1000
ARG GROUP_ID=1000

RUN apt update -y && apt upgrade -y && apt install -y curl php-fpm php-mysqli

RUN usermod -u ${USER_ID} www-data && groupmod -g ${GROUP_ID} www-data

RUN mkdir -p /run/php && chown www-data:www-data /run/php

COPY ./conf/www.conf /etc/php/8.2/fpm/pool.d
WORKDIR /var/www/html

COPY ./tools/script.sh .
RUN chmod +x script.sh

EXPOSE 9000

ENTRYPOINT ["/var/www/html/script.sh"]
CMD ["php-fpm8.2", "-F"]
