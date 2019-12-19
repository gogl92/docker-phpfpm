## docker-phpfpm

Docker PHP FPM with lean alpine base. The download size is just about 90MB.

It contains PHP7.4.0 with plenty of common and useful extensions.

## Usage
To pull latest image:

```sh
docker pull adhocore/phpfpm:7.4
```

To use in docker-compose
```yaml
# ./docker-compose.yml
version: '3'

services:
  phpfpm:
    image: adhocore/phpfpm:7.4
    container_name: phpfpm
    volumes:
      # Here you can also volume php ini settings
      # - /path/to/zz-overrides:/usr/local/etc/php/conf.d/zz-overrides.ini
    ports:
      - 9000:9000
    environment:
      # ...
```

### Extensions

The following PHP extensions are installed:

```
- ast               - bcmath            - bz2               - calendar
- core              - ctype             - curl              - date
- dom               - event             - exif              - fileinfo
- filter            - ftp               - gd                - gettext
- gmp               - hash              - iconv             - igbinary
- imagick           - imap              - intl              - json
- ldap              - libxml            - lzf               - mbstring
- memcached         - mongodb           - msgpack           - mysqli
- mysqlnd           - openssl           - pcntl             - pcov
- pcre              - pdo               - pdo_mysql         - pdo_pgsql
- pdo_sqlite        - pgsql             - phalcon           - phar
- posix             - psr               - readline          - redis
- reflection        - session           - simplexml         - soap
- sockets           - sodium            - spl               - sqlite3
- ssh2              - standard          - swoole            - swoole_async
- sysvmsg           - sysvsem           - sysvshm           - tideways_xhprof
- tidy              - tokenizer         - uuid              - xdebug
- xml               - xmlreader         - xmlwriter         - yaml
- zend opcache      - zip               - zlib
```

Read more about
[pcov](https://github.com/krakjoe/pcov),
[phalcon](https://github.com/phalcon/cphalcon),
[psr](https://github.com/jbboehr/php-psr),
[swoole](https://www.swoole.co.uk/),
[xhprof](https://github.com/tideways/php-xhprof-extension)

### Production Usage

For production you may want to get rid of some extensions that are not really required.
In such case, you can build a custom image on top `adhocore/phpfpm:7.4` like so:

```Dockerfile
FROM adhocore/phpfpm:7.4

# Disable extensions you won't need. You can add as much as you want separated by space.
RUN docker-php-ext-disable xdebug pcov
```

> `docker-php-ext-disable` is shell script available in `adhocore/phpfpm:7.4` only and not in official PHP docker images.
