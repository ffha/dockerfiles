FROM php:8.1-apache
RUN COPY --from=composer /usr/bin/composer /usr/bin/composer
WORKDIR /app
RUN composer create-project flarum/flarum .
ENV APACHE_DOCUMENT_ROOT /app/public
RUN RUN apt-get update && apt-get install -y \
		libfreetype6-dev \
		libjpeg62-turbo-dev \
		libpng-dev \
	&& docker-php-ext-configure gd --with-freetype --with-jpeg \
	&& docker-php-ext-install -j$(nproc) gd
RUN sed -ri -e 's!/var/www/html!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/sites-available/*.conf
RUN sed -ri -e 's!/var/www/!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/apache2.conf /etc/apache2/conf-available/*.conf
VOLUME /app /mnt/docker/flarum
