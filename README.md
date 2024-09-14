# Cloud Basic Revision Notes

### Regions and Zones: 
Our application needs to be deployed at all over world to reduce latency and improve availability(what if one data centre goes down). AWS provide many regions(and zones inside regions), where we can deploy our applications.

### Managed Services:
Suppose we want to setup single VM or multiple VMs across different regions and zones(here we need load balancer). We can use AWS EC2,  ASG(Auto scaling group) and ELB(Elastic load Balancer). In this case Cloud provider(in this case AWS) will provide Hardware and all, but we have manage, load balancer, how to auto scale, OS on the VMS, our Apps run time etc.
But in case of Managed Services, AWS will provide all that, we have to just provide our Apps jar, var or build files.

**Managed Services example:**
For Apps: EBS (Elastic bean Stalk)
For Relational DB: RDS (Relational DB Service)
For NoSQL DB: Dynamo DB

Some terminology: 
IaaS: Infrastructure as Service → When not using Managed Service. Cloud provider just provide hardwares.
Paas: Platform as Service → When we use Manages services like EBS. Cloud manage provides both hardware and also OS and Runtime, availability and scaling.

### Docker:
Docker helps in standardising the deployment process. We can create an image and it can run at any Data centre or our local machine as long as Docker run time is present on the machine.
Docker image consist of OS, runtime(node js or Java) and our application code.
Docker images is created and it is then pushed to container registry. One example is Docker hub. From the registry images can be pulled and deployed to different environment like dev, QA, Pre-stage, production.

We can go with EBS, there also we can run our docker images, AWS also provide caas(Container as service) named fargate.

Cloud provider also provide container registry like docker hub. AWS has ECR (Elastic container registry).

### Kubernetes:
It is one of Container orchestration tool. It has cluster, clusters have multiple nodes in each node there can multiple pods. In pods our app instance runs. one cluster can be spanned across different regions also.
We can use different cluster so that we can separate QA env, dev env to production env.

Why we need Such Orchestration tools?
Suppose we have micro services and we different number of instance for each of them based on their loads.

**What we want:**

- Auto Scaling: They should autoscale the instances based on the load.
- Service discovery: Suppose one service wants to make an api call to other service. We cannot hardcode the urls of the other services. Because they are dynamic. 
In this case generally we have Service Registry(SE). When all the micro services would register themselves when they start to be discoverable. When api call need to be made first micro service will ask to SE for the URL of other micro service and then it will make the API call.
- Self healing: When any instance goes down due to some reason, we want another healthy instance to be automatically start.
- Load balancing:
- Release new versions with very less downtime. As an example we want canary release. where we can release new version to few instances and test it then release to all instances.
- Common feature: Authentication, Logging, Security etc

All of the above feature container orchestration tool does.
### Serverless: 
User Just need to worry about code, scalability, availability will be taken care by clouds providers.
Also Pay per use service is provided. Based on the request you have to pay. In AWS This service is provided by AWS Lambda. Apart from code we need a little configuration.
In terms of serverless database, AWS DynamoDB provides data. We need to pay based on storage and also how many time data is retrieved from DB. 
Serverless are also knows as Faas (Functions as a Service)

### Compute:
These are the different compute services provided by Cloud providers.

| Vms or Group of Vms (Iaas) | Paas | Container | Container orchestration
(For microservices) | Faas |
| --- | --- | --- | --- | --- |
| EC2, ASG, ELB | EBS(Bean Stalk) | AWS Fargate | AWS ECS, or AWS EKS  | AWS Lambda |
|  |  |  |  |  |

### Storage
Different types of data we want to store:
- Files: text, audio, video, zip etc⇒ Unstructured data
- data: Tables ⇒ Structured data
Here We will discuss about Unstructured data. Different use cases for storage are as follows:
1. Hard drive connected to a single VM ⇒ Block Storage
2. Hard drive connected to multiple VMs, not direct connection but one storage is shared by many Vms ⇒ File Sharing
3. Storing Archives files cheaply
4. Temprory storaage (Required in case of data migration)
5. Static websites (HTMl, css Js files)
6. Video/Image/Text files storage(upload) and download 

For 3, 4, 5, 6 we use Object storage.
AWS provides EBS (Elastic bock storage for 1), EFS (Elastic File sharing) ans S3 for 3, 4, 5, 6.
