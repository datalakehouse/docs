Set index retention patterns
============================

This article describes how to configure the maximum number of indices to keep in your DLH for OpenSearch instance. For more information on OpenSearch indices and shards, see :doc:`this article <../concepts/indices>`.

To create cleanup patterns for OpenSearch indices:

#. Log in to the `DLH web console <https://console.DLH.io>`_ and select your service.

#. Click the **Indexes** tab.

   The top of this view lists the patterns that are currently in use.

#. Click **Add New Pattern**.

#. Enter the pattern that you want to use and the maximum index count for the pattern, then click **Create**.


Alternatively, you can use our `API <https://api.DLH.io/doc/>`_ with a request similar to the following::

  curl -X PUT --data '{"user_config":{"index_patterns": [{"pattern": "logs*", "max_index_count": 2},{"pattern":"test.?", "max_index_count": 3}]}' header "content-type: application-json" --header "authorization: DLHv1 <YOUR TOKEN HERE>" https://api.DLH.io/v1beta/project/<project>/service/<service_name>


