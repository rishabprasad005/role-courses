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

## **3.4.** Guided Exercise: Defining and Applying Permissions using RBAC [IMPORTANT]

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


# **Chapter 4:** Configuring Application Security [IMPORTANT]

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