# n8n

Self hosted n8n with Postgres support and exposed webhook.

## Steps to run

1. Download and install [ngrok](https://ngrok.com/). This will create a free URL for you to use on your n8n webhooks.
2. Clone this repository
3. Create a `.env` file with the following environment variables:

```
WEBHOOK_URL={ngrok's URL}
POSTGRES_HOST=localhost
POSTGRES_USER={postgres_user}
POSTGRES_PASSWORD={postgres_password}
POSTGRES_DB=n8n
N8N_ENCRYPTION_KEY={encryption key}
```
The encryption key can be generated with this: `openssl rand -hex 32`

4. Create a key and a certificate file for nginx. Execute in a terminal:

```
sudo openssl req -x509 -sha256 -nodes -newkey rsa:2048 -days 365 -keyout localhost.key -out localhost.crt
```

5. Leave both `localhost.key` and `localhost.crt` in the same directory of the cloned repository.
6. Run `docker compose up` 
