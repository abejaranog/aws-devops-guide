# Elastic Beanstalk

With Elastic Beanstalk, you can quickly deploy and manage applications in the AWS Cloud without having to learn about the infrastructure that runs those applications. Elastic Beanstalk reduces management complexity without restricting choice or control. You simply upload your application, and Elastic Beanstalk automatically handles the details of capacity provisioning, load balancing, scaling, and application health monitoring.

Elastic Beanstalk supports applications developed in Go, Java, .NET, Node.js, PHP, Python, and Ruby. When you deploy your application, Elastic Beanstalk builds the selected supported platform version and provisions one or more AWS resources, such as Amazon EC2 instances, to run your application.

Has his own CLI **EBCLI**.
You can deploy, upgrade an environment, launch new app version through this CLI using a *config.yml* file

**Saved Configurations**

Elastic Beanstalk offers us the option of save the configuration to replicate it in another environment.

**ebextensions**

.ebextensions is a folder that contains *.config* files with additional configuration of our Elastic Beanstalk environment.

You can use the [option_settings](https://docs.aws.amazon.com/es_es/elasticbeanstalk/latest/dg/ebextensions-optionsettings.html) statement to add additional configuration to autoscaling, launch configuration, [etc](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/command-options-general.html).

Using Resources statement you can create any Cloudformation resources using the Cloudformation Template Format.

Also you have the commands and container_commands statements to run scripts before and after the application and webserver are set up.

[Commands](https://docs.aws.amazon.com/es_es/elasticbeanstalk/latest/dg/customize-containers-ec2.html#linux-commands) block are executed **before** the app and server are set up.

[Container_commands](https://docs.aws.amazon.com/es_es/elasticbeanstalk/latest/dg/customize-containers-ec2.html#linux-container-commands) are executed **after** app and server are set up.

Also you have another statements to take another actions like create users, groups, files, [etc](https://docs.aws.amazon.com/es_es/elasticbeanstalk/latest/dg/customize-containers-ec2.html)

**Procfile and Buildfile**

Commands in a Buildfile are only run once and must terminate upon completion, whereas commands in a Procfile are expected to run for the life of the application and will be restarted if they terminate. To run the JARs in your application, use a Procfile.

You can build your application's class files and JAR(s) on the EC2 instances in your environment by invoking a build command from a [Buildfile](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/java-se-buildfile.html) file in your source bundle.

If you have more than one JAR file in the root of your application source bundle, you must include a [Procfile](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/java-se-procfile.html) file that tells Elastic Beanstalk which JAR(s) to run. You can also include a Procfile file for a single JAR application to configure the Java virtual machine (JVM) that runs your application.

We recommend that you always provide a Procfile in the source bundle alongside your application. This way you precisely control which processes Elastic Beanstalk runs for your application and which arguments these processes receive.

**Rolling Update Strategy**

- All at once (Not additional cost)
- Rolling (Not additional cost)
- Rolling with additional batches (First add instances before remove olders) (Small additional cost)
- Immutable (Similar to blue/green, but managed by elastic beanstalk and using temporal ASG, changing instances between ASG with zero downtime) (High cost due to double capacity)
- Blue/Green is not an update strategy, but can be done using DNS Swap between 2 environments

See [deployments](../Automation/Deployment.md)

**Worker Environments**

Is an application that performs long-time running workloads on demand or scheduled.

**Multi-Docker integrations**

See on [AWS](https://docs.aws.amazon.com/es_es/elasticbeanstalk/latest/dg/create_deploy_docker_ecs.html)