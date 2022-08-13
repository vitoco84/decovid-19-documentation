# Decovid-19 Documentation

- [Decovid-19-Logo](#logo)
- [Project Related Repositories](#project-related-repos)
- [Documentation](#dokumentation)
  - [Initial Situation](#ausgangslage)
  - [Planned Approach](#geplantes-vorgehen)
  - [Planned Technologies](#geplante-technologien)
  - [User Story](#user-story)
  - [Requirements](#anforderungen)
  - [Boundary Conditions and Constraints](#randbedingungen)
  - [Functional and Non-Functional Requirements](#anforderungen-funk-nicht)
  - [Use-Cases](#use-cases)
  - [Sequence Diagrams](#sequenz-diagramm)
  - [Architecture and Design](#architektur)
  - [Detail Description Electronic Health Certificate](#hcert)
  - [Security](#security)
  - [Git Flow Strategy](#git-flow)
  - [Prototype User Interface / Usability](#prototyp-layout)
  - [Priorities](#prioritaeten)
  - [Acronyms](#akronyme)
  - [Useful Covid-19 Certificate Related Links](#covid19-links)
  - [Useful Technology Documentation Related Links](#technologien-links)
  - [Useful Formatting / Decoding Links](#formatting-links)
  - [Appendix / Disclaimer](#appendix)

<a name="logo"></a>
## Decovid-19-Logo
![Decovid-19-Logo](/../main/UX%20Design/decovid-19-logo.png)

Created with [Inkscape](https://inkscape.org/)

<a name="project-related-repos"></a>
## Project Related Repositories

Project Repositories:
* [Frontend-Client](https://github.com/vitoco84/decovid-19-client)
* [Backend-Core](https://github.com/vitoco84/decovid-19-core)

Project Kanban Board Repository:
* [Issue Tracker Board](https://github.com/users/vitoco84/projects/2)

<a name="dokumentation"></a>
## Documentation

<a name="ausgangslage"></a>
### Initial Situation
The Covid-19 certificate (QR code) is encoded in an unconventional way. The content of the QR code contains information about the vaccination, test result and specifications of the person. The specifications are given by the European Commission and are publicly available. The goal is to replicate the decoding process of the Covid-19 certificate. The development of the software provides a disclosure of how the Covid-19 certificates are encoded, with associated documentation and a single-page web application where one can upload the Covid-19 certificate, view its contents and then derive the encoded information from it. This means independent decoding and validation of the certificates, where every user can have access to them. For validation, the focus is on the Covid-19 certificates of Switzerland.


![Encoding Process](/../main/Files%20and%20Pictures/QR-Code-Encoding-Process.png)

<a name="geplantes-vorgehen"></a>
### Planned Procedure
* Reading the QR code (upload/scan/drag-and-drop image) and decoding it to a String.
* The content must start with "HC1:" (EU DCC Certificate).
* Remove from header "HC1:".
* Decode Base45.
* Decompress with ZLIB to get the COSE message.
* Deserialize the COSE message.
* Extract the payload to get the CBOR content.
* Decode the CBOR content.
* Obtain JSON schema.

<a name="geplante-technologien"></a>
### Planned Technologies and Procedure Model
* Agile Software Development
* Java Spring Boot Application (Backend / API)
* Swagger UI (Visualize API Resourcen)
* TypeScript, HTML 5, CSS (Frontend / Angular Framework / Bootstrap)
* GitHub Repositories
* CI/CD mit GitHub Actions
* Unit-Tests
* Code Analysis mit SonarCloud
* Application Security with Snyk

#### Spring Boot
Spring Boot is an open-source Java-based framework used to create micro services.

#### Angular
Angular is a development platform based on TypeScript. Angular includes:
* A component-based framework for building scalable web applications.
* A collection of well-integrated libraries that cover a wide range of functions, including routing, form management, client-server communication, and more.
* A set of developer tools for building, testing, and updating code.

#### Bootstrap
Bootstrap is a free frontend framework for faster and easier web development. Bootstrap includes:
* HTML and CSS based design templates for typography, forms, buttons, tables, navigation, modals, image carousels and much more.
* Optional JavaScript plugins.
* It also allows you to easily create responsive designs.

#### Swagger UI
Swagger UI allows anyone, be it the development team or the end user, to visualize and interact with API resources without the implementation logic. It is automatically generated from the OpenAPI specification, with visual documentation facilitating back-end implementation and client-side usage.

#### Snyk
Snyk is a security platform for developers to secure code, dependencies, containers and infrastructure as code. It allows finding vulnerabilities in code automatically.

<a name="user-story"></a>
### User Story
As a user you want to be able to upload a Covid-19 QR code certificate as an image and as a next step evaluate the information contained in the QR code and display it in the browser. The content should be displayed as raw format (JSON schema) and as user-friendly format. As a user, you want to understand the process of how the Covid-19 certificate is encoded. Additionally, as a user, you want to be able to verify that it is a valid Covid certificate.

<a name="anforderungen"></a>
### Requirements
* Test coverage through Unit- and Integrationtets.
* Clean code and application of SOLID Principles.
* Easy to use and understandable UI for the user (browser navigation and comprehensibility).
* Logging und Error Reporting.
* Application Security.
* Do not persist or log sensitive user data.

<a name="randbedingungen"></a>
### Boundary Conditions and Restrictions
It is not yet ensured whether all data for the validation of the certificate (Switzerland) is publicly available, so that offline validation is also possible without using an external interface.

<a name="anforderungen-funk-nicht"></a>
### Functional and Non-Functional Requirements

#### Functional Requirements
* The application must be able to decode the QR code / Covid-19 certificate and display its contents.
* The application must be able to check the QR code / Covid-19 certificate for its validation.
* The application must provide an API.

#### Non-Functional Requirements
* The application shall not persist sensitive personal data.
* The application shall have a user-friendly UI.
* The application shall be available as an open source project.

<a name="use-cases"></a>
### Use-Cases

**Use-Case 1:**\
Covid-19 certificate content display.\
As a user, you want to be able to display the encoded content of the QR code in the browser. The content should be displayed in a user friendly format and as raw json format. In addition, it should be possible to upload the image of the QR code in the browser via button click and drag and drop.
* Certificate Type
* Schema Version
* Firstname
* Lastname
* Birthday
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

**Use-Case 2:**\
Covid-19 Certificate Signature Details Display.\
As a user, one would like to be able to view the signature details of the QR code.
* Algorithm
* Key Identifier (KID)
* Signer

**Use-Case 3:**\
Covid-19 certificate content display change.\
As a user, you want to be able to display the content of the QR code displayed in the browser differently:
* JSON Schema (Raw Format)
* Human Readable Format

**Use-Case 4:**\
Covid-19 certificate QR code verification.\
As a user, you want to be able to verify the validity of the QR code in the browser.

**Use-Case 5:**\
Create Covid-19 test certificate QR code.\
As a user, one would like to be able to create a fakes test certificate.

**Use-Case 6:**\
View PEM formatted digital certificate content.\
As a user, one would like to be able to view the content of PEM formatted digital certificates in the browser.

**Use-Case 7:**\
Step-by-step instructions on how to encode and decode a Covid-19 certificate.\
As a user, you want to learn how to encode and decode Covid-19 certificates (Documentation Page).

<a name="sequenz-diagramm"></a>
### Sequence Diagrams

#### Decode Digital Health Certificate
![Sequence Diagram Decode](/../main/Files%20and%20Pictures/Sequence-Diagram-Decode.png)

#### Create a Fake Test Health Certificate
![Sequence Diagram Test Cert](/../main/Files%20and%20Pictures/Sequence-Diagram-Test-Cert.png)

#### Decode Digitial X509 Certificate
![Sequence Diagram PEM Cert](/../main/Files%20and%20Pictures/Sequence-Diagram-PEM-Cert.png)

<a name="architektur"></a>
### Architecture and Design

* 2-Tier Architecture with:
  * Presentation Layer (client tier)
  * Logic Layer (application-server tier)

![Architecture](/../main/Files%20and%20Pictures/Architecture.png)

<a name="hcert"></a>
### Detail Description Electronic Health Certificate
The user data is structured and encoded as a CBOR with a digital COSE signature. This is commonly referred to as a CBOR Web Token (CWT) and is defined in [RFC 8392](https://datatracker.ietf.org/doc/html/rfc8392). The payload is transported in a hcert (JSON [RFC 7159](https://datatracker.ietf.org/doc/html/rfc7159) object containing the health state information) claim. It must be possible for the verifier to verify the integrity and authenticity of the origin of the payload. To provide this mechanism, the issuer must sign the CWT using an asymmetric electronic signature scheme as defined in the COSE specification ([RFC 8152](https://datatracker.ietf.org/doc/html/rfc8152)). To reduce the size and improve the speed and reliability of reading the hcert, the CWT shall be compressed using ZLib ([RFC 1950](https://datatracker.ietf.org/doc/html/rfc1950)) and the deflate compression mechanism in the format defined in ([RFC 1951](https://datatracker.ietf.org/doc/html/rfc1951)). To better deal with older equipment designed for ASCII payloads, the compressed CWT has been encoded as ASCII using Base45 before being converted to a 2D barcode.

#### CWT Claim Structure
* Protected Header
  * Signature Algorithm (`alg`, label 1)
  * Key Identifier (`kid`, label 4)
* Payload
  * Issuer (`iss`, claim key 1, optional, ISO 3166-1 alpha-2 of issuer)
  * Issued At (`iat`, claim key 6)
  * Expiration Time (`exp`, claim key 4)
  * Health Certificate (`hcert`, claim key -260)
    * EU Digital Covid Certificate v1 (`eu_dcc_v1` aka `eu_dgc_v1`, claim key 1)
* Signature

#### Base45 Data Encoding
A QR code is used to encode text as a graphical image. Depending on the characters used in the text, there are different encoding options for a QR code. E.g. numeric, alphanumeric and bytes-mode. This means that such data must be converted into a suitable text before this text can be encoded as a QR code. For the Covid certificate, a 45 character subset of ASCII (American Standard Code for Information Interchange) is used.

#### ZLib
ZLib is a software library for compressing and decompressing data using the Deflate algorithm (lossless data compression).

#### Concise Binary Object Representation (CBOR)
CBOR is a binary compact data format whose design goals are the possibility of an extremely small code size, a relatively small message size and extensibility without the need for version handling. The underlying data model is an extended version of the JSON data model. It increases processing and transmission speed at the expense of readability. It is the data format on which COSE messages are based.

#### CBOR Object Signing and Encyption (COSE)
COSE specifies how encryption, signatures and message authentication code (MAC) operations are to be processed and how the keys can be encoded using CBOR. Thus, a signed binary data format. The basic structure of a COSE message consists of 2 information areas (Protected and Unprotected header) and the payload of the message. There are 6 different COSE messages. The COSE message used for the Covid certificate is of type `Sign1Message`. This means it contains a signature in bytes. In order to validate the Covid certificate, the validators must implicitly know the public key to verify the message, since no additional key information is transmitted.

#### Requirements on TLS (Transport Layer Security), Upload and CSCA (Swiss Country Signing Certification Authority)
For digital certificates and cryptographic signatures in the DCCG (Digital Covid Certificate Gateway) account text, the most important requirements for cryptographic algorithms and key lengths are summarized as follows:

| Signature Algorithm | Key Size | Hash Function |
|---------------------|----------|---------------|
| EC-DSA | Min. 250 Bit | SHA-2 with an output length >= 256 Bit |
| RSA-PSS (recommended padding) | Min. 3000 Bit RSA Modulus (N) with a public exponent e > 2^16 | SHA-2 with an output length >= 256 Bit |
| RSA-PKCS#1 v1.5 (legacy padding) | Min. 3000 Bit RSA Modulus (N) with a public exponent e > 2^16 | SHA-2 with an output length >= 256 Bit |
| DSA | Min. 3000 Bit prime p, 250 Bit key q | SHA-2 with an output length >= 256 Bit |

#### Covid Certificate Verification Rules
* Does the certificate contain a valid electronic signature?
* Has the certificate definitely not been revoked?
* Does the certificate meet the applicable validity rules (business rules)?

#### Digital Certificates
Digital certificates contain certain information specified by the X.509 [RFC 2459](https://www.ietf.org/rfc/rfc2459.txt) standard.

Digital certificates contain at least the following information about the authority being certified:
* The public key of the holder
* The name of the holder
* The name of the CA (Certificate Authority) that issued the certificate
* The date from which the certificate is valid
* The expiration date of the certificate
* The version number of the certificate data format as defined in X.509 (default is version 3)
* A serial number, a unique identifier assigned by the CA
* An issuer identifier
* A subject identifier

The digital signature in a certificate is generated using the private key of the CA that signed the certificate. Anyone who needs to verify the personal certificate can use the CA's public key to do so. The CA's certificate contains its public key.

Digital certificates do not contain their private key. They must keep their private key secret.

<a name="security"></a>
### Security
The security of the software is ensured according to best practices, and with the consideration of the [OWASP Top 10](https://owasp.org/Top10/) (The Open Web Application Security Project).

<a name="git-flow"></a>
### Git Flow Strategy
GitHub Flow with main and feature branches to keep the main code in a constant, deployable state to support continuous integration and continuous deployment process.

![GitHub Flow](/../main/Files%20and%20Pictures/GitHub-Flow-Strategy.png)

<a name="prototyp-layout"></a>
### Prototype User Interface / Usability
![UI Prototype](/../main/UX%20Design/decovid-19-prototype-layout-diagrams.png)

<a name="prioritaeten"></a>
### Priorities

#### Prio 1:
* Single Page Web-Application
* API Interface (Swagger UI)
* Upload Covid-19 QR code certificate
* Preview Covid-19 QR code certificate
* Covid-19 QR code certificate content decode and display in browser or get from API resource

#### Prio 2:
* Covid-19 QR code certificate validation
* PEM Digital Certificates Show content
* Documentation page of the encoding/decoding process

#### Prio 3:
* Deployment
* Base45 encoder/decoder as separate feature

<a name="akronyme"></a>
### Acronyms
* DSA: Digital Signature Algorithm
* ECDSA: Elliptic Curve Digital Signature Algorithm
* PKCS: Public Key Cryptography Standard
* RSA: Algorithm developed by Rives, Shamir and Adleman
* SHA: Secure Hash Algorithm

<a name="covid19-links"></a>
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
* [Electronic Health Certificate Specifications](https://github.com/ehn-dcc-development/hcert-spec/blob/main/hcert_spec.md)
* [Value Sets Covid Certificate JSON Schema ](https://github.com/ehn-dcc-development/ehn-dcc-valuesets)
* [Technical Specifications for EU Digital COVID Certificates](https://ec.europa.eu/health/publications/technical-specifications-eu-digital-covid-certificates-volumes-1-5_en)

<a name="technologien-links"></a>
### Useful Technology Documentation Related Links
* [Spring Boot](https://spring.io/projects/spring-boot#overview)
* [Angular](https://angular.io/guide/what-is-angular)
* [Bootstrap](https://getbootstrap.com/docs/5.1/getting-started/introduction/)
* [Swagger UI](https://swagger.io/tools/swagger-ui/)
* [Sonarcloud](https://sonarcloud.io/)
* [Snyk](https://snyk.io/)

<a name="formatting-links"></a>
### Useful Formatting / Decoding Links
* [X.509 Fromatter](https://www.samltool.com/format_x509cert.php)
* [PEM Decoder](https://report-uri.com/home/pem_decoder)

<a name="appendix"></a>
### Appendix / Disclaimer
All images published here do not contain explicit information about real people. All images are in the public domain or derived from test data.
