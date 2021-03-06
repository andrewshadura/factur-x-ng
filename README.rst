Factur-X Python library
=======================

Factur-X is a EU standard for embedding XML representations of invoices
in PDF files. This library provides an interface for reading, editing
and saving the this metadata.

Since there are multiple flavors of the embedded XML data, this library
abstracts them into a Python ``dict``, which can be used to load and
save from/to different flavors.

This project was forked from `Akretion <https://github.com/akretion/factur-x>`_ and continues to be under the same license. We aim to make the library higher-level, make editing fields easier and support more standards and flavors.

Main features:
--------------

-  Edit and save existing XML metadata fields.
-  Create new XML representation from template and embed in PDF.
-  Add existing XML representation to PDF.
-  Validate existing XML representation.

Installation
------------

::
   pip install PyPDF2 lxml pyyaml pycountry
   pip install --index-url https://test.pypi.org/simple/ --upgrade factur-x-ng

::

Usage
-----

Load PDF file without XML and assign some values to common fields.

::

   from facturx import FacturX

   inv = FacturX('some-file.pdf')
   inv['due_date'] = datetime(2018, 10, 10)
   inv['seller.name'] = 'Smith Ltd.'
   inv['buyer.country'] = 'France'

Validate and save PDF including XML representation.

::

   inv.is_valid()
   inv.write_pdf('my-file.pdf')

Load PDF *with* XML embedded. View and update fields via pivot dict.

::

   inv = FacturX('another-file.pdf')
   inv_dict = inv.as_dict()
   inv_dict['currency'] = 'USD'
   inv.update(inv_dict)

Save XML metadata in separate file in different formats.

::

   inv.write_xml('metadata.xml')
   inv.write_json('metadata.json')
   inv.write_yaml('metadata.yml')

To have more examples, look at the source code of the command line tools
located in the *bin* subdirectory.

Command line tools
------------------

Several sub-commands are provided with this lib:

-  Dump embedded metadata:   ``facturx dump file-with-xml.pdf metadata.(xml|json|yml)``
-  Validate existing metadata: ``facturx validate file-with-xml.pdf``
-  Add external metadata file: ``facturx add no-xml.pdf metadata.xml``
-  Extract fields from PDF and embed: ``facturx extract no-xml.pdf``

All these command line tools have a **-h** option that explains how to
use them and shows all the available options.

Licence
-------

This library is published under the BSD licence (same licence as
`PyPDF2 <http://mstamy2.github.io/PyPDF2/>`__ on which this lib
depends).

Contributors
------------

-  Alexis de Lattre alexis.delattre@akretion.com: Initial version, PDF- and XMP processing.
-  Manuel Riel: Python 3 support, support for editing individual fields, separate support for different standards 
