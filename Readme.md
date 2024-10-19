# Marp

https://marp.app/

https://www.npmjs.com/package/@marp-team/marp-cli

Marp-cli with docker: https://hub.docker.com/r/marpteam/marp-cli/

## Usage

```shell
# Convert slide deck into HTML
docker run --rm -v $PWD:/home/marp/app/ -e LANG=$LANG docker run --rm -v $PWD:/home/marp/app/ -e MARP_USER="$(id -u):$(id -g)" LANG=$LANG marpteam/marp-cli NewsletterTYPO3.md marpteam/marp-cli NewsletterTYPO3.md

# Convert slide deck into PDF (using Chromium in Docker)
docker run --rm --init -v $PWD:/home/marp/app/ -e LANG=$LANG docker run --rm -v $PWD:/home/marp/app/ -e MARP_USER="$(id -u):$(id -g)" LANG=$LANG marpteam/marp-cli NewsletterTYPO3.md marpteam/marp-cli NewsletterTYPO3.md --pdf

# Convert slide deck into PPTX (using Chromium in Docker)
docker run --rm --init -v $PWD:/home/marp/app/ -e LANG=$LANG docker run --rm -v $PWD:/home/marp/app/ -e MARP_USER="$(id -u):$(id -g)" LANG=$LANG marpteam/marp-cli NewsletterTYPO3.md marpteam/marp-cli NewsletterTYPO3.md --pptx

# Watch mode
docker run --rm --init -v $PWD:/home/marp/app/ -e LANG=$LANG docker run --rm -v $PWD:/home/marp/app/ -e MARP_USER="$(id -u):$(id -g)" LANG=$LANG marpteam/marp-cli NewsletterTYPO3.md -p 37717:37717 marpteam/marp-cli -w NewsletterTYPO3.md

# Server mode (Serve current directory in http://localhost:8080/)
docker run --rm --init -v $PWD:/home/marp/app -e LANG=$LANG docker run --rm -v $PWD:/home/marp/app/ -e MARP_USER="$(id -u):$(id -g)" LANG=$LANG marpteam/marp-cli NewsletterTYPO3.md -p 8080:8080 -p 37717:37717 marpteam/marp-cli -s .
```

We need user id in command.

Add: `-e MARP_USER="$(id -u):$(id -g)"`

Example:

docker run --rm --init -v $PWD:/home/marp/app/ -e LANG=$LANG -p 37717:37717 -e MARP_USER="$(id -u):$(id -g)" marpteam/marp-cli -w NewsletterTYPO3.md

With html output:

docker run --rm --init -v $PWD:/home/marp/app/ -e LANG=$LANG -p 37717:37717 -e MARP_USER="$(id -u):$(id -g)" marpteam/marp-cli -w T3Monitoring.md --html
