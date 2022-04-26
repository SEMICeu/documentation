# Persistent URIs

Persistent URIs are identifiers in the form of a URI that are maintained for eternity. 
They provide stability throughout space and time for data.

A key aspect is that persistent URIs are also dereferenceable.
Dereferenceable means that content negotation is active for the PURI.
Without it, one can change and adapt the semantics for the identifier at will. 
It is a technical mean to ensure that semantics are stable and not shifting behind the back of users.

Because if one changes the definition of a PURI, then this change must create a reflection if a new PURI must be created or not.
If it does, a new PURI must be created.


## PURIs at SEMIC

A PURI is of the form *http://data.europa.eu/{domain}/{reference}*. 

where 

 - domain: requested and assigned by Publications Office which is the maintainer of data.europa.eu
 - reference: maintained and assigned by editors of the data model


### Supported domains by SEMIC

### System setup by SEMIC

All PURIs maintained by SEMIC should be handled by the server *uri.semic.eu*.
On this server a PURI resolvement service is installed that implements the content negotation.
The source code and deployment instructions are found in the repository uri.semic.eu-proxy.




