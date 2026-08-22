# Oracle Siebel (oracle-siebel)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Oracle Siebel CRM APIs provide programmatic access to customer relationship management functionality including sales, marketing, and service automation capabilities. Siebel CRM offers REST, SOAP, scripting, and event-driven integration interfaces for building integrations with enterprise systems.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/oracle-siebel/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/oracle-siebel/refs/heads/main/apis.yml)

## Scope

- **Type:** Index
- **Position:** Consumer
- **Access:** 3rd-Party

## Tags

- CRM
- Customer Management
- Enterprise Software
- Marketing Automation
- Oracle
- Sales Automation
- Service Automation

## Timestamps

- **Created:** 2024-01-01
- **Modified:** 2026-04-28

## APIs

### Oracle Siebel REST API

RESTful API for accessing Siebel business objects, business services, and repository objects. The Siebel REST API supports standard CRUD operations using HTTP verbs (GET, POST, PUT, DELETE) and is compatible with OpenAPI 3.0 specifications for integration with modern applications and mobile devices.

- **Human URL:** [https://docs.oracle.com/cd/E95904_01/books/RestAPI/overview-of-using-the-siebel-rest-api.html](https://docs.oracle.com/cd/E95904_01/books/RestAPI/overview-of-using-the-siebel-rest-api.html)
- **Base URL:** `https://{siebel-server}/siebel/v1.0`

#### Tags

- CRM
- Customer Management
- Integration
- REST
- Sales

#### Properties

- [Documentation](https://docs.oracle.com/cd/E95904_01/books/RestAPI/overview-of-using-the-siebel-rest-api.html)
- [OpenAPI](https://{siebel-server}/siebel/v1.0/swagger.json) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Authentication](https://docs.oracle.com/cd/F26413_26/books/Secur/single-sign-on-authentication.html)
- [Getting Started](https://docs.oracle.com/cd/E95904_01/books/RestAPI/getting-started-with-the-siebel-rest-api.html)

### Oracle Siebel SOAP Web Services

SOAP-based web services for enterprise integration with Siebel CRM, supporting complex business operations and workflows. Siebel provides both inbound web services for external clients to access Siebel functionality and outbound web services for Siebel to call external applications.

- **Human URL:** [https://docs.oracle.com/cd/F26413_08/books/CRMWeb/siebel-crm-web-services-overview.html](https://docs.oracle.com/cd/F26413_08/books/CRMWeb/siebel-crm-web-services-overview.html)
- **Base URL:** `https://{siebel-server}/siebel/app/soap/services`

#### Tags

- CRM
- Enterprise Integration
- SOAP
- Web Services

#### Properties

- [Documentation](https://docs.oracle.com/cd/F26413_08/books/CRMWeb/siebel-crm-web-services-overview.html)
- [W S D L](https://{siebel-server}/siebel/app/soap/services?WSDL)
- [Reference](https://docs.oracle.com/cd/F26413_16/books/CRMWeb/crm-web-services-reference.pdf)

### Oracle Siebel Business Service API

APIs for creating and consuming custom business services within the Siebel platform for specialized business logic. Business services encapsulate reusable business logic that can be invoked through scripting, workflows, REST, or SOAP interfaces.

- **Human URL:** [https://docs.oracle.com/cd/F26413_13/books/OIRef/siebel-object-interfaces-reference.html](https://docs.oracle.com/cd/F26413_13/books/OIRef/siebel-object-interfaces-reference.html)

#### Tags

- Business Services
- Custom Logic
- Integration

#### Properties

- [Documentation](https://docs.oracle.com/cd/F26413_13/books/OIRef/siebel-object-interfaces-reference.html)

### Oracle Siebel EAI (Enterprise Application Integration)

Integration services for connecting Siebel with external systems using various protocols and data formats. Siebel EAI provides bidirectional, real-time, and batch integration solutions with pre-built adapters, enterprise connectors, and support for XML, HTTP, IBM MQSeries, and MSMQ transports.

- **Human URL:** [https://docs.oracle.com/cd/F26413_25/books/EAI1/overview-of-siebel-eai.html](https://docs.oracle.com/cd/F26413_25/books/EAI1/overview-of-siebel-eai.html)

#### Tags

- Data Exchange
- EAI
- Integration
- Middleware

#### Properties

- [Documentation](https://docs.oracle.com/cd/F26413_25/books/EAI1/overview-of-siebel-eai.html)
- [Reference](https://docs.oracle.com/cd/F26413_32/books/EAI2/toc.htm)

### Oracle Siebel Object Interfaces API

Programmatic interfaces for accessing Siebel business objects, business components, and application objects using Siebel eScript, Siebel Visual Basic, or the Siebel Java Data Bean. The Object Interfaces API provides methods for querying, inserting, updating, and deleting records, as well as invoking business services and managing application state.

- **Human URL:** [https://docs.oracle.com/cd/F26413_13/books/OIRef/siebel-object-interfaces-reference.html](https://docs.oracle.com/cd/F26413_13/books/OIRef/siebel-object-interfaces-reference.html)

#### Tags

- Business Components
- Java Data Bean
- Object Interfaces
- Scripting

#### Properties

- [Documentation](https://docs.oracle.com/cd/F26413_13/books/OIRef/siebel-object-interfaces-reference.html)
- [Reference](https://docs.oracle.com/cd/F26413_25/books/EAI3/integrating-siebel-crm-with-java-applications.html)

### Oracle Siebel Open UI JavaScript API

Client-side JavaScript API for customizing the Siebel Open UI user interface. The API provides well-defined customization points for styling, layout, and user interface design, allowing developers to integrate Siebel Open UI objects such as views and applets into third-party user interfaces and include external content in the Siebel Open UI client.

- **Human URL:** [https://docs.oracle.com/cd/F26413_26/books/ConfigOpenUI/configuring-siebel-open-ui-guide.pdf](https://docs.oracle.com/cd/F26413_26/books/ConfigOpenUI/configuring-siebel-open-ui-guide.pdf)

#### Tags

- Customization
- JavaScript
- Open UI
- User Interface

#### Properties

- [Documentation](https://docs.oracle.com/cd/F26413_26/books/ConfigOpenUI/configuring-siebel-open-ui-guide.pdf)
- [Reference](https://docs.oracle.com/cd/F26413_17/books/DeployOpenUI/features-of-siebel-open-ui.html)

### Oracle Siebel Event Pub/Sub API

Event-driven integration framework enabling real-time communication between Siebel CRM and external systems using Apache Kafka. The Event Pub/Sub API supports publishing events from Siebel to Kafka topics and consuming events from Kafka into Siebel, with support for Avro serialization, OAuth 2.0 security, and Kafka partitioning for scalability.

- **Human URL:** [https://docs.oracle.com/cd/F26413_50/books/SystAdm/c-Overview-of-Siebel-CRM-Event-Publication-and-Subscription.html](https://docs.oracle.com/cd/F26413_50/books/SystAdm/c-Overview-of-Siebel-CRM-Event-Publication-and-Subscription.html)

#### Tags

- Event-Driven
- Kafka
- Pub/Sub
- Real-Time Integration

#### Properties

- [Documentation](https://docs.oracle.com/cd/F26413_50/books/SystAdm/c-Overview-of-Siebel-CRM-Event-Publication-and-Subscription.html)

## Common Properties

- [Portal](https://docs.oracle.com/cd/G15000_01/SiebelInfoPortal/)
- [Website](https://www.oracle.com/applications/siebel/)
- [Documentation](https://docs.oracle.com/en/applications/siebel/)
- [Getting Started](https://docs.oracle.com/cd/F26413_61/books/FundOUI/index.html)
- [Authentication](https://docs.oracle.com/cd/F26413_26/books/Secur/single-sign-on-authentication.html)
- [Security](https://docs.oracle.com/cd/F26413_26/books/Secur/index.html)
- [Support](https://www.oracle.com/support/premier/software/siebel/)
- [Community](https://community.oracle.com/customerconnect/categories/onprem-siebel-crm)
- [Blog](https://blogs.oracle.com/siebelcrm/)
- [Changelog](https://docs.oracle.com/cd/F26413_61/homepage.htm)
- [Training](https://learn.oracle.com/ols/home/38497)
- [Terms of Service](https://www.oracle.com/legal/terms.html)
- [Privacy Policy](https://www.oracle.com/legal/privacy/)
- [Status Page](https://ocistatus.oraclecloud.com/)
- [Login](https://support.oracle.com/)
- [GitHub Organization](https://github.com/OracleSiebel)
- [GitHub Repository](https://github.com/OracleSiebel/ConfiguringSiebel)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
