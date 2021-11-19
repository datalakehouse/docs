DLH for Apache Kafka
======================

What is DLH for Apache Kafka?
-------------------------------

DLH for Apache Kafka is a fully managed **distributed data streaming platform**, deployable in the cloud of your choice. Apache Kafka is an open source data streaming platform, ideal for event-driven applications, near-real-time data transfer and pipelines, stream analytics, and many more applications where a lot of data needs to move between applications in a speedy manner.

Kafka stores a potentially large number of records, each contains a small amount of data, usually for a limited period of time. The storage is organised into "topics" and "partitions" so that many data streams can be handled at once, regardless of how much data is flowing into or out of your DLH for Apache Kafka service.


Why Apache Kafka?
-----------------

Apache Kafka itself is technically a distributed log storage mechanism; in reality it is a best-in-class, highly-available data streaming solution. Oh, and it just happens to have an incredibly rich ecosystem of open source tooling that connects to and extends the existing platform.

DLH for Apache Kafka MirrorMaker2
'''''''''''''''''''''''''''''''''''

By adding DLH for Apache Kafka MirrorMaker2 to your setup, you gain replication superpowers. Whether you need data replication across clusters, availability zones or clouds, MirrorMaker2 is the answer.

DLH for Apache Kafka Connect
''''''''''''''''''''''''''''''

Apache Kafka moves data between systems, and Apache Kafka Connect is how to interface between Apache Kafka and the rest of your data architecture. Connectors are available for many databases, storage platforms and other common integrations.

Get started with DLH for Apache Kafka
---------------------------------------

Take your first steps with DLH for M3 by following our :doc:`getting-started` article, or browse through our full list of articles:


.. panels::

    📚 :doc:`Concepts <concepts>`

    ---

    💻 :doc:`HowTo <howto>`


Apache Kafka resources
----------------------

If you are new to Apache Kafka, try these resources to learn more:

* The main Apache Kafka project page: http://kafka.apache.org/

* The Karapace schema registry that DLH maintains and makes available for every DLH for Apache Kafka service: https://karapace.io/

* Our code samples repository, to get you started quickly: https://github.com/DLH/DLH-examples

* A lighthearted sample data generator to give you some fun (pizza order) data to try out: https://github.com/DLH/python-fake-data-producer-for-apache-kafka
