# Localstack

## Install

```sh
# Download
curl --output localstack-cli-4.0.0-linux-amd64-onefile.tar.gz \
    --location https://github.com/localstack/localstack-cli/releases/download/v4.0.0/localstack-cli-4.0.0-linux-amd64-onefile.tar.gz

# Intall
sudo tar xvzf localstack-cli-4.0.0-linux-*-onefile.tar.gz -C /usr/local/bin

```

## Run

```sh
sudo DEBUG=1 localstack start # start localstack in background with -d flag
```

### Check status

```sh
localstack status services
```

## Docker-Compose

```sh
services:
  localstack:
    container_name: "${LOCALSTACK_DOCKER_NAME:-localstack-main}"
    image: localstack/localstack-pro  # required for Pro
    ports:
      - "127.0.0.1:4566:4566"            # LocalStack Gateway
      - "127.0.0.1:4510-4559:4510-4559"  # external services port range
      - "127.0.0.1:443:443"              # LocalStack HTTPS Gateway (Pro)
    environment:
      # Activate LocalStack Pro: https://docs.localstack.cloud/getting-started/auth-token/
      - LOCALSTACK_AUTH_TOKEN=${LOCALSTACK_AUTH_TOKEN:?}  # required for Pro
      # LocalStack configuration: https://docs.localstack.cloud/references/configuration/
      - DEBUG=${DEBUG:-0}
      - PERSISTENCE=${PERSISTENCE:-0}
    volumes:
      - "${LOCALSTACK_VOLUME_DIR:-./volume}:/var/lib/localstack"
      - "/var/run/docker.sock:/var/run/docker.sock"
```

## Docker

```sh
docker run \
  --rm -it \
  -p 127.0.0.1:4566:4566 \
  -p 127.0.0.1:4510-4559:4510-4559 \
  -v /var/run/docker.sock:/var/run/docker.sock \
  localstack/localstack
```

## Logs

```sh
localstack logs
```
