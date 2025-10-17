---
theme: foobar
class:
    - lead
    - invert
auto-scaling:
    - math
    - code
title: CuteMailing und Co - Newsletter mit TYPO3
author: Karsten Nowak /Eike Starkmann
date: März 2025
footer: 'CuteMailing und Co - Newsletter mit TYPO3'
style: |
    a {
      color: #ccc;
    }
---
<!-- backgroundColor: #213e21 -->
# Newsletter mit TYPO3 erstellen und versenden


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
  * dabei Nutzung der Extension `taskqueue` um die einzelnen Versandvorgänge nacheinander abzuarbeiten

* Foundation für E-Mails, fertig einsetzbar in der Extension `email_template`
  * dabei Nutzung der Extension `html_mail_utility` (CSS Inliner, Inky Tags umschreiben)
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

Das ist alles? Ja, diese 3 Angaben, 5 Zeilen Code werden in viele Zeilen HTML Code umgeschrieben.

---

# Das ist der erzeugte Code aus den 5 Zeilen vorher

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
* Das passte alles aber nicht genau für unsere Anforderungen, daher entwickelten wir CuteMailing.

---

# CuteMailing "nur" ein Versand Tool?

Ja genau, da ist es! Das war der Grund für uns im Februar 2022 eine solche Extension für TYPO3 zu bauen.
Wir wollten ein Tool was sich genau um diesen Prozess kümmert.

* `direct_mail` schied aus, da zu alt und nicht zukunftssicher aus unserer Sicht
  * `mail` gab es damals noch nicht
* `luxletter` war zu sehr auf fe_user fixiert, damals die MultiSite Konfiguration noch schwierig
* beide Tools machen noch einiges mehr, was wir gar nicht brauchen oder wollen

---

# Cute Mailing - Wie läuft das?

* Sys-Ordner für CuteMailing
* TypoScript Template für Newsletter anlegen
* Empfängerlisten anlegen (verschiedene Empfängerlistentypen durch zusätzliche Extension bereitgestellt)
* TYPO3 Seite für Versand anlegen
* Newsletterdatensatz anlegen mit den üblichen Daten (Empfänger, Subject, Absender)
* Mittels Scheduler oder manuell in der TaskQueue den Versand anstoßen
  * findet in 2 Schritten statt, 1. Newsletter entpacken, 2. einzelne Mails versenden

---

# Exotische Adressliste? Konnektoren!

* CuteMailing hat nur rudimentäre Empfängerliste (kommasepariert)
* Extensions erweitern dieses Möglichkeit: tt_address_ register address, etc.
* Damit maximale Freiheit

---

# Asynchrone Verarbeitung Taskqueue

+ Ebenfalls eigene Extension
* Newsletter Task
  * Rendert Newsletter
  * Erstellt Versandtask (Mailtask)
* Ersetzt marker (personalisierung)
* Verschickt mail

---

# Case study

* One of our clients sends a daily newsletter with currently about 60.000 recipients a day.
* Möglich mit TYPO3?
* CuteMailing kann das, (1000 mails ~ 30sec)(Auf Standard Hardware)

---


Links:

* https://extensions.typo3.org/extension/registeraddress
* https://packagist.org/packages/undkonsorten/registeraddress-logger
* https://github.com/undkonsorten/registeraddress_honeypot
* https://extensions.typo3.org/extension/cute_mailing
* https://github.com/undkonsorten/typo3-cute-mailing-registeraddress
* https://github.com/undkonsorten/typo3-cute-mailing-ttaddress
* https://extensions.typo3.org/extension/taskqueue
* https://github.com/undkonsorten/email_template
* https://github.com/undkonsorten/html_mail_utility
* https://get.foundation/emails.html

---


## Danke für eure Aufmerksamkeit.

### Fragen?



