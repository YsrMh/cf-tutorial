# CF-Tutorial
this is a first tutorial to deploy an app to CF
Use this tutorial to get a sample app up and running on Pivotal Cloud Foundry (PCF). To save time, we will be using Pivotal Web Services, an instance of PCF hosted by Pivotal.

Ensure you have:
	
	- a free Pivotal Web Services account: 
	- familiarity with command line interfaces

a free account could be created here : https://try.run.pivotal.io/gettingstarted

## 1. Install the CF CLI

Download and install the Cloud Foundry Command Line Interface (cf CLI):

Download for Windows 64 bit: https://cli.run.pivotal.io/stable?release=windows64&source=github

Try the following command to test that the cf CLI works:

`cf help`

You can use the cf CLI to perform all commands on apps deployed to PCF.

## 2. Deploy the Sample App

Now that you have the cf CLI installed and a Pivotal Web Services (PWS) account, you are really close to deploying the sample app.
This sample app is built with Spring Boot to get you up and running as quickly as possible.
Download the app with `git clone`.

If you don't have Git installed, you can download a zip file of the app available here:

	https://github.com/YsrMh/spring-music
	
Navigate to the app directory:

`cd cf-sample-app-spring` 
 
Sign in to PWS:

`cf login -a https://api.run.pivotal.io`

Push the app to PWS:

`cf push`

Open the sample app in your browser. TIPS: you will find the URL of your app after performing this command: `cf apps`

## 3. View the Logs

View a snapshot of recent logs:

`cf logs cf-demo --recent`

Or, stream live logs:

`cf logs cf-demo`

PCF provides access to an aggregated view of logs related to your application. This includes HTTP access logs, as well as output from app operations such as scaling, restarting, and restaging.

Every log line contains four fields:

	- Timestamp
	- Log type
	- Channel
	- Message


Press Control C to stop streaming.

## 4. Connect a Database

PCF enables administrators to provide a variety of services on the platform that can easily be consumed by applications.

List the available ElephantSQL plans:

`cf marketplace -s elephantsql`

Create a service instance with the free plan:

`cf create-service elephantsql turtle cf-demo-db`

Bind the newly created service to the app:

`cf bind-service cf-demo cf-demo-db`

Once a service is bound to an app, environment variables are stored that allow the app to connect to the service after a `push`, `restage`, or `restart` command.

Restage the app:

`cf restage cf-demo`

Verify the new service is bound to the app:

`cf services`

## 5. Scale the App

Increasing the available disk space or memory can improve overall app performance. Similarly, running additional instances of an app can allow an app to handle increases in user load and concurrent requests. These adjustments are called scaling.
Scaling your app horizontally adds or removes app instances. Adding more instances allows your application to handle increased traffic and demand.

Horizontal scaling increases the number of app instances to handle increased demand.

Increase the number of app instances from one to two:

`cf scale cf-demo -i 2`

Check the status of the app and verify there are two instances running:

`cf app cf-demo`

Scaling your app vertically changes the disk space limit or memory limit for each app instance.

Increase the memory limit for each app instance:

`cf scale cf-demo -m 1G`

Decrease the disk limit for each app instance:

`cf scale cf-demo -k 512M`

## Next Steps

Nice work! You have just deployed and scaled an app with PCF!
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
