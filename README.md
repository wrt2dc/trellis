# Trellis

Repository software that implements the [Linked Data Platform](https://www.w3.org/TR/ldp/).

**This is a work in progress**

## Goals

  * Horizontally scalable
  * Fast
  * Modular
  * Light-weight

## Mailing list

An email list is available to anyone who is interested at [https://groups.google.com/forum/#!forum/trellis-ldp](https://groups.google.com/forum/#!forum/trellis-ldp).

## Features

Trellis is an [HTTP/1.1](https://tools.ietf.org/html/rfc7231) server, designed to fully comply with the following specifications:

  * [W3C LDP Server](https://www.w3.org/TR/ldp/)
  * [W3C Activity Streams 2.0](https://www.w3.org/TR/activitystreams-core/)
  * [Solid WebAC](https://github.com/solid/solid-spec#authorization-and-access-control) (Authorization and Access Control)
  * [RFC 7089](https://tools.ietf.org/html/rfc7089) (HTTP Framework for Time-Based Access to Resource States -- Memento)
  * [RFC 3230](https://tools.ietf.org/html/rfc3230) (Instance Digests in HTTP)

## Implementation status

The code is a work-in-progress and currently consists of the following elements:

### Core abstractions

  * [trellis-api](https://github.com/trellis-ldp/trellis-api): The core API abstractions
  * [trellis-spi](https://github.com/trellis-ldp/trellis-spi): The service abstractions
  * [trellis-http](https://github.com/trellis-ldp/trellis-http): The HTTP abstractions
  * [trellis-vocabulary](https://github.com/trellis-ldp/trellis-vocabulary): The core RDF vocabularies in use
  * [trellis-ontology](https://github.com/trellis-ldp/trellis-ontology): The Trellis ontology definitions

### Service implementations

Each of these implements a different service in the `trellis-spi` module. These can be swapped out for different implementations as needed.

  * [trellis-agent](https://github.com/trellis-ldp/trellis-agent): A service for managing user roles
  * [trellis-amqp](https://github.com/trellis-ldp/trellis-amqp): An AMQP-based event publisher (e.g. for [RabbitMQ](https://www.rabbitmq.com) or [Qpid](https://qpid.apache.org))
  * [trellis-constraint-rules](https://github.com/trellis-ldp/trellis-constraint-rules): Rules defining the constraints on the RDF that can be accepted by the server
  * [trellis-binary](https://github.com/trellis-ldp/trellis-binary): A binary object storage and retrieval service
  * [trellis-id](https://github.com/trellis-ldp/trellis-id): An ID generation service
  * [trellis-io-jena](https://github.com/trellis-ldp/trellis-io-jena): A Jena-based I/O service
  * [trellis-jms](https://github.com/trellis-ldp/trellis-jms): A JMS-based event publisher (e.g. for [ActiveMQ](https://activemq.apache.org))
  * [trellis-kafka](https://github.com/trellis-ldp/trellis-kafka): A [Kafka](https://kafka.apache.org)-based event publisher
  * [trellis-namespaces](https://github.com/trellis-ldp/trellis-namespaces): A namespace service using JSON files for persistence
  * [trellis-rosid-file](https://github.com/trellis-ldp/trellis-rosid-file): An implementation that uses a (distributed) filesystem for persisting resources, based on [RDF-Patch](https://afs.github.io/rdf-patch/) and an asynchronous Kafka event bus
  * [trellis-webac](https://github.com/trellis-ldp/trellis-webac): An authorization layer

### In progress

 * Deployable application using [dropwizard.io](http://dropwizard.io)
 * Alternate data storage layers, targeting [HBase](https://hbase.apache.org/) (for high performance, distributed scenarios).
 * Cloud-based datastream resolver based on [jclouds](https://jclouds.apache.org/)

## Main dependencies

An existing Kafka cluster and Zookeeper ensemble are required to run Trellis.

  * [Commons-RDF](https://commons.apache.org/proper/commons-rdf/) -- for RDF abstractions
  * [Jena](https://jena.apache.org/) -- for RDF I/O processing
  * [Jackson](https://github.com/FasterXML/jackson) -- for JSON parsing
  * [Jersey](https://jersey.java.net/) -- for HTTP handling
  * [Curator](https://curator.apache.org/) -- for distributed coordination
  * [Kafka](https://kafka.apache.org/) -- for event handling and stream processing
  * [Beam](https://beam.apache.org/) -- for distributed processing

## Related projects

  * [py-ldnlib](https://github.com/trellis-ldp/py-ldnlib) A Python3 library for linked data notifications
  * [static-ldp](https://github.com/trellis-ldp/static-ldp) A PHP application that serves static files as LDP resources

## Deployment

 * The plan is to support container-less (e.g. Docker) and OSGi (e.g. Karaf) deployment options.

## Building

 * All projects are written in Java and/or Clojure and require at least Java 8. All projects can be built with Gradle.

