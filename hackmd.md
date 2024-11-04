# Food2gether
Ein Gruppenbestellsystem, um die gemeinsame Bestellung in einer größeren Gruppe zu vereinfachen

## Mitglieder
**Marvin:** Backend und Orga
**Nikolas:** Backend
**Kaan:** Backend
**Robin:** Frontend
**Jo:** Wildcard

## Librarys und so
* OpenStreetMap / Leaflet
* PayPal
* Quarkus & Quarkus Web/REST
* Keycloak


## Links
- [Quarkus OpenConnect](https://quarkus.io/guides/security-openid-connect-providers#google)
- Andreas E-Mail: andreas.trautwein@soptim.de
- 

## Rollen
* Mitbestellende
* Organisierende 
* (Admin)

## Erwartungen
* Loginfenster
* Sitzungen
    * erstellen
    * bearbeiten
    * schliessen
    * beitreten
    * Übersicht aller Bestellungen
    * Übersicht eigner Bestellung
    * (Trinkgeld option)
    * Wer bezahlt?
    * Deadline
    * (private Sitzung)
* Restaurantes
    * Auflistung
    * Speisekarte
        * bearbeiten
        * (Computer vision speisekarte analysieren)
    * Location/Karte einbinden
    * (Benachrichtiugnen)
        * Essen is da
        * Nicht bezahlt
        * Deadline abgelaufen
        * 
* Bestellung
    * aufgeben -> sitzung beigereten
    * bearbeiten
    * entfernen
    * Overview
* Bezahlen
    * PayPal-Anbindung/QR-Code (aussicht)
    * Rechnung??
    * Bestatigungsfunktion
    * [Paypal.me-link](https://www.paypal.com/us/cshelp/article/paypalme-frequently-asked-questions-help432)
* (Demokratische Sitzung)
    * Abstimmung
    * Vorschläge
* Webapp(/mobile app??)


## Gregs Tagebuch :)
#### 29.10.
* Weiter Überlegungen zum Aufbau der Applikation
* MVP Usecase-Diagramm

![Usecase diragram](https://cdn-0.plantuml.com/plantuml/png/VP71JiCm38RlUOfezuqxggeDk8108FO4RkkraT9KYfqXfhqB5vw14xU-6CoBfqgRTdFyVqwS_ryIG-JKUsEWvY7Qny0OaSXXPBH0rcNXnN65nEWzXaQKFYkliONW3XEg3COamXe8xMpjU9T2Qp7cuTc1eFk8m7YEKTrvX-FNYVC3NS0gT1oHbNeQN3Y7jXWz42dqZB35oMQhn9qey5zC-dV7RnwVsK6dEmzly7cHWhHfiL9gdQhUyKNGZpzKTme-e4UUBlIEn90Y1BQT2xkq6NzR33UGw6FyFgqHLqspHeyr6pFO-RwqlUbjiPzRPqpsrHQBXNpBtjgYSA7sgS6oD6Bd5VNQiBmsBpKwfQKtsKaXoSsuuqdo6UHYgRKlaQYGy-b54hDpcHqLJ4-ggObB34tgFVy1)

#### 04.11.24
* erstes Treffen mit PO
* Vorstellung unserer Vorstellungen
* Überlegungen zum MVP:
    * Sitzung erstellen
    * auth
        * google gh fb apple usw
        * CLassisch email:password
        * keycloak?
    * beitreten über bestellen
        * Textfeld name, kontakt, essen, betrag
    * Sitzung
        * Zahlungszustand
        * Übersicht
        * einfrieren/deadline
        * 
