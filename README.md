# Trellis

A scalable platform for building [linked data](https://www.w3.org/TR/ldp/) applications.

## Mailing list

A [mailing list](https://groups.google.com/forum/#!forum/trellis-ldp) is available to anyone who is interested in using, contributing to or simply learning more about Trellis.

## Features

Trellis has been designed with four primary goals:

  * Scalability
  * Long-term durability of content
  * Modularity
  * Adherence to existing web standards

### Scalability

Trellis has been built on components that already support horizontal scalability: Kafka, Zookeeper and Spark. While it is
possible to run Trellis on a single machine, scaling out across a cluster is well-defined and supported. Trellis is
"eventually consistent", meaning that many operations run asynchronously. While this makes the system very responsive, it
also means that clients cannot expect operations to be atomic. In general, per-resource operations are atomic; operations
that cause other resources to change are handled asynchronously.

### Durability

Data integrity is vitally important for content that is stored for years and decades. Trellis makes it possible to retrieve
the state of any resource at any, arbitrary point in time. This also means that nothing is ever truly deleted (though if you
need to purge a resource from the persistence layer, there is a mechanism for that). For every operation that changes a
resource, there is a full audit log available through standard LDP mechanisms. This audit log lists who made what change and
when that change was made.

### Modularity

The overall code base for Trellis is small, and it is divided up into even smaller modules each of which can be maintained
independently. This simplifies maintenance and it also makes it easy to customize individual components as needed. Trellis
has also been designed to fully support OSGi deployment (scheduled for the 0.2.0 release).

### Flexibility

Because Trellis is built on top of LDP, clients that interact with it tend to use a lot of RDF (e.g. JSON-LD). Trellis
enforces only a very minimal set of restrictions on what RDF is allowable: basically, if LDP prohibits it, Trellis does not
allow it, but otherwise, pretty much anything goes. You can use any RDF vocabulary; you can store binaries of any type. Any
special handling of particular content types needs to be handled in another layer of your software stack.

### Web Standards

There are a lot of standards in existence. Trellis has selected to conform to a collection of well-defined and broadly used
specifications because doing so provides a solid and well-understood foundation for interacting with the software. In a
word, Trellis doesn't make up new interaction models that clients would need to understand. This also makes the Trellis API
stable and consistent.

### External Integrations

Any time a resource is created, modified or deleted, a notification is made available, making it easy to use an integration
framework to connect Trellis to external applications. The notifications provide enough information to make informed routing
decisions without being too heavy.

## Underlying specifications

Trellis is an [HTTP/1.1](https://tools.ietf.org/html/rfc7231) server, which complies with the following specifications:

  * [W3C LDP Server](https://www.w3.org/TR/ldp/)
  * [W3C Activity Streams 2.0](https://www.w3.org/TR/activitystreams-core/)
  * [Solid WebAC](https://github.com/solid/solid-spec#authorization-and-access-control) (Authorization and Access Control)
  * [RFC 7089](https://tools.ietf.org/html/rfc7089) (HTTP Framework for Time-Based Access to Resource States -- Memento)
  * [RFC 3230](https://tools.ietf.org/html/rfc3230) (Instance Digests in HTTP)


## Source Code

All source code is open source and licensed as Apache 2. Contributions are welcome

### Core abstractions

  * [trellis-api](https://github.com/trellis-ldp/trellis-api): The core API abstractions
  * [trellis-http](https://github.com/trellis-ldp/trellis-http): The HTTP abstractions
  * [trellis-vocabulary](https://github.com/trellis-ldp/trellis-vocabulary): The core RDF vocabularies in use
  * [trellis-ontology](https://github.com/trellis-ldp/trellis-ontology): The Trellis ontology definitions

### Deployable applications

 * [Web Application](https://github.com/trellis-ldp/trellis-app): A self-contained application that provides the main HTTP api for Trellis
 * [Asynchronous data processor](https://github.com/trellis-ldp/trellis-rosid-file-streaming): A data processing application that can be deployed in stand-alone mode or in a compute cluster, such as Spark, Flink or Apex.

### Modules

Each of these implements a different service in the `trellis-api` module. These can be swapped out for different implementations as needed. Each module is available on Maven Central.

  * [trellis-agent](https://github.com/trellis-ldp/trellis-agent): A service for managing user roles
  * [trellis-amqp](https://github.com/trellis-ldp/trellis-amqp): An AMQP-based event publisher (e.g. for [RabbitMQ](https://www.rabbitmq.com) or [Qpid](https://qpid.apache.org))
  * [trellis-audit](https://github.com/trellis-ldp/trellis-audit): A service that writes Audit-related data for resource modifications.
  * [trellis-binary](https://github.com/trellis-ldp/trellis-binary): A binary object storage and retrieval service
  * [trellis-constraint-rules](https://github.com/trellis-ldp/trellis-constraint-rules): Rules defining the constraints on the RDF that can be accepted by the server
  * [trellis-event-serialization](https://github.com/trellis-ldp/trellis-event-serialization): A service for serializing modification events into an Activity Stream format
  * [trellis-id](https://github.com/trellis-ldp/trellis-id): An ID generation service
  * [trellis-io-jena](https://github.com/trellis-ldp/trellis-io-jena): A Jena-based I/O service
  * [trellis-jms](https://github.com/trellis-ldp/trellis-jms): A JMS-based event publisher (e.g. for [ActiveMQ](https://activemq.apache.org))
  * [trellis-kafka](https://github.com/trellis-ldp/trellis-kafka): A [Kafka](https://kafka.apache.org)-based event publisher
  * [trellis-namespaces](https://github.com/trellis-ldp/trellis-namespaces): A namespace service using JSON files for persistence
  * [trellis-rosid-file](https://github.com/trellis-ldp/trellis-rosid-file): An implementation that uses a (distributed) filesystem for persisting resources, based on [RDF-Patch](https://afs.github.io/rdf-patch/) and an asynchronous Kafka event bus
  * [trellis-webac](https://github.com/trellis-ldp/trellis-webac): An authorization layer

## Main dependencies

An existing Kafka cluster and Zookeeper ensemble are required to run Trellis.

  * [Commons-RDF](https://commons.apache.org/proper/commons-rdf/) -- for RDF abstractions
  * [Jena](https://jena.apache.org/) -- for RDF I/O processing
  * [Jackson](https://github.com/FasterXML/jackson) -- for JSON processing
  * [Jersey](https://jersey.java.net/) -- for HTTP processing
  * [Curator](https://curator.apache.org/) -- for distributed coordination
  * [Kafka](https://kafka.apache.org/) -- for event handling and stream processing
  * [Beam](https://beam.apache.org/) -- for distributed processing

## Documentation

Javadocs for each project is available at https://trellis-ldp.github.io/trellis/apidocs/

## Related projects

  * [py-ldnlib](https://github.com/trellis-ldp/py-ldnlib) A Python3 library for linked data notifications
  * [static-ldp](https://github.com/trellis-ldp/static-ldp) A PHP application that serves static files as LDP resources

## Building

 * All projects are written in Java and require at least Java 8. All projects can be built with Gradle.

