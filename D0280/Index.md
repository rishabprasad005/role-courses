# **Chapter 1:** Describing the Red Hat OpenShift Container Platform

## **1.1.** Red Hat OpenShift Container Platform Features

- After completing this section, you should be able to describe the typical usage of the OpenShift product and its features  
- Introducing OpenShift Container Platform and its Features

## **1.3.** Describing the Architecture of OpenShift

- Introducing the Declarative Architecture of Kubernetes
- Introducing the OpenShift Control Plane
- Describing OpenShift Extensions
- Introducing the OpenShift Default Storage Class

## **1.5.** Describing Cluster Operators

- After completing this section, you should be able to describe what a cluster operator is, how it works, and name the major cluster operators
- Introducing Kubernetes Operators
- Introducing the Operator Framework
  - Operator Software Development Kit (Operator SDK)
  - Operator Life Cycle Manager (OLM)
  - Introducing OperatorHub
- Introducing Red Hat Marketplace
- Introducing OpenShift Cluster Operators

# **Chapter 2:** Verifying the Health of a Cluster

## **2.1.** Describing Installation Methods

- After completing this section, you should be able to describe the OpenShift installation process
- Introducing OpenShift Installation Methods  
  - Full-stack Automation
  - Pre-existing Infrastructure
- Comparing OpenShift Installation Methods
- Describing Installation Process step-by-step
- Customizing an OpenShift Installation

## **2.3.** Troubleshooting OpenShift Clusters and Applications [INCOMPLETE]

- After completing this section, you should be able to
  - Execute commands that assist in troubleshooting common problems.
  - Verify that your OpenShift cluster nodes are healthy.
  - Troubleshoot common issues with OpenShift and Kubernetes styles of deployment.
- Troubleshooting Common Issues with an OpenShift Cluster

## **2.5.** Introducing OpenShift Dynamic Storage **[IMPORTANT]**

- After completing this section, you should be able to
  - identify the components and resources of persistent storage
  - deploy an application that uses a persistent volume claim
- Persistent Storage Overview
- Persistent Volume and Persistent Volume Claim Life Cycle
- Verifying the Dynamic Provisioned Storage 
  - oc get storage command
- Deploying Dynamically Provisioned Storage
  - oc set volumes command
  - create a PersistentVolumeClaim API object
- Deleting Persistent Volume Claims

## **2.6.** Guided Exercise: Introducing OpenShift Dynamic Storage

- In this exercise, you will deploy a PostgreSQL database using a persistent volume claim and identify its dynamically allocated volume.
- You should be able to:-
  - Identify the default storage settings of an OpenShift cluster.
  - Create persistent volume claims.
  - Manage persistent volumes.

# **Chapter 3:** Configuring Authentication and Authorization

## **3.1.** Configuring Identity Providers

- After completing this section, you should be able to configure the HTPasswd identity provider for OpenShift authentication
- Describing OpenShift Users, Groups, Role, Identity and Service Account
- Authenticating API Requests
  - Introducing the Authentication Operator
  - Introducing Identity Providers
- Authenticating as a Cluster Administrator
  - Authenticating Using the X.509 Certificate
  - Authenticating Using the Virtual Use
  - Deleting the Virtual User
- Configuring the HTPasswd Identity Provider
  - Configuring the OAuth Custom Resource
  - Updating the OAuth Custom Resource
- Managing Users with the HTPasswd Identity Provider
  - Creating an HTPasswd File
  - Add or update credentials
  - Delete credentials
  - Creating the HTPasswd Secret
  - Extracting Secret Data
  - Updating the HTPasswd Secret 
- Deleting Users and Identities
- Assigning Administrative Privileges

## **3.2.** Guided Exercise: Configuring Identity Providers

- In this exercise, you will configure the HTPasswd identity provider and create users for cluster administrators
- You should be able to:-
  - Create users and passwords for HTPasswd authentication.
  - Configure the Identity Provider for HTPasswd authentication.
  - update password of exixsting user
  - add new users
  - Assign cluster administration rights to users.

## **3.3.** Defining and Applying Permissions Using RBAC

- After completing this section, you should be able to define role-based access controls and apply permissions to users
- Introducing Role-based Access Control (RBAC)
  - Authorization Process
  - Change a regular user to a cluster administrator
  - Change a cluster administrator to a regular user
  - oc adm policy & oc policy command
- Default Roles in OpenShift 
  - admin
  - basic-user
  - cluster-admin
  - cluster-status
  - edit
  - self-provisioner
  - view
- User Types in OpenShift
  - Regular Users
  - System Users
  - Service Acounts

## **3.4.** Guided Exercise: Defining and Applying Permissions using RBAC **[IMPORTANT]**

- In this exercise, you will define role-based access controls and apply permissions to users
- You should be able to:-
  - Remove project creation privileges from users who are not OpenShift cluster administrators.
  - Create OpenShift groups and add members to these groups.
  - Create a project and assign project administration privileges to the project.
  - As a project administrator, assign read and write privileges to different groups of users

## **3.5.** Lab: Configuring Authentication and Authorization

- In this lab, you will configure the HTPasswd identity provider, create groups, and assign roles to users and groups
- You should be able to:-
  - Create users and passwords for HTPasswd authentication.
  - Configure the Identity Provider for HTPasswd authentication.
  - Assign cluster administration rights to users.
  - Remove the ability to create projects at the cluster level.
  - Create groups and add users to groups.
  - Manage user privileges in projects by granting privileges to groups.


# **Chapter 4:** Configuring Application Security **[IMPORTANT]**

## **4.1.** Managing Sensitive Information with Secrets

- After completing this section, you should be able to:-
  - Create and apply secrets to manage sensitive information.
  - Share secrets between applications
- Features and Use case of secrets
- Creating a Secret (oc create secret):-
  - Create a generic secret containing key-value pairs from literal values typed on the command line
  - Create a generic secret using key names specified on the command line and values from files
  - Create a TLS secret specifying a certificate and the associated key
- Exposing Secrets to Pods
  - Secrets as Pod Environment Variables
  - Secrets as Files in a Pod
- Configuration Map Overview (oc create configmap)
- Updating Existing Secrets and Configuration Maps
  - oc extract
  - oc set data

## **4.2.** Guided Exercise: Managing Sensitive Information With Secrets

- In this exercise, you will manage information using secrets
- You should be able to:-
  - Manage secrets and use them to initialize environment variables in applications.
  - Use secrets for a MySQL database application.
  - Assign secrets to an application that connects to a MySQL database.

## **4.3.** Controlling Application Permissions with Security Context Constraints

- After completing this section, you should be able to:-
  - Create service accounts and apply permissions
  - Manage security context constraints
- Security Context Constraints (SCCs)
  - Available SCCs in OpenShift
  - Change the container to run using a different SCC
- Privileged Containers

## **4.4.** Guided Exercise: Controlling Application Permissions with Security Context Constraints

- In this exercise, you will deploy `gitlab server` that require pods with extended permissions.
- You should be able to:-
  - Create service accounts and assign security context constraints (SCCs) to them.
  - Assign a service account to a deployment configuration.
  - Run applications that need root privileges.

## **4.5.** Lab: Configuring Application Security

- In this lab, you will create a secret to share sensitive configuration information and modify a deployment so that it runs with less restrictive settings.
- You should be able to:-
  - Provide sensitive information to deployments using secrets.
  - Allow applications to run in a less restrictive environment using security context constraints.

# **Chapter 5:** Configuring OpenShift Networking for Applications **[IMPORTANT]**

## **5.1.** Troubleshooting OpenShift Software-defined Networking

- After completing this section, you should be able to troubleshoot OpenShift software-defined networking using the command-line interface
- Introducing OpenShift Software-defined Networking
  - Discussing OpenShift Networking Model
  - Migrating Legacy Applications
- Service Resource
  - How to Create Service Resource
  - Using Services for Accessing Pods
- Discussing the DNS Operator
  - Introducing DNS operator
  - Responsibilities of DNS Operator
  - Managing DNS Records for Services
- Introducing the Cluster Network Operator
- Introducing Multus CNI

## **5.2.** Guided Exercise: Troubleshooting OpenShift Software-defined Networking 

- As an OpenShift developer, you just completed the migration of a To Do Node.js application to OpenShift. The application is comprised of two deployments, one for the database, and one for the front end. It also contains two services for communication between pods. Although the application seems to initialize, you cannot access it via a web browser. In this activity, you will troubleshoot your application and correct the issue. 

- In this exercise, you will diagnose and fix connectivity issues with a Kubernetes-style application deployment.You should be able to:-
  - Deploy the To Do Node.js application.
  - Create a route to expose an application service.
  - Troubleshoot communication between pods in your application using oc debug.
  - Update an OpenShift service.

## **5.3.** Exposing Applications for External Access

- After completing this section, you should be able to allow and protect network connections to applications inside an OpenShift cluster
- Accessing Application from External Networks
- Describing Methods for Managing Ingress Traffic
  - Route
  - Ingress
  - External load balancer
  - Service external IP
  - NodePort
- Route vs Ingress
- Creating Routes
  - via command line (oc expose)
  - via definition file
- Securing Routes
- OpenShift Secure Routes
  - Edge
  - Passthrough
  - Re-encryption
- Securing Applications with Edge Routes
- Securing Applications with Passthrough Routes

## **5.4.** Guided Exercise: Exposing Applications for External Access

- As an application developer, you are ready to deploy your application in OpenShift. In this activity, you will deploy two versions of the application, one that is exposed over unencrypted traffic (HTTP), and one that is exposed over secure traffic.
- In this exercise, you will expose an application secured by TLS certificates. You should be able to:-
  - Deploy an application and create an unencrypted route for it.
  - Create an OpenShift edge route with encryption.
  - Update an OpenShift deployment to support a new version of the application.
  - Create an OpenShift TLS secret and mount it to your application i.e. Passthrough Route
  - Verify that the communication to the application is encrypted.

## **5.5.** Configuring Network Policies

- After completing this section, you should be able to restrict network traffic between projects and pods
- Managing Network Policies in OpenShift
- How to create network policies
- Example use-cases for network policies

## **5.6.** Guided Exercise: Configuring Network Policies

- In this exercise, you will create network policies and review pod isolation created by these network policies. You will be able to:-
  - Create network policies to control communication between pods.
  - Verify ingress traffic is limited to pods.

## **5.7.** Lab: Configuring OpenShift Networking for Applications

- In this review, you deploy a PHP application that prints some information about the system. The application is available with two different configurations: one that runs with an unencrypted network that listens on port 8080, and one that uses a TLS certificate to encrypt the network traffic, which listens on port 8443.
- In this lab, you will configure a TLS passthrough route for your application. You should be able to:-
  - Deploy an application and configure an insecure route.
  - Restrict traffic to the applications.
  - Generate a TLS certificate for an application.
  - Configure a passthrough route for an application with a TLS certificate.

# **Chapter 6:** Controlling Pod Scheduling **[IMPORTANT]**

## **6.1.** Controlling Pod Scheduling Behavior

- After completing this section, you should be able to describe pod scheduling algorithms, the methods used to influence scheduling, and apply these methods.
- Introducing the OpenShift Scheduler Algorithm
- Scheduling and Topology
- Labeling Nodes (oc label node command)
- Labeling Machine Sets
- Controlling Pod Placement
- Configuring a Node Selector for a Project (oc adm new-project)
- Scaling the Number of Pod Replicas

## **6.2.** Guided Exercise: Controlling Pod Scheduling Behavior

- In this exercise, you will configure an application to run on a subset of the cluster worker nodes. You should be able to use the OpenShift command-line interface to:-
  - Add a new label to a node.
  - Deploy pods to nodes that match a specified label.
  - Remove a label from a node.
  - Troubleshoot when pods fail to deploy to a node.

## **6.3.** Limiting Resource Usage by an Application

- After completing this section, you should be able to limit the resources consumed by containers, pods, and projects.
- Defining Resource Requests and Limits for Pods (oc set resources)
- Viewing Requests, Limits, and Actual Usage
- Applying Quotas (oc create quota)
- Applying Limit Ranges
- Applying Quotas to Multiple Projects
- Customizing the Default Project Template

## **6.4.** Guided Exercise: Limiting Resource Usage by an Application

- In this exercise, you will configure an application so that it does not consume all computing resources from the cluster and its worker nodes. You should be able to use the OpenShift command-line interface to:-
  - Configure an application to specify resource requests for CPU and memory usage.
  - Modify an application to work within existing cluster restrictions.
  - Create a quota to limit the total amount of CPU, memory, and configuration maps available to a project.

## **6.5.** Scaling an Application

- After completing this section, students should be able to:-
  - Control the number of replicas of a pod.
  - Specify the number of replicas in a deployment or deployment configuration resource.
  - Manually scale the number of replicas.
  - Create a horizontal pod autoscaler (HPA) resource.
- Specifying Pod Replicas in Configuration Workloads
- Manually Scaling the Number of Pod Replicas (oc scale)
- Autoscaling Pods (oc autoscale)

## **6.6.** Guided Exercise: Scaling an Application

- In this exercise, you will scale an application manually and automatically. You should be able to use the OpenShift command-line interface to:-
  - Manually scale an application.
  - Configure an application to automatically scale based on usage.

## **6.7.** Lab: Controlling Pod Scheduling

- In this lab, you will configure an application to run on a subset of the cluster nodes, and to scale with load. You should be able to use the OpenShift command-line interface to:-
  - Add a new label to nodes.
  - Deploy pods to nodes that match a specified label.
  - Request CPU and memory resources for pods.
  - Configure an application to scale automatically.
  - Create a quota to limit the amount of resources a project can consume.

# **Chapter 7:** Describing Cluster Updates

## **7.1.** Introducing Cluster Updates

- Introducing Cluster Updates
- Upgrade Channels (Update Paths)
  - Candidate Channel
  - Fast Channel
  - Stable Channel
- Changing the Update Channel
- Describing _Over The Air(OTA)_ Updates
- Updating the Cluster

# **Chapter 8:** Managing a Cluster with the Web Console **[IMPORTANT]**

## **8.1.** Performing Cluster Administration

- Describing the Web Console Components and options
  - Home
  - Operators
  - Workloads, Networking and Storage
  - Builds
  - Monitoring
  - Compute
  - User Managemnt
  - Administration
- Accessing the OpenShift Web Console
- Creating Users and Groups
- Creating a Project
- Limitations of Web Console

## **8.2.** Guided Exercise: Performing Cluster Administration

- In this exercise, you will perform cluster administration with the web console
- You should be able to use the OpenShift web console to:-
  - Find resources associated with an operator.
  - Review a pod's status, YAML definition, and logs.
  - View and edit cluster configuration resources.
  - Create a new project and configure its resource quotas, limit ranges, and role-based access control (RBAC). 

## **8.3.** Managing Workloads and Operators

- After completing this section, you should be able to manage applications and Kubernetes Operators with the web console
- Exploring Workload Resources
- Managing Workloads
- Deploying Applications
- Installing and Using Operators

## **8.4.** Guided Exercise: Managing Workloads and Operators

- In this exercise, you will manage cluster workloads with the web console.
- You should be able to use the OpenShift web console to:-
  - Install an operator from OperatorHub
  - Use a custom resource to create a database.
  - Deploy and troubleshoot an application that uses the operator-managed resources.

## **8.5.** Examining Cluster Metrics

- After completing this section, you should be able to examine performance and health metrics for cluster nodes and applications
- Viewing Cluster Metrics
- Viewing Resource Metrics
- Performing Prometheus Queries in the Web Console

## **8.6.** Guided Exercise: Examining Cluster Metrics

- In this exercise, you will examine the metrics page and dashboard within the web console
- You should be able to use the Red Hat OpenShift web console to:-
  - View cluster, project, pod, and node metrics.
  - Identify a pod consuming large amounts of memory or CPU.

## **8.7.** Lab: Managing a Cluster with the Web Console

- In this lab, you will manage the OpenShift cluster using the web console.
- You should be able to use the OpenShift web console to:-
  - Modify a secret to add htpasswd entries for new users.
  - Configure a new project with role-based access controls and resource quotas.
  - Use an OperatorHub operator to deploy a database.
  - Create a deployment, service, and route for a web application.
  - Troubleshoot an application using events and logs.