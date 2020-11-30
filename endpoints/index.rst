Available API endpoints
=======================

Below are described the API endpoints that Qeios makes available for third parties.

Endpoints are relative to the base URL. The base URL is ``https://www.qeios.com/api``. So, for example, in order to request the endpoint ``/definitions`` you should call the URL ``https://www.qeios.com/api/definitions``.

POST /definitions
-----------------

Create a new Definition draft. In the response you'll get the details of the Publication that you've just created, together with its ``qeios_id``.

Request
^^^^^^^
+-------------------------+--------------------------------------------------------------------------------------------+
| Parameter               | Value                                                                                      |
+=========================+============================================================================================+
| is_echo                 | Boolean. Default: ``false``                                                                |
+-------------------------+--------------------------------------------------------------------------------------------+
| previous_version_qid    | | If you want to create a new version of an existing Definition,                           |
|                         | | this must be the ``qeios_id`` of the current latest version.                             |
+-------------------------+--------------------------------------------------------------------------------------------+

Response
^^^^^^^^
.. code-block:: json

    {
        "data": {
            "publication": {
                "qeios_id": "ABCDEF",
                "title": null,
                ...
            }
        },
        "links": {
            "edit": "https://www.qeios.com/..."
        }
    }

PUT /publications/``qeios_id``
------------------------------

Update a Publication draft's contents. You cannot do this action on a Publication that's already ``published``.

Request
^^^^^^^
+------------+------------------------------------------------------------------------------------------+
| Parameter  | Value                                                                                    |
+============+==========================================================================================+
| title      | Plain text.                                                                              |
+------------+------------------------------------------------------------------------------------------+
| body       | HTML Body.                                                                               |
+------------+------------------------------------------------------------------------------------------+
| abstract   | *(Articles only)* HTML Abstract. Only inline elements are allowed.                       |
+------------+------------------------------------------------------------------------------------------+
| source     | | *(Echo Definitions only)* HTML Source. Only inline elements are allowed.               |
|            | | You probably want to specify a URI or DOI. Anyway, you are free to just use plain text.|
+------------+------------------------------------------------------------------------------------------+

Response
^^^^^^^^
.. code-block:: json

    {
        "data": {
            "publication": {
                "qeios_id": "ABCDEF",
                "title": "Updated title",
                ...
            }
        },
        "links": {
            "edit": "https://www.qeios.com/..."
        }
    }

PUT /publications/``qeios_id``/vacant-authors
---------------------------------------------

Update the Vacant Authors that are associated to an Echo Definition.

Request
^^^^^^^
+-------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Parameter         | Value                                                                                                                                                                                                                                  |
+===================+========================================================================================================================================================================================================================================+
| vacant_authors    | | List of vacant authors (defined as having ``first_name`` and ``last_name``).                                                                                                                                                         |
|                   | | If you want to attribute authorship to an organization you can omit the ``last_name`` and write the organization name as ``first_name``.                                                                                             |
+-------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Example request parameters:

.. code-block:: php

    [
        "vacant_authors" => [
            [
                "first_name" => "Albert",
                "last_name" => "Einstein"
            ],
            [
                "first_name" => "National Cancer Institute (NCI)"
            ]
        ]
    ]

Response
^^^^^^^^
.. code-block:: json

    {
        "data": {
            "presentation_authors": [
                {
                    "first_name": "Albert",
                    "last_name": "Einstein",
                    ...
                },
                {
                    "first_name": "National Cancer Institute (NCI)",
                    ...
                }
            ]
        }
    }

DELETE /publications/``qeios_id``
---------------------------------

Delete a Publication draft and all its related information. You cannot do this action on a Publication that's already ``published``.

Response
^^^^^^^^
HTTP 204

POST /publications/``qeios_id``/publish
---------------------------------------

Publish a Publication, taking it from ``draft`` state to ``published``.
You'll get an error response if the Publication you're trying to publish doesn't have all its essential details filled.

E.g., for an Echo Definition you must have added:

- Title
- Body
- Source
- One or more Vacant Authors

Request
^^^^^^^
+---------------+-------------------------------------------------+
| Parameter     | Value                                           |
+===============+=================================================+
| as_preprint   | *(Articles only)* Boolean. Default: ``false``   |
+---------------+-------------------------------------------------+

Response
^^^^^^^^
.. code-block:: json

    {
        "data": {
            "publication": {
                "qeios_id": "ABCDEF",
                "title": "The title",
                ...
            }
        }
    }

POST /publications/``qeios_id``/attach-tag
------------------------------------------

Attach one or more tags to a Publication.

Request
^^^^^^^
+---------------+------------------------------------------------------------+
| Parameter     | Value                                                      |
+===============+============================================================+
| tag_name      | Name (or array of names) of the tag(s) you want to attach. |
+---------------+------------------------------------------------------------+

Response
^^^^^^^^
HTTP 200

POST /publications/``qeios_id``/detach-tag
------------------------------------------

Detach one or more tags from a Publication.

Request
^^^^^^^
+---------------+------------------------------------------------------------+
| Parameter     | Value                                                      |
+===============+============================================================+
| tag_name      | Name (or array of names) of the tag(s) you want to detach. |
+---------------+------------------------------------------------------------+

Response
^^^^^^^^
HTTP 200