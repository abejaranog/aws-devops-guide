# Cloudformation

Cloudformation is the service that allow us to handle infrastructure as a code. You can create resources and their interconnetion between them.
A CloudFormation template is deployed into the AWS environment as a stack. You can manage stacks through the AWS Management Console, AWS Command Line 
Interface, or AWS CloudFormation APIs. If you need to make changes to the running resources in a stack you update the stack. Before making changes to your resources,  you can generate a change set, which is a summary of your proposed changes. Change sets enable you to see how your changes might impact your running resources, especially for critical resources, before implementing them.

Cloudformation templates using JSON and YAML as code languages.
I recommend to use YAML because is more legible, but's your choice.

**Parameters**

Cloudformation Template allow parameters and this is the way to input data to our Cloudformation template.

Can be referenced using the Fn::Ref (_!Ref ParameterName_) in yaml.

Cloudformation also offers us pseudo parameters predefined by Cloudformation like AccountId, Region, StackId or StackName.

**Mappings**

Mappings are fixed variables in your CF Template.
Are very handy to differentiate between environments, or regions.
Mappings are great when you know in advance all the values that can be deduced from variables.

Example
```
Mappings:
  Mapping01:
    dev:
      Name: "dev-ami-template"
    prod:
      Name: "prod-ami-template"
```

To access a map value we need to use _Fn::FindInMap_ function: 
```
!FindInMap [MapName, TopLevelKey, SecondLevelKey]
```

**Outputs**

Declares optional outputs values that we can import from other stacks.
You can't delete a CF Stack if their outputs are referenced by another stack.

To import a value we need to use _Fn::ImportValue_ function.


**Conditions**

Are used to control the creation of resources or outputs using the Conditions statement.

Conditions can be applied to resources, outputs and previously defined using logic intrinsic functions like And, Equals...

But... what is intrinsic functions?


**Intrinsic Functions**

Functions that can be called in our cloudformation template and used to parse some data.

Must know the following intrinsic functions:

````
Ref  -> Returns the value of the parameter or the physical ID of the resource.
Shortcut in YAML: !Ref ResourceID

Fn::GetAtt -> Returns an attribute from a Resource.
Shortcut in YAML: !GetAtt ResourceId.Propertie

Fn::FindInMap -> Returns a map value. Explained in map section.

Fn::ImportValue -> Return an exported value.
Explained in Outputs section.

Fn::Join -> Join values with a delimiter.
Shortcut in YAML: !Join [ delimiter, [ comma-delimited list of values ] ]

Fn::Sub -> Substitute variables in a string.
Shortcut in YAML: 
!Sub 
  - "MyString-${environment}"
  - { environment: "prod" }

You also can reference directly with Parameters or Pseudo-Variables

Condition Functions (If, Not, Equals...) -> Explained in Conditions section.
````
**SSM Parameters**

When you declare a parameter, you can retrieve data from AWS SSM

Example:
````
Parameters:
  InstanceType:
    Type: 'AWS::SSM::Parameter::Value<String>'
    Default: /EC2/InstanceType ##This is the parameter name
````

AWS also has public parameters like the latest AMI.

**DependsOn**

The depends on clause are used to tell to a resource that should not be created before to another resource have finished.

**Drift Detection**

Detects changes make outside the template in a resource managed by a cloudformation template.

**User Data**

We can also include EC2 user data in cloudformation.

User data log is in */var/log/cloud-init-output.log

The important thing to pass is the entire script throught the function Fn::Base64

Example:
````
In the UserData parameter in an EC2 Cloudformation resource:

UserData:
  Fn::Base64: |
    #!/bin/bash
    yum update -y
````

**cfn-init**

Retrieve metadata from Cloudformation to an EC2 resource through user-data.

Example:
```
Metadata:
  AWS::CloudFormation::Init:
```

cfn-signal is another script to send to Cloudformation the signal that cfn-init is end.

We need to define a WaitCondition to block the template until it receives a signal from cfn-signal.

Example:
````
SampleWaitCondition:
  CreationPolicy:
    ResourceSignal:
      Timeout: PT2M
  Type: AWS::CloudFormation::WaitCondition
````

What if Wait Condition didn't receive the required number of signals from an EC2?

- Ensure AMI has Cloudformation Helper Scripts installed
- Verify that the cfn-init and cfn-signal was successfully on the logs
- Verify that instance has internet connection

In the middle of both scripts, you can launch cfn-hup to listen for changes to the EC2 Instance Metadata.

Also you can use cfn-get-metadata to retrieve metadata from Cloudformation


**Rollbacks**

Default behavior: Rollback on failure.
To troubleshoot is recommended the DO_NOTHING option.

**Nested Stacks**

Are stacks as part of ohter stacks.
They allow to isolate repeated patterns or common components in separate stacks.

**ChangeSets**

When you update a stack you need to know what changes before it happens for greater confidence.

Changesets won't say if the update will be successful.

**Deletion & Termination**

You can put a DeletionPolicy in resources to control what happens when Cloudformation template is deleted.

There are various kind of deletion policy:
- Retain
- Snapshot(Default only on DBCluster resources)
- Delete(Default)

Also you can protect your stacks using termination protection policies.

**Cloudformation Status Codes**

See on [Cloudformation Status Code](https://docs.aws.amazon.com/es_es/AWSCloudFormation/latest/UserGuide/using-cfn-describing-stacks.html)

**Capabilities**

We need to provide our templates the capability to create IAM resources by a checkbox(Web Console) or a flag (CLI)
CAPABILITY_IAM or CAPABILITY_NAMED_IAM for resources with custom names

**Stack Policies**

You can prevent the update of a stack using Stack Policies.
Looks like an IAM Policy and you can put Allow or Deny statements based in actions and resources.