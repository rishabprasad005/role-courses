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

## **2.6.** Introducing OpenShift Dynamic Storage [GUIDED EXCERCISE]

- In this exercise, you will deploy a PostgreSQL database using a persistent volume claim and identify its dynamically allocated volume.
- You should be able to:-
  - Identify the default storage settings of an OpenShift cluster.
  - Create persistent volume claims.
  - Manage persistent volumes.
