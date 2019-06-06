# cf-tutorial
this is a first tutorial to deploy an app to CF
Use this tutorial to get a sample app up and running on Pivotal Cloud Foundry (PCF). To save time, we will be using Pivotal Web Services, an instance of PCF hosted by Pivotal.
Ensure you have:
	* 
a free Pivotal Web Services account
	* 
familiarity with command line interfaces

Install the CF CLIDownload and install the Cloud Foundry Command Line Interface (cf CLI):

Download for Windows 64 bit
Try the following command to test that the cf CLI works:
cf help
You can use the cf CLI to perform all commands on apps deployed to PCF.

Deploy the Sample AppNow that you have the cf CLI installed and a Pivotal Web Services (PWS) account, you are really close to deploying the sample app.
This sample app is built with Spring Boot to get you up and running as quickly as possible.
Download the app with git:
git clone https://github.com/cloudfoundry-samples/cf-sample-app-spring.git
If you don't have Git installed, you can download a zip file of the app at https://github.com/cloudfoundry-samples/cf-sample-app-spring/archive/master.zip
Navigate to the app directory:
cd cf-sample-app-spring
Sign in to PWS:
cf login -a https://api.run.pivotal.io
Push the app to PWS:
cf push
Open the sample app in your browser.

View the LogsView a snapshot of recent logs:
cf logs cf-demo --recent
Or, stream live logs:
cf logs cf-demo
PCF provides access to an aggregated view of logs related to your application. This includes HTTP access logs, as well as output from app operations such as scaling, restarting, and restaging.
Every log line contains four fields:
	* 
Timestamp
	* 
Log type
	* 
Channel
	* 
Message


Press Control C to stop streaming.

Connect a DatabasePCF enables administrators to provide a variety of services on the platform that can easily be consumed by applications.
List the available ElephantSQL plans:
cf marketplace -s elephantsql
Create a service instance with the free plan:
cf create-service elephantsql turtle cf-demo-db
Bind the newly created service to the app:
cf bind-service cf-demo cf-demo-db
Once a service is bound to an app, environment variables are stored that allow the app to connect to the service after a push, restage, or restart command.
Restage the app:
cf restage cf-demo
Verify the new service is bound to the app:
cf services

Next StepsNice work! You have just deployed and scaled an app with PCF!
Topics to explore:

How PCF Works
https://docs.pivotal.io/pivotalcf/concepts

PCF Documentation
https://docs.pivotal.io/pivotalcf/installing/pcf-docs.html

Installing PCF (IaaS-specific guides for installing PCF)
https://docs.pivotal.io/pivotalcf/installing/

Learn more about the Spring Framework
https://spring.io/guides

Explore and download more Cloud Foundry sample apps
https://github.com/cloudfoundry-samples/

Enroll in Pivotal Cloud Foundry Developer Training
https://pivotal.io/training/courses/pivotal-cloud-foundry-developer-training
