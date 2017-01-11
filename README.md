# Trellis

A repository that implements the Fedora API.

This currently consists of the following elements:

  * [trellis-api](https://github.com/acoburn/trellis-api): The core API abstractions
  * [trellis-spi](https://github.com/acoburn/trellis-spi): The service abstractions
  * [trellis-service-datastream](https://github.com/acoburn/trellis-service-datastream): A datastream storage and retrieval service
  * [trellis-service-id](https://github.com/acoburn/trellis-service-id): An ID generation service
  * [trellis-service-io-jena](https://github.com/acoburn/trellis-service-io-jena): A Jena-based I/O service
  * [trellis-service-namespaces-json](https://github.com/acoburn/trellis-service-namespaces-json): A namespace service using JSON files for persistence
  * [trellis-service-webac](https://github.com/acoburn/trellis-service-webac): An authorization layer
  * [trellis-vocabulary](https://github.com/acoburn/trellis-vocabulary): The core RDF vocabularies in use

In progress:

 * Event Service -- for serializing Fedora Events to a broker technology, such as [Kafka](http://kafka.apache.org) or AMQP
 * Core (distributed) implementation -- for creating, deleting, updating and fetching resources, based on [RDF-Patch](https://afs.github.io/rdf-patch/) and an asynchronous Kafka event bus
 * HTTP layer -- this will use [dropwizard.io](http://dropwizard.io)
 * Cloud-based datastream resolver based on [jclouds](https://jclouds.apache.org/)

Deployment:

 * Container-less deployment and OSGi options will be available.

Building:

 * All projects can be built with Java 8 and gradle.
