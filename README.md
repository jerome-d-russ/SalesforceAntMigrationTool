# Salesforce Ant Script Documentation

## Installation

In order to begin using the ANT Migration Tool and the scripts associated with them, we must first install the software!

* Install Java and Ant: https://developer.salesforce.com/docs/atlas.en-us.daas.meta/daas/forcemigrationtool_prereq.htm

* Setup Properties File (detailed below)

* Configure External Tools Configuration in Force.com IDE (or your preferred tool's equivalent)

## Properties File
A file (build.properties) to put default and/or custom entries to prevent ANT's input popups from occurring.   

*Note*: This file needs setup when you first start using ANT.  

Input boxes can be skipped if you specify the value in the build.properties files. For example:  
dc.pwd = password123  
in the build.properties file will skip the question asking for your password (which is good, as the input box is open text).

All of the variables outline below can be overriden in this way (which is how you get CI to work).

#### Global Values

##### Workspace Variables
* *workspace* - The local workspace location; Ex: workspace=c:/devl/ws/teamname/
* *dc.default.user* - The default username you would like to use most often (can be changed on input)  
* *sf.maxPoll* - The max time to wait

##### Proxy Variables - If not using, remove depends='proxy' from targets in build.xml
* *proxy.url* - URL of proxy
* *proxy.port* - Port used by proxy
* *proxy.username* - username to login to proxy
* *proxy.password* - password to login to proxy

## Target: ValidateProjectToOrg
Deploy/Validate a local project to Salesforce
#### Inputs
* *dc.project* - The project you want to validate/deploy (Should match Force.com's Package Explorer)
* *dc.deployment* - The temp folder to use for deployment/validation/retrieve
* *dc.update* - Update to head
* *dc.user* - The username you want to validate/deploy the project with
* *dc.pwd* - The password of the username you want to validate the project with
* *dc.checkOnly* - Check Only? If true, does a validate. If false, deploys.
* *dc.testLevel* - What, if any, tests do you want to run?
* *dc.serverurl* - Interact through test or production?
* *dc.destructiveChanges* - Do you want to deploy Destructive Changes?
* *dc.checkFlows* - Do you want to deploy Process Builder Flows?

## Target: DeployDestructiveChanges
Deploy destructive changes to Salesforce (ignores warnings)
#### Inputs
* *dc.project* - The project you want to validate (Should match Force.com's Package Explorer)
* *dc.deployment* - The temp folder to use for deployment/validation/retrieve
* *dc.update* - Update to head
* *dc.user* - The username you want to validate/deploy the project with
* *dc.pwd* - The password of the username you want to validate the project with
* *dc.checkOnly* - Check Only? If true, does a validate. If false, deploys.
* *dc.testLevel* - What, if any, tests do you want to run?
* *dc.serverurl* - Interact through test or production?
* *dc.destructiveChanges* - Do you want to deploy Destructive Changes?
* *dc.checkFlows* - Do you want to deploy Process Builder Flows?

## Target: PullDownCodeFromSalesforce
Retrieve code from Salesforce and put it in your local project
#### Inputs
* *dc.project* - The project you want to put code in (Should match Force.com's Package Explorer)
* *dc.deployment* - The temp folder to use for deployment/validation/retrieve
* *dc.update* - Update to head
* *dc.user* - The username you want to login with
* *dc.pwd* - The password of the username you want to login with
* *dc.serverurl* - Interact through test or production?

## Target: BuildApexDoc
Build ApexDoc Documentation for the specified project  
#### Inputs
* *dc.project* - The project you want to validate (Should match Force.com's Package Explorer)

## Target: BuildMarkDownFile
Build MarkDown Documentation based on inputs  
#### Inputs
* *dc.buildMd* - The full file path of the md file you want to compile (or relative file path from build.xml)
* *dc.buildHtml* - The full file path of the html file you want to create (or relative file path from build.xml)  

#### Customize
* *dc.md.exe* - The full file path of the exe you want to use to compile  
**Note:** - The program must follow the parameters of "-i 'file/path/inputFile.md' -o 'file/path/outputFile.html'"
* *dc.default.buildMd* - The default input MarkDown file
* *dc.default.buildHtml* - The default output HTML file  

## Target: CleanProjectFolder    
Remove components that are not deployable using Salesforce's ANT Migration Tool  
#### Inputs  
* *dc.project* - The project you want to remove the undeployable components from (Should match Force.com's Package Explorer)  
