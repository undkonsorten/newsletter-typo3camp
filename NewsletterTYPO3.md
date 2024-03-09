---
theme: foobar
class:
    - lead
    - invert
auto-scaling:
    - math
    - code
title: CuteMailing und Co - Newsletter mit TYPO3
author: Karsten Nowak
date: März 2024
---

# Newsletter mit TYPO3 erstellen und versenden

Präsentation von Karsten Nowak zum TYPO3 Camp Mitteldeutschland 14.-16.3.24

---

# Vorteile

* TYPO3 können und kennen wir! Auch die Redakteure!
* Inhalte aus TYPO3 verwenden, News nicht doppelt schreiben.


# Herausforderungen

* An- und Abmeldungen für eine Empfängerliste
* Templating für Tabellenlayout
* Versandtool
* Versandprobleme, als Spam eingestuft
* Bouncehandling
* Auswertungen, Statistiken

---

# Unsere Tools für Newsletter in TYPO3

* Für die An- und Abmeldung: `registeraddress`
  * als Ergänzung: `registeraddress_logger` für das Loggen des An- und Abmeldevorgangs
* Für Anlegen der Newsletter und den Versand: `cute_mailing`
  * dabei Nutzung der Extension `task_queue` um die einzelnen Versandvorgänge nacheinander abzuarbeiten

* Foundation für E-Mails, fertig einsetzbar in der Extension `email_templating`
  * Notwendig auch die Extension `html_mail_utility` (CSS Inliner, Inky Tags umschreiben)
    * PHP Erweiterung xsl notwendig

---

# Newsletter Templating bedeutet Tabellenlayout?

Wollen wir wirklich solchen Code schreiben?

```html

<table align="center" class="container">
  <tbody>
    <tr>
      <td>
        <table class="row">
          <tbody>
            <tr>
              <th class="small-12 large-12 columns first last">
                <table>
                  <tbody>
                    <tr>
                      <th>Put content in me!</th>
                    …
```

---

# Mit Inky können wir das so schreiben

```html
<container>
  <row>
    <columns>Put content in me!</columns>
  </row>
</container>
```

Das ist alles? Ja, diese 3 Angaben, 5 Zeilen Code werden in vielen Zeilen HTML Code umgeschrieben.

---

# Das ist der erzeugt Code aus den 3 Zeilen vorher

```html
<table align="center" class="container">
  <tbody>
    <tr>
      <td>
        <table class="row">
          <tbody>
            <tr>
              <th class="small-12 large-12 columns first last">
                <table>
                  <tbody>
                    <tr>
                      <th>Put content in me!</th>
                      <th class="expander"></th>
                    </tr>
                  </tbody>
                </table>
              </th>
            </tr>
          </tbody>
        </table>
      </td>
    </tr>
  </tbody>
</table>
```

---

# Und was war jetzt mit CSS Inliner?

CSS muss für beste Kompatibilität direkt in die HTML Tags geschrieben werden.
Das macht auch niemand per Hand oder?

Foundation bietet dafür online einen Service an:
https://get.foundation/emails/inliner.html

Man könnte nun mit dem E-Mail Templates von Foundation
https://get.foundation/emails/email-templates.html

und dem CSS Inliner sich sein Template manuell zusammenbauen.

Das wollen wir nicht tun!

---

## Die TYPO3 Extension `email_template` bringt alles notwendige mit!

* ein PHP Ersatz für Inky
* ein CSS Inliner
* unterschiedliches Rendering für Ansicht im Browser und in der E-Mail
* ein fertiges Template was man sofort benutzen kann


---

# Newsletter anlegen und Versenden mit TYPO3

Für den Versand gibts es mittlerweile brauchbare Tools.

DirectMail war lange das Tool der Wahl für die meisten, ist aber in die Jahre gekommen.

* Mittlerweile ist mit `mail` ein direkter Nachfolger im TER und wird auch gepflegt.
* `luxletter` gibt es auch schon eine Weile.
* Und jetzt kommen wir mit CuteMailing?

---

# CuteMailing "nur" ein Versand Tool?

Ja genau, da ist es! Das war der Grund für uns im Februar 2022 eine solche Extension für TYPO3 zu bauen.
Es gab damals für uns nichts was wirklich gepasst hatte.

* `direct_mail` schied aus, da zu alt und nicht zukunftssicher aus unserer Sicht
* `luxletter` war zu sehr auf fe_user fixiert, damals die MultiSite Konfiguration noch schwierig
* beide Tools machen noch einiges mehr, was wir gar nicht brauchen oder wollen
* `mail` gab es damals noch nicht

---

# Cute Mailing

* Sys-Ordner für Cutemailing
* TypoScript Template für Newsletter anlegen
* Empfängerlisten anlegen
* TYPO3 Seite für Versand anlegen
* Newsletterdatensatz anlegen mit den üblichen Daten (Empfänger, Subject, Absender)
* Scheduler oder manuell in der TaskQueue den Versand anstoßen
  * findet in 2 Schritten statt, 1. Newsletter entpacken, 2. einzelne Mails versenden

---

Links:

https://extensions.typo3.org/extension/registeraddress
https://packagist.org/packages/undkonsorten/registeraddress-logger
https://extensions.typo3.org/extension/cute_mailing
https://extensions.typo3.org/extension/taskqueue
https://get.foundation/emails.html
