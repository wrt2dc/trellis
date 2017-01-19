# Trellis

Repository software that implements the [Fedora API](http://fedora.info/spec/).

## Goals

  * Horizontally scalable
  * Fast
  * Modular
  * Light-weight

## Implementation status

The code currently consists of the following elements:

### Core abstractions

  * [trellis-api](https://github.com/acoburn/trellis-api): The core API abstractions
  * [trellis-spi](https://github.com/acoburn/trellis-spi): The service abstractions
  * [trellis-vocabulary](https://github.com/acoburn/trellis-vocabulary): The core RDF vocabularies in use

### Service implementations

  * [trellis-agent](https://github.com/acoburn/trellis-agent): A service for managing user roles
  * [trellis-datastream](https://github.com/acoburn/trellis-datastream): A datastream storage and retrieval service
  * [trellis-id](https://github.com/acoburn/trellis-id): An ID generation service
  * [trellis-io-jena](https://github.com/acoburn/trellis-io-jena): A Jena-based I/O service
  * [trellis-namespaces](https://github.com/acoburn/trellis-namespaces): A namespace service using JSON files for persistence
  * [trellis-webac](https://github.com/acoburn/trellis-webac): An authorization layer

### In progress

 * Event Service -- for serializing repository events to message broker technology, such as [Kafka](http://kafka.apache.org) or AMQP
 * Core (distributed) implementation -- for creating, deleting, updating and fetching resources, based on [RDF-Patch](https://afs.github.io/rdf-patch/) and an asynchronous Kafka event bus
 * LDP Paging support
 * HTTP layer -- this is slated to be implemented with [dropwizard.io](http://dropwizard.io)
 * Cloud-based datastream resolver based on [jclouds](https://jclouds.apache.org/)
 * HTML UI based on [LDPath Templates](http://marmotta.apache.org/ldpath/template.html)

## Main dependencies

  * [Commons-RDF](https://commons.apache.org/proper/commons-rdf/) -- for RDF abstractions
  * [Jena](https://jena.apache.org/) -- for RDF I/O processing
  * [Jackson](https://github.com/FasterXML/jackson) -- for JSON parsing
  * [Jersey](https://jersey.java.net/) -- for HTTP handling
  * [Zookeeper](https://zookeeper.apache.org/) -- for distributed coordination
  * [Kafka](https://kafka.apache.org/) -- for event handling and stream processing

## Deployment

 * The plan is to support container-less (e.g. Docker) and OSGi (e.g. Karaf) deployment options.

## Building

 * All projects are written in Java and/or Clojure and require at least Java 8. All projects can be built with Gradle.

