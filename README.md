# Trellis

Repository software that implements the [Fedora API](http://fedora.info/spec/).

Goals:

  * Really, really scalable
  * Really, really fast
  * Modular
  * Light-weight

The code currently consists of the following elements:

  * [trellis-api](https://github.com/acoburn/trellis-api): The core API abstractions
  * [trellis-spi](https://github.com/acoburn/trellis-spi): The service abstractions
  * [trellis-service-datastream](https://github.com/acoburn/trellis-service-datastream): A datastream storage and retrieval service
  * [trellis-service-id](https://github.com/acoburn/trellis-service-id): An ID generation service
  * [trellis-service-io-jena](https://github.com/acoburn/trellis-service-io-jena): A Jena-based I/O service
  * [trellis-service-namespaces-json](https://github.com/acoburn/trellis-service-namespaces-json): A namespace service using JSON files for persistence
  * [trellis-service-webac](https://github.com/acoburn/trellis-service-webac): An authorization layer
  * [trellis-vocabulary](https://github.com/acoburn/trellis-vocabulary): The core RDF vocabularies in use

In progress:

 * Event Service -- for serializing repository events to message broker technology, such as [Kafka](http://kafka.apache.org) or AMQP
 * Core (distributed) implementation -- for creating, deleting, updating and fetching resources, based on [RDF-Patch](https://afs.github.io/rdf-patch/) and an asynchronous Kafka event bus
 * LDP Paging support
 * HTTP layer -- this is slated to be implemented with [dropwizard.io](http://dropwizard.io)
 * Cloud-based datastream resolver based on [jclouds](https://jclouds.apache.org/)
 * HTML UI based on [LDPath Templates](http://marmotta.apache.org/ldpath/template.html)

Main dependencies:

  * [Commons-RDF](https://commons.apache.org/proper/commons-rdf/) -- for RDF abstractions
  * [Jena](https://jena.apache.org/) -- for RDF I/O processing
  * [Jackson](https://github.com/FasterXML/jackson) -- for JSON parsing
  * [Jersey](https://jersey.java.net/) -- for HTTP handling
  * [Zookeeper](https://zookeeper.apache.org/) -- for distributed coordination
  * [Kafka](https://kafka.apache.org/) -- for event handling and stream processing

Deployment:

 * Container-less deployment and (possibly) also OSGi.

Building:

 * All projects are written in Java or Clojure and require at least Java 8. All projects can be built with Gradle.
