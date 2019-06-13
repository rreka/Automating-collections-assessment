# Automating collections assessment

This repository contains programs designed to automate the work of evaluating library electronic journal collections. The programs use the Scopus API to retreive citation data and query a library's link resolver systems using the OpenURL protocol.

This project is in development, but will contain three programs that:
* identify which journals researchers publish in, and if the library collects them
* identify which journals researchers reference in their publications, and if the library collects them
* idenify which journals in a journal ranking list the library collects

## Installation
### Requirements
To use these programs you must have access to Elsevier's Scopus citation database and be running it from an IP address that is affiliated with an institution subscribing to Scopus. You must also have an [API key from Elsevier](https://dev.elsevier.com/).

This program is designed to query library link resolvers that follow the [OpenURL protocol](https://en.wikipedia.org/wiki/OpenURL).

### Technical requirements
This program is written in Python using Jupyter, and is dependent on the following modules that don't come pre-installed with Python:
* [scopus](https://github.com/scopus-api/scopus) (a community-based Python wrapper for the Scopus API)
* pandas

### Configuring the programs to get started
#### Scopus API
When you first use the scopus module, you will need to [configure it](https://scopus.readthedocs.io/en/latest/configuration.html) by entering the API key provided to you by Elsevier.
#### Link resolver
The link resolver querying functionality is provided by the `searchOpenURL` function, and has been written to parse out XML statements that follow the OpenURL protocol, and more specifically, the Alma link resolver.

* Add your link resolver's base URL in `r = requests.get` by replacing  `http://na01.alma.exlibrisgroup.com/view/uresolver/01UTON_UW/openurl?svc_dat=CTO&issn={}` with your base URL. The `?svc_dat=CTO&issn={}` parameters must remain
* Review the XML output from your link resolver and check to see if there are [namespace values](https://www.w3schools.com/xml/xml_namespaces.asp). If so, edit the `ns` dictionary and replace the current values with the namespace values in the XML output from your link resolver. Currently, these values are for the Alma Link Resolver.
* This function parses out the XML data based on the element names. Much of this is uniform with the OpenURL protocol, but please double check the `findall` statements and ensure that the element names reflect the names in your link resolver's XML output.

## Usage
Once configured, use these programs by providing properly-structued data in the Data folder. Run the programs with Jupyter.

`scopusGetPapersByAuthors`
* To use this function, place a CSV file with two columns in the Data folder. The two columns are the researcher's name and their Scopus ID.

## Credits
These programs have been developed by Roger Reka.

## License
GNU GPLv3; see LICENSE.

