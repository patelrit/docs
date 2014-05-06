============
Introduction
============

Nirmata's mission is to help businesses innovate faster. It does this by enabling businesses to develop 
and operate cloud native code more effeciciently.

Nirmata's cloud based platform that helps enterprise platform teams rapidly deliver cloud based services and applications. It is light-weight, non-intrusive and easy-to-adopt for enterprises that are looking to transform existing applications or interested in building new cloud-native applications. 

At Nirmata, our goal is to eliminate the undifferentiated heavy lifting enterprise software teams have to undertake to adopt cloud-native architectures. We have extracted the core components of traditional PaaS offerings such as application orchestration, governance and key platform services to provide the flexibility, visibility and control that enterprise teams need. By separating the application control plane from the data plane, we reduce the lock-in while simplifying the adoption of our platform.


1.0 Concepts
=============

With Nirmata platform, an application is made up of multiple services. These services are the basic unit of deployment and management. An application can be deployed to multiple environments across one or more cloud providers. A policy defines how applications and services are deployed and how cloud provider resources are consumed.


2.0 Usage
=============

To get started with Nirmata, following is needed:
- AWS account: Nirmata currently works with Amazon Web Services. We support all US regions in AWS.
- Nirmata account: This should be provided by the Nirmata team.
- Nirmata AMI: Nirmata AMI (ami-id) is available in the AWS market place for us-west regions. For other regions let us know. 
You can also use your own linux AMI with Docker running on it. If you do plan to use your own AMI, you will need to install the Nirmata agent on that instance by including an install script while launching the AMI (instructions).

2.1 AWS Setup
---------------
First step is to setup the cloud provider. Nirmata needs to know which cloud resources should be used to deploy applications. For AWS, this can be done by configuring Auto Scaling groups. Detailed information on creating and managing Auto Scaling groups can be found here. While Auto Scaling groups enables dynamic scaling of cloud resources, this capability is not needed to use them with Nirmata. For Nirmata, Auto Scaling group provides a collection of cloud resources that are available to deploy the desired application. Users can setup multiple Auto Scaling groups depending on their application, environment and services.
Prior to creating an Auto Scaling group, a Launch Configuration needs to be created for that Auto Scaling group. In the launch configuration, the following needs to be specified: 
- Nirmata AWS AMI Id: This will ensure that Nirmata AMI is used
- Nirmata agent install script: The install script needs to be specified in user-data so that the agent is installed when an EC2 instance is initialized.

2.2 Nirmata Setup
-------------------

The next step is to set up Nirmata. This involves:

Setup: When a user signs in to Nirmata for the first time, a setup wizard is displayed. This wizard can also be launched later by selecting the Setup Wizard menu. This wizard helps with configuration of the cloud provider and the placement policy.

Cloud Provider: Cloud provider details including the AWS Access Key and Private Key need to be entered. Also the AWS region, where Auto Scaling policies are configured need to be selected. 

Once these details are entered, the Auto Scaling groups can be selected and host groups can be. Host groups can now be used in defining placement rules needed to deploy applications. 

Placement Policy: Now, a placement policy can be created. This policy can be selected for one or more applications. A policy contains multiple rules. Rules can be created in the Setup Wizard by specifying the rule name and selecting the environment type, container type and host group. These rules will be applied to services at deploy time.


2.3 Application Deployment
---------------------------

Once the Setup Wizard is completed, application, services and environments can be created and applications can be deployed to one or more environments.

Application: An application contains multiple services and can be deployed to one or more environments. While creating an application, a cloud policy needs to be created so that services can be deployed according the the rules specified.

Service: A service is the fundamental unit of deployment and management. To create a new service, Add Service wizard can be used. When creating a new service, all the information required to deploy a service needs to be provided. Selecting the Type of services allows the service to be mapped to appropriate placement rules during deployment. Specifying an image is required. This will ensure that the appropriate image is used when the service is deployed. Other settings such as Run Settings and Ports are optional and are not required if these settings are already specified in the image. 

Lastly, any dependencies across services in the same application can be specified. Specifying dependencies allows the services to be deployed in the correct order as well as allows injection of key variables into dependent services.

Environment: Once the application and services are deployed, environments can be created to deploy the application. While creating an environment, an application and the environment type needs to be selected. The services from that application will be deployed to the environment based on the placement rules. 


2.4 Application Management & Operations
-----------------------------------------

Once the services are deployed, their status can be viewed in the environment details view. Runtime instances for each deployed service can be started and stopped. The logs for the deployed service instances can also be viewed. 

The host group details view also provides the infrastructure view of the application. It provides information on which cloud provider resources are being used for your application. 


