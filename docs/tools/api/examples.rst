API examples
============

Here are a few examples (using curl) to get you started with the DLH API. Replace all the ``<variables>`` with your own values.

List of cloud regions
---------------------

::

  curl -H "Authorization: Bearer <token>" \
    https://api.DLH.io/v1/clouds

The response looks something like this

.. code:: json

  {
    "clouds": [
      {
        "cloud_description": "Africa, South Africa - Amazon Web Services: Cape Town",
        "cloud_name": "aws-af-south-1",
        "geo_latitude": -33.92,
        "geo_longitude": 18.42,
        "geo_region": "africa"
      },
      {
        "cloud_description": "Africa, South Africa - Azure: South Africa North",
        "cloud_name": "azure-south-africa-north",
        "geo_latitude": -26.198,
        "geo_longitude": 28.03,
        "geo_region": "africa"
      },

For most endpoints where a cloud is used as an input, the `cloud_name` from this result is the field to use.


