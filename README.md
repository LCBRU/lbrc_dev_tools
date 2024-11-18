# LBRC Dev Tools

This repository contains a set of tools to help the development process that can be run using [Docker Compose](https://docs.docker.com/compose/).

**Do not use these tools, as is, in a production environment!**

## Installation

To use this toolset you will need to install Docker Compose using the [Docker Compose Install Guide](https://docs.docker.com/compose/install/)

## Usage

To start the toolset use the command:

```bash
docker compose up
```

To only start a single tool use the command below inserting the name of the specific service from the `docker-compose.yml` file:

```bash
docker compose up {tool service name}
```

## Tools
### Redis

[Redis](https://redis.io/) is an in-memory key/value database that can be used as a temporary data store.  Example uses are:
- Cache storage
- Message broker

Leicester BRC Flask applications can use Redis as a broker for asynchronous task execution using [Celery](https://docs.celeryq.dev/en/stable/getting-started/introduction.html). To use this dev instance of Redis with Celery in your LBRC Flask Application, use the following values in their `.env` file:

```bash
export BROKER_URL='redis://localhost:6379/0'
export CELERY_RESULT_BACKEND='redis://localhost:6379/0'
export CELERY_RATE_LIMIT='100/m'
export CELERY_REDIRECT_STDOUTS_LEVEL='INFO'
export CELERY_SERVER_NAME='localhost:8000'
export CELERY_DEFAULT_QUEUE='{application name}'
export CELERY_LOG_DIRECTORY='./logs/'
```

- Change `{application name}` to the name of your application
- Log entries will be stored in the `service.log` file in the `log` directory.

### SMTP4Dev

[smtp4dev](https://github.com/rnwood/smtp4dev) is an development email server that stores emails instead of forwarding them to the end user.  These emails can then be viewed in a web GUI.  This is useful for application development as it allows you to test emailing, without spamming your users.

Leicester BRC Flask Applications can use smtp4dev as an email server by using the following settings in their `.env` file:

```bash
export MAIL_DEFAULT_SENDER="{valid email address}"
export SMTP_SERVER="localhost"
```

To view the emails on the web GUI, browse to [http://localhost:5000/](http://localhost:5000/).
