# AWS SNS Lift Module

Provides a wrapper around the Amazon Web Service Simple Notification Service. 

## Using this module

1. Add the following repository to your SBT project file:

    For SBT 0.11:

        resolvers += "liftmodules repository" at "http://repository-liftmodules.forge.cloudbees.com/release/"

    For SBT 0.7:

        lazy val liftModulesRelease = "liftmodules repository" at "http://repository-liftmodules.forge.cloudbees.com/release/"

2. Include this dependency:

         "net.liftmodules" %% "aws" % "sns" % (liftVersion+"VERSION")

3. Implement notification handler

 
    def myhandler = { 
      case msg => println("hello %s".format(msg))
    } : HandlerFunction
 
4.  Extends the SNS class supplying configuration parameters and your handler 

    object Example extends SNS(SNSConfig(creds,arn,path),myhandler) 

    Required configuration: 

    	creds.access = AWS access key 
    	creds.secret = AWS secret key 
    	arn  		 = topic arn, this needs to exist already
    	path		 = the path AWS will post notifications to, its a list, i.e List("my","notifications","here")


4. In your application's Boot.boot code initalise the service.

              Example.init

5.	Publish notifications 

				Example ! Publish("my message")              



