Django CSV Import
=================

Ed Crewe - July 2011

Overview
--------

django-csvimport is a generic importer tool to allow the upload of CSV files for
populating data. The egg installs an admin cvsimport model that has a file upload field.
Add a new csvimport and upload a comma separated values file or MS Excel file.

The upload triggers the import mechanism which matches the header line of the files 
field names to the fields in the selected model. Importing any rows that include all required fields.
Optionally required fields can be specified as part of the upload.
By default duplicate value rows are not inserted.

The import can also be run as a custom command, ie manage.py csvimport filename
for possible use via cronjob etc.

The core import code was based on http://djangosnippets.org/snippets/633/ by Jonathan Holst.
It adds character encoding handling, model field and column autodetection, admin interface,
custom command etc.

NB: There is another similar application django-batchimport but it not packaged,
requires Excel files and doesnt provide a custom command for batch usage.

Custom command
--------------

Use manage.py csvimport --mappings='' --model='app_label.model_name' importfile.csv

For mappings enter a list of fields in order only if you dont have a header row 
with matching field names - or you want to override it, eg.

--mappings = 'column1=shared_code,column2=org(Organisation|name)'

where (model|foreign key field) is used to specify relations if again, you want to
override what would be looked up from your models.

Admin interface import
----------------------

Just add a csvimport item, fill in the form and submit. 
Failed import rows are added to the log field.

Acknowledgements
----------------

This egg was created as part of a django dash at the House of Omni, Bristol UK, organised
by Dan Fairs and the local django users group, DBUG. It was a core component for an application
for aid agency supply chain sharing, prompted by Fraser Stephens of the HELIOS foundation
and developed by Ed Crewe and Tom Dunham.

 
