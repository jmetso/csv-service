# csv-service

A very simple Spring Boot application to demonstrate various Openshift functionalities in demos and workshops.

Parses CSV files and returns the content as JSON.

CSV file format:

*id*, *firstname*, *lastname*

1, Janne, Metso

Requires env variable **DATA_FOLDER**. This points the service to a folder that contains the CSV files. 

In order to set up lab environment go to lab and read the readme there. 

New functions provided with OPENSHIFT_ENV_VAR which will give you access to put in text on the index page. 

Use with oc env dc csv-service OPENSHIFT_ENV_VAR=SomeTextHere

Contributer Kim Borup Red Hat. 

