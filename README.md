
# Anypoint Template: Salesforce to Netsuite Opportunity Aggregation

+ [License Agreement](#licenseagreement)
+ [Use Case](#usecase)
+ [Considerations](#considerations)
	* [Salesforce Considerations](#salesforceconsiderations)
	* [Netsuite Considerations](#netsuiteconsiderations)
+ [Run it!](#runit)
	* [Running on premise](#runonopremise)
	* [Running on Studio](#runonstudio)
	* [Running on Mule ESB stand alone](#runonmuleesbstandalone)
	* [Running on CloudHub](#runoncloudhub)
	* [Deploying your Anypoint Template on CloudHub](#deployingyouranypointtemplateoncloudhub)
	* [Properties to be configured (With examples)](#propertiestobeconfigured)
+ [API Calls](#apicalls)
+ [Customize It!](#customizeit)
	* [config.xml](#configxml)
	* [businessLogic.xml](#businesslogicxml)
	* [endpoints.xml](#endpointsxml)
	* [errorHandling.xml](#errorhandlingxml)


# License Agreement <a name="licenseagreement"/>
Note that using this template is subject to the conditions of this [License Agreement](AnypointTemplateLicense.pdf).
Please review the terms of the license before downloading and using this template. In short, you are allowed to use the template for free with Mule ESB Enterprise Edition, CloudHub, or as a trial in Anypoint Studio.

# Use Case <a name="usecase"/>
As an administrator I want to aggregate opportunities from Salesforce and NetSuite instances and compare them to see which opportunities can only be found in one of the two and which opportunities are in both instances. 

For practical purposes this Template will generate the result in the format of an e-mail with attached CSV Report.

This Template should serve as a foundation for extracting data from two systems, aggregating data, comparing values of fields for the objects, and generating a report on the differences. 

This implementation retrieves opportunities from both Salesforce and Netsuite instances, compares them (opportunities match if the names are equal), and generates a CSV file which shows opportunities in Salesforce, opportunities in NetSuite, and opportunities present in both systems. The report is then sent to a configured group of e-mail addresses.

# Considerations <a name="considerations"/>

To make this Anypoint Template run, there are certain preconditions that must be considered. All of them deal with the preparations in both systems, that must be made in order for all to run smoothly. **Failling to do so could lead to unexpected behavior of the template.**



## Salesforce Considerations <a name="salesforceconsiderations"/>

There may be a few things that you need to know regarding Salesforce, in order for this template to work.

In order to have this template working as expected, you should be aware of your own Salesforce field configuration.

###FAQ

 - Where can I check that the field configuration for my Salesforce instance is the right one?

    [Salesforce: Checking Field Accessibility for a Particular Field][1]

- Can I modify the Field Access Settings? How?

    [Salesforce: Modifying Field Access Settings][2]


[1]: https://help.salesforce.com/HTViewHelpDoc?id=checking_field_accessibility_for_a_particular_field.htm&language=en_US
[2]: https://help.salesforce.com/HTViewHelpDoc?id=modifying_field_access_settings.htm&language=en_US

### As source of data

If the user configured in the template for the source system does not have at least *read only* permissions for the fields that are fetched, then a *InvalidFieldFault* API fault will show up.

```
java.lang.RuntimeException: [InvalidFieldFault [ApiQueryFault [ApiFault  exceptionCode='INVALID_FIELD'
exceptionMessage='
Account.Phone, Account.Rating, Account.RecordTypeId, Account.ShippingCity
^
ERROR at Row:1:Column:486
No such column 'RecordTypeId' on entity 'Account'. If you are attempting to use a custom field, be sure to append the '__c' after the custom field name. Please reference your WSDL or the describe call for the appropriate names.'
]
row='1'
column='486'
]
]
```






## Netsuite Considerations <a name="netsuiteconsiderations"/>


### As destination of data

There are no particular considerations for this Anypoint Template regarding Netsuite as data destination.



# Run it! <a name="runit"/>
Simple steps to get Salesforce to Netsuite Opportunity Aggregation running.


## Running on premise <a name="runonopremise"/>
In this section we detail the way you should run your Anypoint Template on your computer.


### Where to Download Mule Studio and Mule ESB
First thing to know if you are a newcomer to Mule is where to get the tools.

+ You can download Mule Studio from this [Location](http://www.mulesoft.com/platform/mule-studio)
+ You can download Mule ESB from this [Location](http://www.mulesoft.com/platform/soa/mule-esb-open-source-esb)


### Importing an Anypoint Template into Studio
Mule Studio offers several ways to import a project into the workspace, for instance: 

+ Anypoint Studio generated Deployable Archive (.zip)
+ Anypoint Studio Project from External Location
+ Maven-based Mule Project from pom.xml
+ Mule ESB Configuration XML from External Location

You can find a detailed description on how to do so in this [Documentation Page](http://www.mulesoft.org/documentation/display/current/Importing+and+Exporting+in+Studio).


### Running on Studio <a name="runonstudio"/>
Once you have imported you Anypoint Template into Anypoint Studio you need to follow these steps to run it:

+ Locate the properties file `mule.dev.properties`, in src/main/resources
+ Complete all the properties required as per the examples in the section [Properties to be configured](#propertiestobeconfigured)
+ Once that is done, right click on you Anypoint Template project folder 
+ Hover you mouse over `"Run as"`
+ Click on  `"Mule Application"`


### Running on Mule ESB stand alone <a name="runonmuleesbstandalone"/>
Complete all properties in one of the property files, for example in [mule.prod.properties] (../master/src/main/resources/mule.prod.properties) and run your app with the corresponding environment variable to use it. To follow the example, this will be `mule.env=prod`. 
After this, to trigger the use case you just need to hit the local HTTP endpoint with the port you configured in your file. If this is, for instance, `9090` then you should hit: `http://localhost:9090/generatereport` and this will create a CSV report and send it to the configured e-mail addresses.

## Running on CloudHub <a name="runoncloudhub"/>
While [creating your application on CloudHub](http://www.mulesoft.org/documentation/display/current/Hello+World+on+CloudHub) (Or you can do it later as a next step), you need to go to Deployment > Advanced to set all environment variables detailed in **Properties to be configured** as well as the **mule.env**.
Once your app is all set up and started, supposing you choose as domain name `sfdc2nets-opportunity-aggregation` to trigger the use case, you just need to hit `http://sfdc2nets-opportunity-aggregation.cloudhub.io/generatereport` and report will be sent to the e-mails configured.

### Deploying your Anypoint Template on CloudHub <a name="deployingyouranypointtemplateoncloudhub"/>
Mule Studio provides you with really easy way to deploy your Template directly to CloudHub, for the specific steps to do so please check this [link](http://www.mulesoft.org/documentation/display/current/Deploying+Mule+Applications#DeployingMuleApplications-DeploytoCloudHub)


## Properties to be configured (With examples) <a name="propertiestobeconfigured"/>
In order to use this Mule Anypoint Template you need to configure properties (Credentials, configurations, etc.) either in properties file or in CloudHub as Environment Variables. Detail list with examples:
### Application configuration
+ http.port `9090` 

#### SalesForce Connector configuration

+ sfdc.username `bob.dylan@example.com`
+ sfdc.password `DylanPassword123`
+ sfdc.securityToken `avsfwCUl7apQs56Xq2AKi3X`
+ sfdc.url `https://login.salesforce.com/services/Soap/u/32.0`

#### NetSuite Connector configuration

+ nets.email `email@example.com`
+ nets.password `netsuite_password`
+ nets.account `YHCtmLGOdrjkKvBruTKaiLan`
+ nets.roleId `1`
+ nets.applicationId `77EBCBD6-AF9F-11E5-BF7F-FEFF819CDC9F`

#### SMTP Services configuration

+ smtp.host `smtp.gmail.com`
+ smtp.port `587`
+ smtp.user `exampleuser@gmail.com`
+ smtp.password `ExamplePassword456`

#### Mail details

+ mail.from `exampleuser@gmail.com`
+ mail.to `woody.guthrie@gmail.com`
+ mail.subject `Opportunities Report`
+ mail.body `Please find attached your Opportunities Report`
+ attachment.name `opportunities_report`

# API Calls <a name="apicalls"/>
Salesforce imposes limits on the number of API Calls that can be made. However, we make API call to Salesforce only once during aggregation.


# Customize It!<a name="customizeit"/>
This brief guide intends to give a high level idea of how this Anypoint Template is built and how you can change it according to your needs.
As mule applications are based on XML files, this page will be organized by describing all the XML that conform the Anypoint Template.
Of course more files will be found such as Test Classes and [Mule Application Files](http://www.mulesoft.org/documentation/display/current/Application+Format), but to keep it simple we will focus on the XMLs.

Here is a list of the main XML files you'll find in this application:

* [config.xml](#configxml)
* [endpoints.xml](#endpointsxml)
* [businessLogic.xml](#businesslogicxml)
* [errorHandling.xml](#errorhandlingxml)


## config.xml<a name="configxml"/>
Configuration for Connectors and [Properties Place Holders](http://www.mulesoft.org/documentation/display/current/Configuring+Properties) are set in this file. **Even you can change the configuration here, all parameters that can be modified here are in properties file, and this is the recommended place to do it so.** Of course if you want to do core changes to the logic you will probably need to modify this file.

In the visual editor they can be found on the *Global Element* tab.


## businessLogic.xml<a name="businesslogicxml"/>
Functional aspect of the template is implemented in this XML file, directed by one flow responsible of conducting the aggregation of data, comparing records and finally formating the output, in this case a CSV report.
The *mainFlow* organises the job in three different steps and finally invokes the *outboundFlow* which will deliver the report to the corresponding outbound endpoint.
This flow has Exception Strategy which basically consists on invoking the *defaultChoiseExceptionStrategy* defined in *errorHandling.xml* file.

### Gather Data Flow
Mainly consisting of two calls (Queries), one to SalesForce, the other one to NetSuite, and storing each response in the Invocation Variable named *opportunitiesFromSFDC* or *opportunitiesFromNetsuite* accordingly.

### Aggregation Flow
[Java Transformer](http://www.mulesoft.org/documentation/display/current/Java+Transformer+Reference) is responsible for aggregating the results from the SalesForce and NetSuite instances.
Criteria and format applied:

+ Transformer receives a Mule Message with the two Invocation variables *opportunitiesFromSFDC* and *opportunitiesFromNetsuite* to result in List of Maps with keys: **Name**, **IDInSFDC**, **AmountInSFDC**, **IDInNetsuite**, **AmountInNetsuite**.
+ Opportunities will be matched by names. A record in Netsuite matches SFDC record if the names are equal.

### Format Output Flow

+ [Java Transformer](http://www.mulesoft.org/documentation/display/current/Java+Transformer+Reference) responsible for sorting the list of users in the following order:

	1. Opportunities only in SalesForce
	2. Opportunities only in NetSuite
	3. Opportunities in both SalesForce and NetSuite

All records ordered alphabetically by name within each category.
If you want to change this order then the *compare* method should be modified.

+ CSV Report [DataMapper](http://www.mulesoft.org/documentation/display/current/Datamapper+User+Guide+and+Reference) transforming the List of Maps in CSV with headers **Name**, **IDInSFDC**, **AmountInSFDC**, **IDInNetsuite**, **AmountInNetsuite**.
+ An [Object to string transformer](http://www.mulesoft.org/documentation/display/current/Transformers) is used to set the payload as String.



## endpoints.xml<a name="endpointsxml"/>
This is the file where you will find the inbound and outbound sides of your integration app. This Template has an HTTP Connector as the way to trigger the use case and an SMTP Transport as the outbound way to send the report.

### Trigger Flow
**HTTP Connector** - Start Report Generation

+ `${http.port}` is set as a property to be defined either on a property file or in CloudHub environment variables.
+ The path configured by default is `generatereport` and you are free to change for the one you prefer.
+ The host name for all endpoints in your CloudHub configuration should be defined as `localhost`. CloudHub will then route requests from your application domain URL to the endpoint.

### Outbound Flow
**SMTP Outbound Endpoint** - Send Mail

+ Both SMTP configuration and the actual mail to be sent are defined in this endpoint.
+ This flow is going to be invoked from the flow that does all the functional work: *mainFlow*, the same that is invoked from the Inbound Flow upon triggering of the HTTP Endpoint.



## errorHandling.xml<a name="errorhandlingxml"/>
This is the right place to handle how your integration will react depending on the different exceptions. 
This file holds a [Choice Exception Strategy](http://www.mulesoft.org/documentation/display/current/Choice+Exception+Strategy) that is referenced by the main flow in the business logic.



