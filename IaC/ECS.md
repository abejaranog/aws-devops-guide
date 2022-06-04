# ECS & ECR

## What is Docker?
[Docker](https://docs.docker.com/) is a software developmen platform to deploy apps based on containers that can be ran on any OS.

Docker images are stored in Docker Repositories public or private.

Public: [Docker Hub](https://hub.docker.com)
Private: Amazon ECR or Google GCR

## ECR

Elastic Container Repository, is used to store private own images of Docker containers.

Access is controlled through IAM and you must to log-in in ECR using AWS CLI before to docker push or pull images.

## ECS

ECS Clusters are logical grouping of EC2 Instances running ECS Agent to allow Docker Containers.

At cluster level you have all the information about EC2 that composes the cluster, the scheduling and the tasks running on this cluster.

### Tasks Definitions

Tasks definitions are metadata in JSON form to tell ECS how to run a Docker Container.

It contains crucial information around:
- Image Name
- Port Binding for container and host
- Memory and CPU required
- Environment Variables
- Networking information

Tasks may have an IAM Role that allows to make API requests to authorized AWS Services.

### Services

ECS Services help define how many tasks should run and how they should be run.
They ensure that the number of tasks desired is running across our fleet of EC2 instances.
They can be linked to an ELB/ALB as needed.

Tasks can be deployed by rolling update or Blue/Green strategy using CodeDeploy.

## Load Balancers

You can use an ALB with dynamic port forwarding, that is able to map the dynamic port assign of the containers.

You need to use tasks definitions with no-mapping ports.

At service level you can add the load balancer with enabling a flag and selecting a Load Balancer previously created with a dummy target group.

## Fargate

Fargate allows to create containers in "Serverless" mode. You don't need to provision EC2 instances.
To scale, just increase the task number. 

You need to create task definitions compatible with Fargate to use them.

In Fargate you need to indicate the Task Size and Task CPU.

## Multi Docker Beanstalk

You can run Elastic Beanstalk in Single & Multi Docker container mode.
This will create for you ECS Cluster, EC2 Instances, Load Balancer, Task definitions and Services.

Requires a config file Dockerrun.aws.json

## Cloudwatch integrations

You can auto-configure Cloudwatch Logs to send logs from ECS containers. Also you can manually configure to send them to Splunk.

Also you can install the cloudwatch agent in EC2 innstances to know the information about the instance running the container.

Activating container insights you can view the metrics of any container isolated. It's good to troubleshoot a single container that presents an anomaly.

If you are using the Fargate launch type for your tasks, this allows you to view the logs from your containers. If you are using the EC2 launch type, this enables you to view different logs from your containers in one convenient location, and it prevents your container logs from taking up disk space on your container instances.

The type of information that is logged by the containers in your task depends mostly on their ENTRYPOINT command. By default, the logs that are captured show the command output that you would normally see in an interactive terminal if you ran the container locally, which are the STDOUT and STDERR I/O streams. The awslogs log driver simply passes these logs from Docker to CloudWatch Logs.

---------------
[Go Home](../README.md)