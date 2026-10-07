# Marp

https://marp.app/

https://www.npmjs.com/package/@marp-team/marp-cli

Marp-cli with docker: https://hub.docker.com/r/marpteam/marp-cli/

## Usage

All talks share the theme `theme/undkonsorten.css` `.marprc.yml` already
enables raw HTML, local files, the theme and the progress bar, so just run from the repo root.
`MARP_USER` is needed so output files belong to you.

```bash
RUN="docker run --rm --init -v $PWD:/home/marp/app/ -e LANG=$LANG -e MARP_USER=$(id -u):$(id -g)"

# Convert slide deck into HTML (or add --pdf / --pptx)
$RUN marpteam/marp-cli NewsletterTYPO3.md

# Watch mode (preview in browser, http://localhost:37717)
$RUN -p 37717:37717 marpteam/marp-cli -w NewsletterTYPO3.md

# Server mode (serve current directory in http://localhost:8080/)
$RUN -p 8080:8080 -p 37717:37717 marpteam/marp-cli -s .
```

Marp talks: `NewsletterTYPO3.md` (CuteMailing), `T3Monitoring.md`. Screenshots for the bounce slides live in `images/bounce/`.
Asset paths in the theme are relative to the deck, so keep the Marp decks in the repo root.

## EasyChat (plain HTML, not Marp)

`EasyChat.html` is the hand-written deck from `easychat-dev/docs/presentation/easychat-extension-cube.html`,
copied unchanged (self-contained, images embedded). Open it in a browser:
arrows/space/PageUp/PageDown, `Home`/`End`, `F` for fullscreen, `#n` in the URL jumps to slide n.
When the original changes, copy it over again.

```bash
# PDF (one slide per page, the file has a print stylesheet)
google-chrome --headless=new --no-sandbox --no-pdf-header-footer --print-to-pdf=EasyChat.pdf "file://$PWD/EasyChat.html"
```
