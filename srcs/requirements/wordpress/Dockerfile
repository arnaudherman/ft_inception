FROM debian:11

RUN apt-get update -y && apt-get upgrade -y \
  && apt-get install -y wget php php-fpm php-mysql sendmail -y

RUN wget -P /var/www/ https://wordpress.org/latest.tar.gz \
  && tar -xzvf /var/www/latest.tar.gz -C /var/www/ && rm /var/www/latest.tar.gz \
  && chown -R www-data:www-data /var/www/wordpress && chmod 755 /var/www/wordpress \
  && wget https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar \
  && chmod +x wp-cli.phar

COPY ./conf/www.conf /etc/php/7.4/fpm/pool.d

COPY ./tools/wp-setup.sh .

RUN chmod u+x wp-setup.sh && mkdir -p /run/php/

EXPOSE 9000

ENTRYPOINT ["./wp-setup.sh"]
