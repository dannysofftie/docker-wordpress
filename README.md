# Docker Wordpress

Easy Wordpress setup using docker

## Follow below steps to setup wordpress, easy and fast

Before you proceed, ensure you have `docker` and `docker-compose` installed.

1. Follow [docker installation steps](https://docs.docker.com/engine/install/ubuntu/) to install `docker`
2. Follow [docker-compose installation steps](https://docs.docker.com/compose/install/) to install `docker-compose`

## Wordpress Installation steps

These steps will install MySQL, Wordpress, Nginx and Certbot for automatic SSL certificate issuance and renewal

1.  Close this repo into a directory of your choice,
    `git clone https://github.com/dannysofftie/docker-wordpress.git`
2.  Open `docker-compose.yml` in your editor, and change below line to match your email and domain name

    `certonly --webroot --webroot-path=/var/www/html --email info@example.com --agree-tos --no-eff-email --force-renewal -d blog.example.com -d blog.example.com`

3.  Open `nginx.conf` in `nginx-conf` directory, and change all instances of `blog.example.com` to your domain.
4.  Run `docker-compose up -d`, then wait for about 2 minutes for MySQL to boot up,
5.  At this point, we need to make some changes to the wordpress docker image to allow uploading and editing theme files.

    - Run `docker exec -it wordpress bash` to access wordpress image shell,
    - Open `wp-config.php` in `nano` or `vim`,
    - Add `define( 'FS_METHOD', 'direct' )` at the bottom of the file and save it,
    - Change ownership of wordpress installation directory to allow making file modifications

      `chmod -R www-data:www-data /var/www`

6.  Exit the shell with the command `exit`
7.  Shut down your containers and restart to effect above changes

    `docker-compose down && docker-compose up -d`

8.  Now open `your-server-ip:3400` or `your-domain.com` on a browser to access your wordpress website and to set it up.
