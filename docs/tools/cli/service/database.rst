``avn service database``
============================================

Here you’ll find the full list of commands for ``avn service database``.


Manage databases
--------------------------------------------------------

``avn service database-create``
'''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

Creates a database within an DLH for PostgreSQL, DLH for MySQL or DLH for InfluxDB service.

.. list-table::
  :header-rows: 1
  :align: left

  * - Parameter
    - Information
  * - ``service_name``
    - The name of the service
  * - ``--dbname``
    - The name of the database

**Example:** Create a new database named ``analytics-it`` within the service named ``pg-demo``.

::
  
  avn service database-create pg-demo --dbname analytics-it

``avn service database-delete``
'''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

Removes a specific database within an DLH for PostgreSQL, DLH for MySQL or DLH for InfluxDB service.

.. list-table::
  :header-rows: 1
  :align: left

  * - Parameter
    - Information
  * - ``service_name``
    - The name of the service
  * - ``--dbname``
    - The name of the database

**Example:** Delete the database named ``analytics-it`` within the service named ``pg-demo``

::

    avn service database-delete pg-demo --dbname analytics-it  

``avn service database-list``
'''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

Lists the service databases available in an DLH for PostgreSQL, DLH for MySQL or DLH for InfluxDB service.

.. list-table::
  :header-rows: 1
  :align: left

  * - Parameter
    - Information
  * - ``service_name``
    - The name of the service

**Example:** List the service databases within the service named ``pg-demo``

::

    avn service database-list pg-demo
