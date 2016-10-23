FROM php:5.6.26

WORKDIR /app

RUN set -xe \
    && curl -A "Docker" -o /usr/bin/blackfire -D - -L -s https://packages.blackfire.io/binaries/blackfire-agent/1.8.0/blackfire-cli-linux_static_amd64 \
    && chmod +x /usr/bin/blackfire \
    && version=$(php -r "echo PHP_MAJOR_VERSION.PHP_MINOR_VERSION;") \
    && curl -A "Docker" -o /tmp/blackfire-probe.tar.gz -D - -L -s https://blackfire.io/api/v1/releases/probe/php/linux/amd64/$version \
    && tar zxpf /tmp/blackfire-probe.tar.gz -C /tmp \
    && mv /tmp/blackfire-*.so $(php -r "echo ini_get('extension_dir');")/blackfire.so \
    && printf "extension=blackfire.so\nblackfire.agent_socket=tcp://blackfire:8707\n" > $PHP_INI_DIR/conf.d/blackfire.ini \
    && rm -rf /tmp/blackfire-*
