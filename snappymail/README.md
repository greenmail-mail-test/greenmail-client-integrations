GreenMail test setup with SnappyMail
=========

The nginx image is based on the standard nginx Alpine image by NGINX, Inc. 
It relies on the nginx configuration of [nginx-for-php-fpm](https://github.com/JoshuaWalsh/docker-nginx-for-php-fpm) by
[Joshua Walsh](https://github.com/JoshuaWalsh). The image allows for serving php-fpm apps with nginx and is enriched
with SnappyMail for checking access and serving static content.

The php-fpm image is based on the official php fpm-alpine image maintained by the
[Docker Community](https://github.com/docker-library/php). It is also enriched with SnappyMail to serve its php files.

Run `docker compose up` and access SnappyMail in your browser. For further configuration refer to the
[wiki](https://github.com/the-djmaze/snappymail/wiki) especially the part of
[accessing the admin page](https://github.com/the-djmaze/snappymail/wiki/Installation-instructions#now-access-the-admin-page).

| Port | Description       |
|------|-------------------|
| 8080 | GreenMail API     |
| 8090 | SnappyMail Client |
| 3025 | GreenMail SMTP    |
| 3143 | GreenMail IMAP    |
