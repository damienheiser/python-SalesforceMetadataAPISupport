# python-SalesforceMetadataAPISupport
Support for the Salesforce Metadata API calls.

Using the Metadata API module:

Using the module to login to your salesforce account:

## Changelog
createMetadata() and updateMetadata() are available.  Encapsulate a properly formed metadata xml to manipulate.

Sandbox functionality was added.  By default this class will connect to a sandbox if the sandbox variable is not passed.

Updated to API Version 45 (Spring '19)

## Sample code:
### Connect To Sandbox
```python
import SalesforceMetadataModule as smm
sandbox = True
sfdc = smm.SalesforceMetadataModule(
    yourSalesforceUserName, yourSalesforcePassword, yourSalesforceSecurityToken, sandbox)
print sfdc.getSessionId()
```

### Connect To Production
```python
import SalesforceMetadataModule as smm
sandbox = False
sfdc = smm.SalesforceMetadataModule(
    yourSalesforceUserName, yourSalesforcePassword, yourSalesforceSecurityToken, sandbox)
print sfdc.getSessionId()
```
output: You should be able to see a session id generated

## Calling the metadata api methods using the object (sfdc) created above:

using the 'sfdc' object you can call methods like:

```python
sfdc.listMetadata(SalesforceObject, soap_api_version) # this will return a list of dictionaries
```
### Example:
```python
listContent = sfdc.listMetadata('CustomField', '34.0')
```

```python
for each in listContent:
    for k, v in each.iteritems():
        print k, "=>", v
```        
sample output will look like this:
```createdById => 00528000000OjSzAAK

createdByName => Sunil Singh

createdDate => 2015-06-23T08:41:46.000Z

fileName => objects/Account.object

fullName => Account.UpsellOpportunity__c

id => 00N28000003Z7lOEAS

lastModifiedById => 00528000000OjSzAAK

lastModifiedByName => Sunil Singh

lastModifiedDate => 2015-06-23T08:41:46.000Z

manageableState => unmanaged

type => CustomField
```

## To retrieve any package from the salesforce account use the below method:

sfdc.retrievePackage(members, name, api version, output zip file name)
```python
sfdc.retrievePackage("AllReports/CustomReportTypeJoin",
                     "Report", "34.0", "reportzip.zip")
```
                     
A zipped file will be saved in your working directory.

## To create metadata into salesforce account use the below method:
sfdc.createMetadata (metadataXML)

## To update metadata into salesforce account use the below method:
sfdc.updateMetadata (metadataXML)
