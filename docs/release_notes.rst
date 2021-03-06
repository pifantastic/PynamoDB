Release Notes
=============

v1.3.4
------

:date: 2014-10-06

This is a backward compatible, minor bug fix release.

Bugs fixed in this release.

* Fixed bug where attributes could not be used in multiple indexes when creating a table.
* Fixed bug where a depedency on mock was accidentally introduced.

v1.3.3
------

:date: 2014-9-18

This is a backward compatible, minor bug fix release, fixing the following issues

* Fixed bug with Python 2.6 compatibility (#28)
* Fixed bug where update_item was incorrectly checking attributes for null (#34)

Other minor improvements

* New API for backing up and restoring tables
* Better support for custom attributes (https://github.com/jlafon/PynamoDB/commit/0c2ba5894a532ed14b6c14e5059e97dbb653ff12)
* Explicit Travis CI testing of Python 2.6, 2.7, 3.3, 3.4, and PyPy
* Tests added for round tripping unicode values


v1.3.2
------

:date: 2014-7-02

* This is a minor bug fix release, fixing a bug where query filters were incorrectly parsed (#26).

v1.3.1
------

:date: 2014-05-26

* This is a bug fix release, ensuring that KeyCondition and QueryFilter arguments are constructed correctly (#25).
* Added an example URL shortener to the examples.
* Minor documentation fixes.


v1.3.0
------

:date: 2014-05-20

* This is a minor release, with new backward compatible features and bug fixes.
* Fixed bug where NULL and NOT_NULL were not set properly in query and scan operations (#24)
* Support for specifying the index_name as a Index.Meta attribute (#23)
* Support for specifying read and write capacity in Model.Meta (#22)


v1.2.2
------

:date: 2014-05-14

* This is a minor bug fix release, resolving #21 (key_schema ordering for create_table).

v1.2.1
------

:date: 2014-05-07

* This is a minor bug fix release, resolving #20.

v1.2.0
------

:date: 2014-05-06

* Numerous documentation improvements
* Improved support for conditional operations
* Added support for filtering queries on non key attributes (http://aws.amazon.com/blogs/aws/improved-queries-and-updates-for-dynamodb/)
* Fixed issue with JSON loading where escaped characters caused an error (#17)
* Minor bug fixes

v1.1.0
------

:date: 2014-04-14

* PynamoDB now requires botocore version 0.42.0 or greater
* Improved documentation
* Minor bug fixes
* New API endpoint for deleting model tables
* Support for expected value conditions in item delete, update, and save
* Support for limit argument to queries
* Support for aliased attribute names

Example of using aliased attribute names:

.. code-block:: python

    class AliasedModel(Model):
        class Meta:
            table_name = "AliasedModel"
        forum_name = UnicodeAttribute(hash_key=True, attr_name='fn')
        subject = UnicodeAttribute(range_key=True, attr_name='s')

v1.0.0
------

:date: 2014-03-28

* Major update: New syntax for specifying models that is not backward compatible.

.. important::
    The syntax for models has changed!

The old way:

.. code-block:: python

    from pynamodb.models import Model
    from pynamodb.attributes import UnicodeAttribute


    class Thread(Model):
        table_name = 'Thread'
        forum_name = UnicodeAttribute(hash_key=True)

The new way:

.. code-block:: python

    from pynamodb.models import Model
    from pynamodb.attributes import UnicodeAttribute


    class Thread(Model):
        class Meta:
            table_name = 'Thread'
        forum_name = UnicodeAttribute(hash_key=True)

Other, less important changes:

* Added explicit support for specifying the server hostname in models
* Added documentation for using DynamoDB Local and dynalite
* Made examples runnable with DynamoDB Local and dynalite by default
* Added documentation for the use of ``default`` and ``null`` on model attributes
* Improved testing for index queries


v0.1.13
-------

:date: 2014-03-20

* Bug fix release. Proper handling of update_item attributes for atomic item updates, with tests. Fixes #7.

v0.1.12
-------

:date: 2014-03-18

* Added a region attribute to model classes, allowing users to specify the AWS region, per model. Fixes #6.

v0.1.11
-------

:date: 2014-02-26

* New exception behavior: Model.get and Model.refresh will now raise DoesNotExist if the item is not found in the table.
* Correctly deserialize complex key types. Fixes #3
* Correctly construct keys for tables that don't have both a hash key and a range key in batch get operations. Fixes #5
* Better PEP8 Compliance
* More tests
* Removed session and endpoint caching to avoid using stale IAM role credentials
