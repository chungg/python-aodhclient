The :program:`aodh` shell utility
=========================================

.. program:: aodh
.. highlight:: bash

The :program:`aodh` shell utility interacts with Aodh API
from the command line. It supports the entirety of the Aodh API.

You'll need to provide :program:`aodh` with your OpenStack credentials.
You can do this with the :option:`--os-username`, :option:`--os-password`,
:option:`--os-tenant-id` and :option:`--os-auth-url` options, but it's easier to
just set them as environment variables:

.. envvar:: OS_USERNAME

    Your OpenStack username.

.. envvar:: OS_PASSWORD

    Your password.

.. envvar:: OS_TENANT_NAME

    Project to work on.

.. envvar:: OS_AUTH_URL

    The OpenStack auth server URL (keystone).

For example, in Bash you would use::

    export OS_USERNAME=user
    export OS_PASSWORD=pass
    export OS_TENANT_NAME=myproject
    export OS_AUTH_URL=http://auth.example.com:5000/v2.0

The command line tool will attempt to reauthenticate using your provided credentials
for every request. You can override this behavior by manually supplying an auth
token using :option:`--aodh-endpoint` and :option:`--os-auth-token`. You can alternatively
set these environment variables::

    export AODH_ENDPOINT=http://aodh.example.org:8041
    export OS_AUTH_PLUGIN=token
    export OS_AUTH_TOKEN=3bcc3d3a03f44e3d8377f9247b0ad155

Also, if the server doesn't support authentication, you can provide
:option:`--os-auth-plugon` aodh-noauth, :option:`--aodh-endpoint`, :option:`--user-id` 
and :option:`--project-id`. You can alternatively set these environment variables::

    export OS_AUTH_PLUGIN=aodh-noauth
    export AODH_ENDPOINT=http://aodh.example.org:8041
    export AODH_USER_ID=99aae-4dc2-4fbc-b5b8-9688c470d9cc
    export AODH_PROJECT_ID=c8d27445-48af-457c-8e0d-1de7103eae1f

From there, all shell commands take the form::

    aodh <command> [arguments...]

Run :program:`aodh help` to get a full list of all possible commands,
and run :program:`aodh help <command>` to get detailed help for that
command.

Examples
--------

Create a resource::

    gnocchi resource create --attribute id:5a301761-f78b-46e2-8900-8b4f6fe6675a --attribute project_id:eba5c38f-c3dd-4d9c-9235-32d430471f94 -n temperature:high instance

List resources::

    gnocchi resource list --type instance

Search of resources::

    gnocchi resource search --query "project_id=5a301761-f78b-46e2-8900-8b4f6fe6675a and type=instance"
