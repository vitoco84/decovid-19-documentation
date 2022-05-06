# Decovid-19 Documentation

## Project Related Repositories

Project Repositories:
* [Frontend-Client](https://github.com/vitoco84/decovid-19-client)
* [Backend-Core](https://github.com/vitoco84/decovid-19-core)

Project Kanban Board Repository:
* [Issue Tracker Board](https://github.com/users/vitoco84/projects/2)

## Dokumentation

### Ausgangslage
Das Covid-19 Zertifikat (QR-Code) ist auf unkonventionelle Weise encodet. Der Inhalt des QR-Codes enthält Informationen über die Impfung, Testergebnis und Angaben der Person. Die Spezifikationen sind von der Europäischen Kommission gegeben und öffentlich zugänglich. Das Ziel ist ein Nachbauen des Encoding-Prozess des Covid-19 Zertifikat. Die Entwicklung der Software bietet eine Offenlegung, wie die Covid-19 Zertifikate kodiert sind, mit dazugehöriger Dokumentation und eine Single-Page-Webanwendung, wo man das Covid-19 Zertifikat hochladen kann, Anzeigen und anschliessend daraus die kodierten Informationen abzuleiten. Das bedeutet, eine unabhängige Enkodierung und Validierung der Zertifikate, wo jeder Benutzer darauf Zugriff haben kann.

![Encoding Process](/../main/Files%20and%20Pictures/QR-Code-Encoding-Process.png)

### Geplantes Vorgehen
* Lesen des QR-Codes (Upload/Scan/Drag-and-Drop Image) und Decoden zu einem String.
* Der Inhalt muss mit "HC1:" anfangen (EU Dcc Certificate).
* Entfernen vom Header "HC1:".
* Base45 decoden.
* Decompress mit ZLIB um die COSE Nachricht zu erhalten.
* Deserialize die COSE Nachricht.
* Den Payload extrahieren um den CBOR Inhalt zu erhalten.
* CBOR Inhalt decoden.
* JSON Schema erhalten.

### Geplante Technologien und Vorgehensmodell
* Agile Software Development
* Java Spring Boot Application (Backend / API)
* Swagger UI (Visualize API Resourcen)
* TypeScript, HTML 5, CSS (Frontend / Angular Framework / Bootstrap)
* GitHub Repositories
* CI/CD mit GitHub Actions
* Integrations- und Unit-Tests
* Code Analysis mit SonarCloud
* Application Security mit Snyk

#### Spring Boot
Spring Boot ist ein Open-Source Framework auf Java-Basis, das zur Erstellung von Micro Services verwendet wird.

#### Angular
Angular ist eine Entwicklungsplattform, die auf TypeScript basiert. Angular umfasst:
* Ein komponentenbasiertes Framework für die Erstellung skalierbarer Webanwendungen.
* Eine Sammlung gut integrierter Bibliotheken, die eine Vielzahl von Funktionen abdecken, darunter Routinrg, Formularverwaltung, Client-Server-Kommunikation und mehr.
* Eine Reihe von Entwicklertools für das Erstellen, Testen und Aktualsieren des Codes.

#### Bootstrap
Bootstrap ist ein kostenloses Frontend Framework für eine schnellere und einfachere Webentwicklung. Bootstrap umfasst:
* HTML- und CSS-basierte Designvorlagen für Typografie, Formulare, Schaltflächen, Tabellen, Navigation, Modals, Bildkarusselle und vieles mehr.
* Optionale JavaScript Plugins.
* Es ermöglicht auch die einfache Erstellung von responsiven Designs.

#### Swagger UI
Swagger UI ermöglicht es jedem, sei es das Entwicklungsteam oder den Endverbraucher, die API-Ressourcen zu visualisieren und mit ihnen zu interagieren, ohne dass die Implementierungslogik vorhanden ist. Sie wird automatisch aus der OpenAPI-Spezifikation generiert, wobei die visuelle Dokumentation die Backend-Implementierung und die Nutzung auf der Client-Seite erleichtert.

### Snyk
Snyk ist eine Sicherheitsplattform für Entwickler zur Sicherung von Code, Abhängigkeiten, Containern und Infrastruktur als Code. Es erlaubt das automatische Finden von Schwachstellen im Code.

### User Story
Als Benutzer möchte man ein Covid-19 QR-Code Zertifikat als Bild hochladen können und als nächster Schritt die Informationen die im QR-Code enthalten sind auswerten und im Browser darstellen können. Den Inhalt soll als raw Format (JSON-Schema) und als user-friendly Format dargestellt werden. Als Benutzer möchte man das Verfahren verstehen, wie das Covid-19 Zertifikat kodiert ist. Zusätzlich möchte man als Benutzer überprüfen können, ob es sich um ein valides Covid Zertifikat handelt.

### Anforderungen
* Testabdeckung durch Unit-Tests.
* Clean Code und Anwendung von SOLID Principles.
* Einfach zu bedienendes und verständliches UI für den Benutzer (Browser Navigation und Verständlichkeit).
* Logging und Fehlermeldung (File Persistierung).
* Application Security.
* Keine sensitive Daten von Benutzern persistieren oder loggen.

### Randbedingungen und Einschränkungen
Es ist noch nicht sichergestellt, ob alle Daten für die Validierung des Zertifikates (Schweiz) öffentlich zugänglich sind, so dass auch eine offline Validierung möglich ist, ohne ein exteren Schnittstelle zu benutzen.

### Funktionale- und Nicht Funktionale-Anforderungen

### Kriterien für die Akzeptanz

### Use-Cases

**Use-Case 1:**\
Covid-19 Zertifikat QR-Code Upload via Button.\
Als Benutzer möchte man ein Covid-19 Zertifikat als QR-Code im Browser hochladen können via Button click.

**Use-Case 2:**\
Covid-19 Zertifikat QR-Code Upload via Drag and Drop.\
Als Benutzer möchte man ein Covid-19 Zertifikat als QR-Code im Browser via Drag and Drop hochladen können.

**Use-Case 3:**\
Covid-19 Zertifikat QR-Code Upload via Scanning.\
Als Benutzer möchte man ein Covid-19 Zertifikat als QR-Code im Browser mit der Kamera des Computers hochladen können.

**Use-Case 4:**\
Covid-19 Zertifikat Inhalt Anzeigen.\
Als Benutzer möchte man den kodierten Inhalt des QR-Codes im Browser anzeigen lassen können. Der Inhalt soll in einem User Friendly Format und als Raw Format angezeigt werden können.
* Certification Type
* Schema Version
* Vorname
* Nachname
* Geburtstag
* Unique Certificate Identifier (UVCI)
* Dose Number
* Total Series of Doses
* Date of Vaccination
* Vaccine
* Vaccine Medicinal Product
* Vaccine Manufacturer
* Disease or Agent Targeted
* Country of Vaccination
* Certificate Issuer

**Use-Case 5:**\
Covid-19 Zertifikat Signature Details Anzeigen.\
Als Benutzer möchte man die Signatur Details des QR-Codes anzeigen lassen können.
* Algorithm
* Key Identifier (KID)
* Signer

**Use-Case 6:**\
Covid-19 Zertifikat Inhalt Anzeige ändern.\
Als Benutzer möchte man den Inhalt des QR-Codes der im Browser dargestellt wird anderst anzeigen können, als:
* JSON Schema (Raw Format)
* Human Readable Format

**Use-Case 7:**\
Covid-19 Zertifikat QR-Code Verifizieren.\
Als Benutzer möchte man den QR-Code im Browser auf Gültikeit verifizieren können.

### Sequenz Diagramme
![Sequence Diagram](/../main/Files%20and%20Pictures/Sequence-Diagram.png)

### Testing
Testabdeckung durch Unit-Tests.

### Architektur und Design
![Architecture](/../main/Files%20and%20Pictures/Architecture.png)

### Detail Beschreibung

### Fehlerbehandlung

### Performance

### Security
Die Sicherheit der Software wird nach best practices sichergestellt, und mit der Berücksichtigung der [OWASP Top 10](https://owasp.org/Top10/) (The Open Web Application Security Project).

### Git Flow Strategy
GitHub Flow with main and feature branches, to keep the main code in a constant deployable state and hence support continuous integration and continuous delivery process.
![GitHub Flow](/../main/Files%20and%20Pictures/GitHub-Flow-Strategy.png)

### Prototype User Interface / Usability
![UI Prototype](/../main/UX%20Design/decovid-19-prototype-layout.png)

### Prioritäten

#### Prio 1:
* Single-Page-Webanwendung
* API
* Covid-19 QR-Code Zertifikat hochladen
* Covid-19 QR-Code Zertifikat previewen
* Covid-19 QR-Code Zertifikat Inhalt encoden und im Browser Anzeigen oder über die API Resource beziehen

#### Prio 2:
* Covid-19 QR-Code Zertifikat Validuerung
* Dokumentation Page des Encoding / Decoding Prozess

#### Prio 3:
* Deployment
* Base45 Encoder / Decoder als separates feature

### Useful Covid-19 Certificate Related Links
* [EHN DCC Test Data](https://github.com/ehn-dcc-development/dcc-testdata)
* [Swiss Covid Certificate Examples](https://github.com/admin-ch/CovidCertificate-Examples)
* [Guidelines on Values Sets for Digital Green Certificates](https://ec.europa.eu/health/system/files/2021-04/digital-green-certificates_dt-specifications_en_0.pdf)
* [Digital Covid Certificate Schema](https://github.com/eu-digital-green-certificates/ehn-dgc-schema)
* [Covid Certificate Apps Android](https://github.com/admin-ch/CovidCertificate-App-Android)
* [Covid Certificate SDK Android](https://github.com/admin-ch/CovidCertificate-SDK-Android)
* [Covid Certificate API Gateway Service](https://github.com/admin-ch/CovidCertificate-Api-Gateway-Service)
* [EU Digital Green Certificate DGC Gateway](https://github.com/eu-digital-green-certificates/dgc-gateway)
* [Covid Certificate API Doc](https://github.com/admin-ch/CovidCertificate-Apidoc)

### Useful Technology Documentation Related Links
* [Spring Boot](https://spring.io/projects/spring-boot#overview)
* [Angular](https://angular.io/guide/what-is-angular)
* [Bootstrap](https://getbootstrap.com/docs/5.1/getting-started/introduction/)
* [Swagger UI](https://swagger.io/tools/swagger-ui/)
* [Sonarcloud](https://sonarcloud.io/)
* [Snyk](https://snyk.io/)

### Appendix / Disclaimer
Alle hier veröffentlichten Bilder enthalten keine expliziten Informationen über reale Personen. Alle Bilder sind öffentlich zugänglich oder von Testdaten abgeleitet.
