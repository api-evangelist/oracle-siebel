# Oracle Siebel (oracle-siebel)

Oracle Siebel CRM APIs provide programmatic access to customer relationship management functionality including sales, marketing, and service automation capabilities. Siebel CRM offers REST, SOAP, scripting, and event-driven integration interfaces for building integrations with enterprise systems.

**URL:** [Visit APIs.json URL](https://raw.githubusercontent.com/api-evangelist/oracle-siebel/refs/heads/main/apis.yml)

## Tags

- CRM, Customer Management, Enterprise Software, Marketing Automation, Oracle, Sales Automation, Service Automation

## Timestamps

- **Created:** 2024-01-01
- **Modified:** 2026-04-28

## APIs

### Oracle Siebel REST API

RESTful API for accessing Siebel business objects, business services, and repository objects. The Siebel REST API supports standard CRUD operations using HTTP verbs (GET, POST, PUT, DELETE) and is compatible with OpenAPI 3.0 specifications for integration with modern applications and mobile devices.

**Human URL:** [https://docs.oracle.com/cd/E95904_01/books/RestAPI/overview-of-using-the-siebel-rest-api.html](https://docs.oracle.com/cd/E95904_01/books/RestAPI/overview-of-using-the-siebel-rest-api.html)

**Base URL:** `https://{siebel-server}/siebel/v1.0`

#### Tags

- CRM, Customer Management, Integration, REST, Sales

#### Properties

- [Documentation](https://docs.oracle.com/cd/E95904_01/books/RestAPI/overview-of-using-the-siebel-rest-api.html)
- [OpenAPI](openapi/oracle-siebel-rest-api-openapi.yml)
- [Authentication](https://docs.oracle.com/cd/F26413_26/books/Secur/single-sign-on-authentication.html)
- [Getting Started](https://docs.oracle.com/cd/E95904_01/books/RestAPI/getting-started-with-the-siebel-rest-api.html)

### Oracle Siebel SOAP Web Services

SOAP-based web services for enterprise integration with Siebel CRM, supporting complex business operations and workflows. Siebel provides both inbound web services for external clients to access Siebel functionality and outbound web services for Siebel to call external applications.

**Human URL:** [https://docs.oracle.com/cd/F26413_08/books/CRMWeb/siebel-crm-web-services-overview.html](https://docs.oracle.com/cd/F26413_08/books/CRMWeb/siebel-crm-web-services-overview.html)

**Base URL:** `https://{siebel-server}/siebel/app/soap/services`

#### Tags

- CRM, Enterprise Integration, SOAP, Web Services

#### Properties

- [Documentation](https://docs.oracle.com/cd/F26413_08/books/CRMWeb/siebel-crm-web-services-overview.html)
- [WSDL](https://{siebel-server}/siebel/app/soap/services?WSDL)
- [Reference](https://docs.oracle.com/cd/F26413_16/books/CRMWeb/crm-web-services-reference.pdf)

### Oracle Siebel Business Service API

APIs for creating and consuming custom business services within the Siebel platform for specialized business logic. Business services encapsulate reusable business logic that can be invoked through scripting, workflows, REST, or SOAP interfaces.

**Human URL:** [https://docs.oracle.com/cd/F26413_13/books/OIRef/siebel-object-interfaces-reference.html](https://docs.oracle.com/cd/F26413_13/books/OIRef/siebel-object-interfaces-reference.html)

#### Tags

- Business Services, Custom Logic, Integration

#### Properties

- [Documentation](https://docs.oracle.com/cd/F26413_13/books/OIRef/siebel-object-interfaces-reference.html)

### Oracle Siebel EAI (Enterprise Application Integration)

Integration services for connecting Siebel with external systems using various protocols and data formats. Siebel EAI provides bidirectional, real-time, and batch integration solutions with pre-built adapters, enterprise connectors, and support for XML, HTTP, IBM MQSeries, and MSMQ transports.

**Human URL:** [https://docs.oracle.com/cd/F26413_25/books/EAI1/overview-of-siebel-eai.html](https://docs.oracle.com/cd/F26413_25/books/EAI1/overview-of-siebel-eai.html)

#### Tags

- Data Exchange, EAI, Integration, Middleware

#### Properties

- [Documentation](https://docs.oracle.com/cd/F26413_25/books/EAI1/overview-of-siebel-eai.html)
- [Reference](https://docs.oracle.com/cd/F26413_32/books/EAI2/toc.htm)

### Oracle Siebel Object Interfaces API

Programmatic interfaces for accessing Siebel business objects, business components, and application objects using Siebel eScript, Siebel Visual Basic, or the Siebel Java Data Bean. The Object Interfaces API provides methods for querying, inserting, updating, and deleting records, as well as invoking business services and managing application state.

**Human URL:** [https://docs.oracle.com/cd/F26413_13/books/OIRef/siebel-object-interfaces-reference.html](https://docs.oracle.com/cd/F26413_13/books/OIRef/siebel-object-interfaces-reference.html)

#### Tags

- Business Components, Java Data Bean, Object Interfaces, Scripting

#### Properties

- [Documentation](https://docs.oracle.com/cd/F26413_13/books/OIRef/siebel-object-interfaces-reference.html)
- [Reference](https://docs.oracle.com/cd/F26413_25/books/EAI3/integrating-siebel-crm-with-java-applications.html)

### Oracle Siebel Open UI JavaScript API

Client-side JavaScript API for customizing the Siebel Open UI user interface. The API provides well-defined customization points for styling, layout, and user interface design, allowing developers to integrate Siebel Open UI objects such as views and applets into third-party user interfaces and include external content in the Siebel Open UI client.

**Human URL:** [https://docs.oracle.com/cd/F26413_26/books/ConfigOpenUI/configuring-siebel-open-ui-guide.pdf](https://docs.oracle.com/cd/F26413_26/books/ConfigOpenUI/configuring-siebel-open-ui-guide.pdf)

#### Tags

- Customization, JavaScript, Open UI, User Interface

#### Properties

- [Documentation](https://docs.oracle.com/cd/F26413_26/books/ConfigOpenUI/configuring-siebel-open-ui-guide.pdf)
- [Reference](https://docs.oracle.com/cd/F26413_17/books/DeployOpenUI/features-of-siebel-open-ui.html)

### Oracle Siebel Event Pub/Sub API

Event-driven integration framework enabling real-time communication between Siebel CRM and external systems using Apache Kafka. The Event Pub/Sub API supports publishing events from Siebel to Kafka topics and consuming events from Kafka into Siebel, with support for Avro serialization, OAuth 2.0 security, and Kafka partitioning for scalability.

**Human URL:** [https://docs.oracle.com/cd/F26413_50/books/SystAdm/c-Overview-of-Siebel-CRM-Event-Publication-and-Subscription.html](https://docs.oracle.com/cd/F26413_50/books/SystAdm/c-Overview-of-Siebel-CRM-Event-Publication-and-Subscription.html)

#### Tags

- Event-Driven, Kafka, Pub/Sub, Real-Time Integration

#### Properties

- [Documentation](https://docs.oracle.com/cd/F26413_50/books/SystAdm/c-Overview-of-Siebel-CRM-Event-Publication-and-Subscription.html)
- [AsyncAPI](asyncapi/oracle-siebel-event-pubsub-asyncapi.yml)

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
- [Change Log](https://docs.oracle.com/cd/F26413_61/homepage.htm)
- [Training](https://learn.oracle.com/ols/home/38497)
- [Terms of Service](https://www.oracle.com/legal/terms.html)
- [Privacy Policy](https://www.oracle.com/legal/privacy/)
- [Status](https://ocistatus.oraclecloud.com/)
- [Login](https://support.oracle.com/)
- [GitHub Organization](https://github.com/OracleSiebel)
- [GitHub Repository](https://github.com/OracleSiebel/ConfiguringSiebel)
- [OpenAPI](openapi/oracle-siebel-rest-api-openapi.yml)
- [AsyncAPI](asyncapi/oracle-siebel-event-pubsub-asyncapi.yml)
- [JSON Schema](json-schema/oracle-siebel-account-schema.json)
- [JSON Schema](json-schema/oracle-siebel-contact-schema.json)

## Maintainers

- **FN:** Kin Lane
- **Email:** kin@apievangelist.com
