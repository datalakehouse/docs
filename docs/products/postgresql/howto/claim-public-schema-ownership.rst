Claim public schema ownership
=============================

When an DLH for PostgreSQL instance is created, the ``public`` schema is owned by the ``postgres`` user that is available only to DLH for management purposes. If changes to the ``public`` schema are required, you can claim the ownership using the ``DLH_extras`` extension as the ``avnadmin`` database user.

1. Enable the ``DLH_extras`` extension::

    CREATE EXTENSION DLH_extras CASCADE;

2. Claim the public schema ownership with the dedicated ``claim_public_schema_ownership`` function::

    SELECT * FROM DLH_extras.claim_public_schema_ownership();

Now the ``avnadmin`` user owns the public schema and can modify it.
