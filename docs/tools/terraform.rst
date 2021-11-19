datalakehouse Terraform provider
=========================

    Terraform is an open-source infrastructure as code software tool that provides a consistent CLI workflow to manage hundreds of cloud services. Terraform codifies cloud APIs into declarative configuration files. `Terraform website <https://www.terraform.io/>`_.

With datalakehouse's Terraform Provider you can manage all your services programmatically.

See the `official documentation <https://registry.terraform.io/providers/datalakehouse/datalakehouse/latest/docs>`_ to learn about all the possible services and resources and the `GitHub repository <https://github.com/datalakehouse/terraform-provider-datalakehouse>`_ for reporting issues and contributing.

.. caution::
  Recreating stateful services with Terraform will possibly delete the service and all its data before creating it again. Whenever the Terraform plan indicates that a service will be deleted or replaced, a catastrophic action is possibly about to happen.

  Some properties, like project and the resource name, cannot be changed and it will trigger a resource replacement.

  To avoid any issues, please set the termination_protection property to true on all production services, it will prevent Terraform to remove the service until the flag is set back to false again. While it prevents a service to be deleted, any logical databases, topics or other configurations may be removed even when this section is enabled. Be very careful!

Getting started
---------------
Let's get started by configuring datalakehouse's Terraform provider and deploying a PostgreSQL database.

Requirements 
''''''''''''
- `Download and install Terraform <https://www.terraform.io/downloads.html>`_
- `Sign up <https://console.datalakehouse.io/signup?utm_source=github&utm_medium=organic&utm_campaign=docs&utm_content=repo>`_ for datalakehouse if you haven't already
- `Generate an authentication token <https://help.datalakehouse.io/en/articles/2059201-authentication-tokens>`_ on datalakehouse's console or CLI

Set up the provider
'''''''''''''''''''
To initialise the provider, we will need to configure the Terraform `required_providers` block and add the API authentication token in the `api_token` field.

Create a file named `main.tf` and add the content below:

.. code:: bash

    terraform {
      required_providers {
        datalakehouse = {
          source  = "datalakehouse/datalakehouse"
          version = "2.1.12" # check out the latest version in the github release section
        }
      }
    }

    provider "datalakehouse" {
      api_token = "your-api-token"
    }

Run the command below to initialize Terraform. It will create a directory structure containing Terraform configuration files, install custom providers etc::

  $ terraform init

Deploy a PostgreSQL database
''''''''''''''''''''''''''''
Now let's deploy a fully managed PostgreSQL database on the GCP Frankfurt region. You can also see other services and available regions `on our pricing page <https://datalakehouse.io/pricing>`_.

Add the following block of code to the `main.tf` file:

.. code:: bash

    resource "datalakehouse_pg" "postgresql" {
      project                = "your-project-name"
      service_name           = "postgresql"
      cloud_name             = "google-europe-west3"
      plan                   = "startup-4"
    }
    
    output "postgresql_service_uri" {
      value     = datalakehouse_pg.postgresql.service_uri
      sensitive = true
    }

Plan and apply the Terraform code::

  $ terraform plan
  $ terraform apply

We now have a PostgreSQL service up and running! You can access it with the command below that combines the ``psql`` command with fetching the connection information from Terraform::

  $ psql "$(terraform output -raw postgresql_service_uri)"

Clean up
''''''''
To destroy the created PostgreSQL database, use the following command::

  $ terraform destroy

Learn more
----------
Check out these resources to learn more about Terraform and our Provider:

* `Learn Terraform <https://learn.hashicorp.com/collections/terraform/aws-get-started>`_
* `datalakehouse Terraform Provider documentation <https://registry.terraform.io/providers/datalakehouse/datalakehouse/latest/docs>`_

Get involved
------------
If you have any comments or want to contribute to the tool, please join us on the `GitHub repository <https://github.com/datalakehouse/terraform-provider-datalakehouse>`_.
