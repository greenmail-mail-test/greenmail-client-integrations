FROM nginx:1.24.0-alpine

EXPOSE 8080

ARG SNAPPY_MAIL_VERSION=2.28.4
ARG GPG_FINGERPRINT="1016 E470 7914 5542 F8BA  1335 4820 8BA1 3290 F3EB"

RUN apk update && apk -U upgrade \
 && apk add -t build-dependencies gnupg \
 && cd /tmp \
 && SNAPPY_MAIL_TGZ="snappymail-${SNAPPY_MAIL_VERSION}.tar.gz" \
 && curl -L --no-progress-meter -w "Downloaded %{url}\n" -o snappymail.tar.gz \
    https://github.com/the-djmaze/snappymail/releases/download/v${SNAPPY_MAIL_VERSION}/${SNAPPY_MAIL_TGZ} \
 && curl -L --no-progress-meter -w "Downloaded %{url}\n" -o snappymail.tar.gz.asc \
    https://github.com/the-djmaze/snappymail/releases/download/v${SNAPPY_MAIL_VERSION}/${SNAPPY_MAIL_TGZ}.asc \
 && curl -L --no-progress-meter -w "Downloaded %{url}\n" -O \
    https://raw.githubusercontent.com/the-djmaze/snappymail/master/build/SnappyMail.asc \
 && gpg --import SnappyMail.asc \
 && FINGERPRINT="$(LANG=C gpg --verify snappymail.tar.gz.asc snappymail.tar.gz 2>&1 \
  | sed -n "s#Primary key fingerprint: \(.*\)#\1#p")" \
 && if [ -z "${FINGERPRINT}" ]; then echo "ERROR: Invalid GPG signature!" && exit 1; fi \
 && if [ "${FINGERPRINT}" != "${GPG_FINGERPRINT}" ]; then echo "ERROR: Wrong GPG fingerprint!" && exit 1; fi \
 && mkdir -p /var/www/webmail \
 && tar xzf /tmp/snappymail.tar.gz -C /var/www/webmail \
 && find /var/www/webmail -type d -exec chmod 755 {} \; \
 && find /var/www/webmail -type f -exec chmod 644 {} \; \
 && chown -R nginx:nginx /var/www/webmail \
 && apk del build-dependencies \
 && rm -rf /tmp/* /var/cache/apk/* /root/.gnupg

ADD default.conf /etc/nginx/conf.d
