Claim public schema ownership
=============================

When an datalakehouse for PostgreSQL instance is created, the ``public`` schema is owned by the ``postgres`` user that is available only to datalakehouse for management purposes. If changes to the ``public`` schema are required, you can claim the ownership using the ``datalakehouse_extras`` extension as the ``avnadmin`` database user.

1. Enable the ``datalakehouse_extras`` extension::

    CREATE EXTENSION datalakehouse_extras CASCADE;

2. Claim the public schema ownership with the dedicated ``claim_public_schema_ownership`` function::

    SELECT * FROM datalakehouse_extras.claim_public_schema_ownership();

Now the ``avnadmin`` user owns the public schema and can modify it.
