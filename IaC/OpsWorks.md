# OpsWorks

Is a configuration management service that helps you build and operate highly dynamic applications and propagate changes instantly.

Is based on Chef recipes and cookbooks.

A stack is a set of layers, instances and related resources whose configuration you want to manage together.

You can import chef cookbooks in an OpsWorks stack using Git, S3 or HTTP.

Instances are managed by OpsWorks. You can create a 24/7 instance, a time based instance or Load Based instances. When a metric exceeds up a threshold, Opsworks starts more instances, like an autoscaling group.

Deployments need to be created manually to execute recipes, update cookbooks, etc

## Lifecycle events

Each layer has a set of fice lifecycle events, each of which has an associated set of recipes that are specific to the layer. When an event occurs on layer's instance, AWS OpsWorks automatically run the appropiate set of recipes. 

You can also manually configure this events to run as manual commands.

Setup:
This event occurs after a started instance has finished booting.

A setup event takes an instance out of service. Instances on which you run setup events are removed from a load balancer.

Configure:
This events occurs on all instances that:
- Enters or leaves the online state
- Associate an EIP or dissasociate
- Attach or detach a Load Balancer to the layer

Deploy:
This events occurs when you run a Deploy command. Setup includes Deploy.


Undeploy:
This event occurs when you delete an app or run an Undeploy command.


Shutdown:
This event occurs after indicates to OpsWorks Stacks to shut an instance down but before the associate EC2 instance is terminated.

NOTE: Configure is the only event that occurs in all instances. The others are instance individually. Is useful to use to know the instance neighbours.