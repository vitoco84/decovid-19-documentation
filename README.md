# Decovid-19 Documentation

## Project Related Repositories

Project Repositories:
* [Frontent-Client](https://github.com/vitoco84/decovid-19-client)
* [Backend-Core](https://github.com/vitoco84/decovid-19-core)

Project Kanban Board Repository:
* [Issue Tracker Board](https://github.com/users/vitoco84/projects/2)

## Documentation

### Ausgangslage
Das Covid-19 Zertifikat (QR-Code) ist auf unkonventionelle Weise encodet. Der Inhalt des QR-Codes enthält Informationen über die Impfung, Testergebnis und Angaben der Person. Die Spezifikationen sind von der Europäischen Kommission gegeben und öffentlich zugänglich. Das Ziel ist ein Nachbauen des Encoding-Prozess des Covid-19 Zertifikat. Die Entwicklung der Software bietet eine Offenlegung, wie die Covid-19 Zertifikate kodiert sind, mit dazugehöriger Dokumentation und eine Single-Page-Webanwendung, wo man das Covid-19 Zertifikat hochladen kann, Anzeigen und anschliessend daraus die kodierten Informationen abzuleiten. Das bedeutet, eine unabhängige Enkodierung und Validierung der Zertifikate, wo jeder Benutzer darauf Zugriff haben kann.

![Encoding Process](/../main/Files%20and%20Pictures/QR-Code-Encoding-Process.png)

### Geplantes Vorgehen
* Lesen des QR-Codes (Upload/Scan/Drag-and-Drop Image) und Decoden zu einem String.
* Der Inhalt muss mit "HC1:" anfangen.
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
* TypeScript, HTML 5, CSS (Fronten / Angular Framework)
* GitHub Repositories
* CI/CD mit GitHub Actions
* Integrations- und Unit-Tests
* Application Security and Code Analysis mit SonarCloud

### User Story
Als Benutzer möchte man ein Covid-19 QR-Code Zertifikat als Bild hochladen können und als nächster Schritt die Informationen die im QR-Code enthalten sind auswerten und im Browser darstellen können. Den Inhalt soll als raw Format (JSON-Schema) und als user-friendly Format dargestellt werden. Als Benutzer möchte man das Verfahren verstehen, wie das Covid-19 Zertifikat kodiert ist. Zusätzlich möchte man als Benutzer überprüfen können, ob es sich um ein valides Covid Zertifikat handelt.

### Anforderungen
* Testabdeckung durch Unit- und Integration-Tests.
* Clean Code und Anwendung von SOLID Principles.
* Einfach zu bedienendes und verständliches UI für den Benutzer (Browser Navigation und Verständlichkeit).
* Logging und Fehlermeldung (File Persistierung).
* Application Security.
* Keine sensitive Daten von Benutzern persistieren oder loggen.

### Randbedingungen und Einschränkungen
Es ist noch nicht sichergestellt, ob alle Daten für die Validierung des Zertifikates (Schweiz) öffentlich zugänglich sind, so dass auch eine offline Validierung möglich ist, ohne ein exteren Schnittstelle zu benutzen.

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

### Architektur und Design
![Architecture](/../main/Files%20and%20Pictures/Architecture.png)

### Detail Beschreibung

### Fehlerbehandlung

### Performance

### Security

### Prototype User Interface / Usability
![UI Prototype](/../main/UX%20Design/decovid-19-prototype-layout.png)

### Useful Links
* [Test Data](https://github.com/ehn-dcc-development/dcc-testdata)
* [Guidelines on Values Sets for Digital Green Certificates](https://ec.europa.eu/health/system/files/2021-04/digital-green-certificates_dt-specifications_en_0.pdf)
* [Digital Covid Certificate Schema](https://github.com/eu-digital-green-certificates/ehn-dgc-schema)

### Appendix / Disclaimer
All images published here do not contain explicit information of real persons. All images are publicly available or are derived from test data.
