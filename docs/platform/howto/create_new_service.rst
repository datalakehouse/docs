﻿Create a new DLH service
==========================

You can add services for the various DLH products in the DLH web console.

To create a new service:

1. Log in to the `DLH web console <https://console.DLH.io/>`_.

2. On the *Services* page, click **Create a new service**.

   This opens a new page with the available service options.

   .. image:: /images/tools/console/console_create_service.png

3. Select the main properties for your service:

   a. Select the service type.

      If there are several versions available, select the version that you want to use. By default, the latest available version is selected.

   b. Select the cloud provider and region that you want to run your service on.

      .. note:: 
	      The pricing for the same service may vary between different providers and regions. The service summary on the right side of the console shows you the pricing for your selected options.

   c. Select a service plan.

      This defines the number of servers and what kind of memory, CPU, and disk resources are allocated to your service.

   d. Enter a name for your service.

      A random name is provided by default, but you can enter a more recognizable name to distinguish it from other services.


4. Click **Create Service** under the summary on the right side of the console.

   This brings you back to the **Services** view. Your new service is listed with a status indicator to show that it is being created.

5. Click the service name.

   The *Overview* page for the service opens.

   .. image:: /images/tools/console/console_service.png

   This view shows you the connection parameters for your service, its current status, and the configuration options.

   The status is *Rebuilding* while the service is being created for you. Once the service is ready, the status changes to *Running*. While services typically start up in a couple of minutes, the performance varies between cloud providers and regions, and it may take longer in some circumstances.

   
