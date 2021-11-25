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

**User Data**