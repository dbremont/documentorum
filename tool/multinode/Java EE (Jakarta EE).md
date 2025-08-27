# Java EE (Jakarta EE)

> Java EE (Jakarta EE) is a specification-driven, enterprise-grade Java platform that defines a set of standardized APIs, runtime environments, and container-managed services for building distributed, scalable, and transactional applications, leveraging a component-based architecture with servlets, JSP, JSF, CDI, EJB, JPA, JMS, JTA, and web services (REST and SOAP) while enforcing dependency injection, declarative security, and multi-threaded request processing within managed execution environments such as application servers (e.g., WildFly, Payara, or **Tomcat with EE extensions**).
> 

| **Category** | **Technology/Specification** | **Description** |
| --- | --- | --- |
| **Web Tier** | **Jakarta Servlet** | Handles HTTP requests and responses, providing the foundation for web applications. |
|  | **Jakarta Server Pages** |  |
|  | **Jakarta Faces** | Simplifies building user interfaces for web applications (formerly JSF - JavaServer Faces). |
|  | **Jakarta Expression Language (EL)** | Provides a simple language for accessing and manipulating object properties in Java-based web apps. |
| **Web Services** | **Jakarta RESTful Web Services (JAX-RS)** | Simplifies development of REST APIs. |
|  | **Jakarta XML Web Services (JAX-WS)** | Enables SOAP-based web service development. |
|  | **Jakarta JSON Processing (JSON-P)** | Provides APIs for parsing, generating, and manipulating JSON data. |
|  | **Jakarta JSON Binding (JSON-B)** | Provides APIs for mapping Java objects to JSON and vice versa. |
| **Persistence** | **Jakarta Persistence (JPA)** | Simplifies database interaction by providing ORM (Object-Relational Mapping) functionality. |
|  | **Jakarta Data** | A newer addition to Jakarta EE, offering a more streamlined API for accessing relational databases. |
| **Enterprise Integration** | **Jakarta Messaging (JMS)** | Enables asynchronous communication via messaging systems. |
|  | **Jakarta Batch** | Supports batch processing of large data sets. |
|  | **Jakarta Mail** | Provides APIs for sending and receiving emails. |
|  | **Jakarta Concurrency** | Enables multithreaded programming in enterprise applications. |
| **Business Logic** | **Jakarta Enterprise Beans (EJB)** | Simplifies transactional and distributed business logic development. |
|  | **Jakarta CDI (Contexts and Dependency Injection)** | Provides a dependency injection framework for simplifying object management. |
|  | **Jakarta Interceptors** | Allows cross-cutting concerns (e.g., logging, auditing) to be handled via interceptors. |
| **Security** | **Jakarta Security** | Provides APIs for application-level security (authentication, authorization, etc.). |
| **Transaction Management** | **Jakarta Transactions (JTA)** | Enables transaction management for enterprise applications. |
|  | **Jakarta Connectors (JCA)** | Provides integration with enterprise information systems like ERPs and legacy systems. |
| **Configuration** | **Jakarta Annotations** | Provides standard annotations to simplify metadata-driven development. |
|  | **Jakarta Dependency Injection (DI)** | Ensures loose coupling between components through DI principles. |
| **Cloud & Microservices** | **Jakarta Config** | Offers centralized and dynamic configuration for microservices and cloud apps. |
|  | **Jakarta MVC** | A model-view-controller framework for building web apps (optional). |
|  | **Jakarta JSON Binding (JSON-B)** | Works well with cloud-native and microservices architectures for JSON data manipulation. |
| **Testing** | **Jakarta Bean Validation** | Ensures data integrity via annotations for bean validation. |
|  |  |  |

## Implementation

| **Jakarta EE Specification** | **Implementation** | **Provider** |
| --- | --- | --- |
| **Jakarta Servlet** | Apache Tomcat / Jetty | Apache Software Foundation |
| **Jakarta Server Pages (JSP)** | Jasper | Apache Software Foundation |
| **Jakarta Faces (JSF)** | Mojarra / MyFaces | Eclipse / Apache |
| **Jakarta Expression Language (EL)** | Eclipse EL | Eclipse Foundation |
| **Jakarta RESTful Web Services (JAX-RS)** | RESTEasy / Jersey / CXF | JBoss / Eclipse / Apache |
| **Jakarta XML Web Services (JAX-WS)** | Metro / CXF | Eclipse / Apache |
| **Jakarta JSON Processing (JSON-P)** | Eclipse JSON-P | Eclipse Foundation |
| **Jakarta JSON Binding (JSON-B)** | Eclipse Yasson | Eclipse Foundation |
| **Jakarta Persistence (JPA)** | Hibernate / EclipseLink | Red Hat / Eclipse |
| **Jakarta Data** | Eclipse JNoSQL (early) | Eclipse Foundation |
| **Jakarta Messaging (JMS)** | Apache ActiveMQ / Artemis | Apache / Red Hat |
| **Jakarta Batch** | Eclipse Batch | Eclipse Foundation |
| **Jakarta Mail** | Eclipse Angus | Eclipse Foundation |
| **Jakarta Concurrency** | Eclipse Concurrency | Eclipse Foundation |
| **Jakarta Enterprise Beans (EJB)** | OpenEJB / WildFly EJB | Apache / Red Hat |
| **Jakarta CDI (Contexts and Dependency Injection)** | Weld / OpenWebBeans | Red Hat / Apache |
| **Jakarta Interceptors** | Provided by CDI Implementation | Various |
| **Jakarta Security** | Soteria | Eclipse Foundation |
| **Jakarta Transactions (JTA)** | Narayana / Geronimo | Red Hat / Apache |
| **Jakarta Connectors (JCA)** | IronJacamar | Red Hat |
| **Jakarta Annotations** | Eclipse Annotations | Eclipse Foundation |
| **Jakarta Config** | SmallRye Config | Red Hat |
| **Jakarta MVC** | Ozark | Eclipse Foundation |
| **Jakarta Bean Validation** | Hibernate Validator | Red Hat |

## **Jakarta Faces**

> aka. Java Server Faces.
> 

QA:

- How events are handle?
- How data binding works?
- How partial updates works?
- What is the execution model?
- How `DemuxCompositeELResolver` works?

Phases:

- com.sun.faces.lifecycle.RestoreViewPhase@4793eed2
- com.sun.faces.lifecycle.ApplyRequestValuesPhase@4f2666db
- com.sun.faces.lifecycle.ProcessValidationsPhase@382e51f1
- com.sun.faces.lifecycle.UpdateModelValuesPhase@26a93b9b
- com.sun.faces.lifecycle.InvokeApplicationPhase@7e14a4e2 -> Use dr.gov.esigef.pds.presentacion.nucleo.evento.EventoEjecutadoCambioValor@42185d63
- com.sun.faces.lifecycle.RenderResponsePhase@2f80545

Expression Language (EL):

- …

## References

- https://github.com/weld/core [weld/core]
- https://github.com/csiglab/web-frameworks-labs
- https://en.wikipedia.org/wiki/Jakarta_EE
- https://jakarta.ee/specifications/faces/3.0/jsdoc/jsf.ajax.html
- https://stackoverflow.com/questions/7295096/what-exactly-is-java-ee
- https://jakarta.ee/specifications/