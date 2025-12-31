# n8n

Self hosted n8n with Postgres support and exposed webhook.

## Steps to run

1. Clone this repository
2. Create a file named `.env` as a copy of the given `env.sample`
3. Edit the `.env` file and set the correct values (see below how to generate them)
4. Get a certificate for https connections using Let's Encrypt (see below)
5. Run `docker compose up`

## Generate environment values

- Generate the `N8N_ENCRYPTION_KEY` value using `openssl rand -hex 32`

## Get a certificate from Let's Encrypt

[Let's Encrypt](https://letsencrypt.org/) is a nonprofit organization that
provides free TLS certificates. To get a certificate from them you have to
have a valid DNS for your server and a webserver listening on the :80 port.

Upon request via `certbot`, Let's Encrypt will atempt to verify your domain
name by running an HTTP GET to the given domain name. If it's successful,
they will issue a certificate for that domain.

To request a certificate:

- Run `docker compose start nginx -d`
- Run `docker compose run --rm certbot certonly --webroot -w /var/www/certbot
 -d "servers_domain_name" --email "your@email.com" --agree-tos --no-eff-email`
(be mindful of `servers_domain_name` and `your@email.com`)
- Run `docker compose down`

This will install the certificates in the directory `./certbot-data/conf/`

To renew the certificates:

- Run `docker compose run --rm certbot renew --webroot -w /var/www/certbot`
- Run `docker compose exec nginx nginx -s reload`

The commands above can be left in the `crontab` file for automatic renewal.
