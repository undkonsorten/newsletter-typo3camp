---
theme: foobar
class:
    - lead
    - invert
auto-scaling:
    - math
    - code
title: TYPO3 Installationen mit T3Monitoring überwachen
author: Karsten Nowak
date: Oktober 2024
footer: 'TYPO3 Installationen mit T3Monitoring überwachen - TYPO3 Camp Berlin-Brandenburg 2024'
style: |
    a {
      color: #ccc;
    }
    small {font-size:.8em;}
---
<!-- backgroundColor: #213e21 -->
# TYPO3 Installationen mit T3Monitoring überwachen

Talk zum TYPO3 Camp Berlin-Brandenburg 2024


Karsten Nowak


---

# Ausgangslage

* Mehrere TYPO3 Versionen einfach überprüfen auf
* verwendete TYPO3 Version, ist die unsicher?
* installierte Extensions
* unsichere Extension vorhanden?
* bestimmte Konfigurationen
* was auch immer

---

# Benötigte Tools

* https://ddev.readthedocs.io/en/stable/
* https://extensions.typo3.org/extension/t3monitoring_client
* https://extensions.typo3.org/extension/t3monitoring

---

## Vorbereitung

### Die zu überwachende TYPO3 Instanz

* t3monitoring_client installieren
* Secret für T3Monitoring erzeugen und setzen

### Lokales Ddev für T3Monitoring Server

* Ddev Projekt mit t3monitoring aufsetzen
* im Backend einen Datensatz für die TYPO3 Instanz anlegen
* alle benötigten Infos angeben: Domain, Secrect, eventuelle Basic Auth,…
* Daten abrufen

---

**Das ist alles. Jetzt gehts an die Präsentation!**

---

# Das war's?

* Nicht ganz.

* Ein wichtiger Hinweis in der Doku https://github.com/georgringer/t3monitoring im Abschnitt "Pricing".

---

## Danke für eure Aufmerksamkeit.
