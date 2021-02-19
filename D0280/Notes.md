# **Chapter 1:** Describing the Red Hat OpenShift Container Platform

## **1.1.** Red Hat OpenShift Container Platform Features

- Container orchestration is a fundamental enabler of digital transformation initiatives. However, as monolithic applications transition to containerized services, it can be tedious to manage these applications with legacy infrastructure. Red Hat OpenShift Container Platform (RHOCP) allows developers and IT organizations to better manage application life cycles.

    Red Hat OpenShift Container Platform is a containerized application platform that allows enterprises to manage and scale applications utilizing container deployments. OpenShift provides predefined application environments, based upon Kubernetes, to support DevOps principles such as reduced time to market, infrastructure-as-code, continuous integration (CI), and continuous delivery (CD).

    Similar to Linux distributions(RHEl, Ubuntu), OpenShift is a Kubernetes distribution. RHOCP is based on the Kubernetes open source project and extends the platform with features that bring a robust, flexible, and scalable container platform to customer data centers, enabling developers to run their workload in a high availability environment.

- **Kubernetes vs OpenShift:** A lot of functionality from Kubernetes depends on external components, such as container registry server, ingress controllers, storage plug-ins, network plug-ins, authentication plug-ins, access control and network isolation.

    OpenShift is a Kubernetes distribution that provides many of these components already integrated and configured, and managed by operators. Which means openShift provides a number of services on top of Kubernetes, such as a web console, an internal container image registry, storage, networking providers, and centralized logging and monitoring.

    OpenShift also adds to Kubernetes a series of extension APIs and custom resources. For example, build configurations for the Source-to-Image process, and route resources to manage external access to the cluster.

- The Red Hat OpenShift product family includes a set of solutions to improve the delivery of business applications in a variety of environments ( Red Hat OpenShift Container Platform, Red Hat OpenShift Dedicated, Red Hat OpenShift Online, Red Hat OpenShift Kubernetes Engine, Red Hat Code Ready Containers)

- **Clusters provide three types of load balancers:-**

  - an external load balancer, which manages access to the OpenShift API 
  - the HAProxy load balancer, for external access to applications 
  - The internal load balancer, which uses Netfilter rules for internal access to applications and services.

- The technology that external load balancers use is dependent on the cloud provider that runs your cluster.

- Route resources use HAProxy for load-balancing and to manage external access to the cluster.

- Service resources use Netfilter rules for load-balancing and to manage traffic from inside the cluster.

- RHOCP ships with an advanced monitoring solution, based on Prometheus, which gathers hundreds of metrics about your cluster. This solution interacts with an alerting system that allows you to obtain detailed information about your cluster activity and health. OpenShift uses metrics from Prometheus to dynamically scale application pods.

- RHOCP ships with an advanced aggregated logging solution, based on Elasticsearch, which allows long-term retention of logs from cluster nodes and containers.

- Kubernetes adds an abstraction layer between the storage back end and the storage consumption. As such, applications can consume long-lived, short-lived, block, and file-based storage using unified storage definitions that are independent of the storage back end. This way your applications are not dependent on particular cloud provider storage APIs.

    RHOCP embeds a number of storage providers that allow for automatic provisioning of storage on popular cloud providers and virtualization platforms, and so cluster administrators do not need to manage the fine details of proprietary storage arrays.

- Red Hat, in collaboration with AWS, Google Cloud, and Microsoft, launched the OperatorHub, accessible at <https://operatorhub.io>. The platform is a public repository and marketplace for operators compatible with OpenShift and other distributions of Kubernetes that include the OLM.

    Red Hat Marketplace is a platform that allows access to certified software packaged as Kubernetes operators that can be deployed in an OpenShift cluster. The certified software includes automatic deployments and seamless upgrades for an integrated experience.

## **1.3** Describing the Architecture of OpenShift

- The architecture of OpenShift is based on the declarative nature of Kubernetes. Declarative architectures allow for self-optimizing and self-healing systems that are easier to manage than imperative architectures.

- A Kubernetes cluster consists of a set of nodes that run the kubelet system service and a container engine. OpenShift runs exclusively the CRI-O container engine.

    Some nodes in the cluster are control plane nodes that run the REST API, the etcd database, and the platform controllers. OpenShift configures its control plane nodes so that they are not schedulable to run end-user application pods and are dedicated to running the control plane services. OpenShift schedules end-user application pods to be executed on the worker nodes.

- Unlike many container platforms that focus on cloud-native, stateless applications, OpenShift also supports stateful applications that do not follow the standard Twelve-Factor App methodology.

    OpenShift supports stateful applications by offering a comprehensive set of storage capabilities and supporting operators. OpenShift ships with integrated storage plug-ins and storage classes that rely on the underlying cloud or virtualization platform to provide dynamically provisioned storage.

    For example, if you install OpenShift on Amazon Web Services (AWS), your OpenShift cluster comes pre-configured with a default storage class that uses AWS EBS service automatically to provision storage volumes on-demand. Users can deploy an application that requires persistent storage, such as a database, and OpenShift automatically creates an EBS volume to host the application data.

    OpenShift cluster administrators can later define additional storage classes that use different EBS service tiers. For example, you could have one storage class for high-performance storage that sustains a high input-output operations per second (IOPS) rate, and another storage class for low-performance, low-cost storage. Cluster administrators can then allow only certain applications to use the high-performance storage class, and configure data archiving applications to use the low-performance storage class.

## **1.5.** Describing Cluster Operators

- Kubernetes operators are applications that invoke the Kubernetes API directly to manage Kubernetes resources. operators, unlike common applications, require direct access to the Kubernetes resources, they usually require custom security settings.

    Operators usually define custom resources (CR) that store their settings and configurations. An OpenShift administrator manages an operator by editing its custom resources. The syntax of a custom resource is defined by a custom resource definition (CRD).

    The purpose of an operator is to automate tasks that a human administrator (or human operator) would perform to deploy, update, and manage an application.

- You can develop operators using your preferred programming language. Technically you do not need a special-purpose SDK to develop an operator. All you need is the ability to invoke REST APIs and consume secrets that contain access credentials to the Kubernetes APIs.

- The Operator Framework is an open source toolkit for building, testing, and packaging operators. The Operator Framework makes these tasks easier than coding directly to low-level Kubernetes APIs by providing the following components:-

  - **Operator Software Development Kit (Operator SDK):** Provides a set of Golang libraries and source code examples that implement common patterns in operator applications. It also provides a container image and playbook examples that allow you to develop operators using Ansible. 
  - **Operator Life Cycle Manager (OLM):** Provides an application that manages the deployment, resource utilization, updates, and deletion of operators that have been deployed through an operator catalog. The OLM itself is an operator that comes preinstalled with OpenShift. Hence, OLM can be said as an operator for the operators.

    The Operator Framework also defines a set of recommended practices for implementing operators and CRDs and a standard way of packaging an operator manifest as a container image, that allows an operator to be distributed using an operator catalog. The most common form of an operator catalog is an image registry server.

    An operator container image that follows the Operator Framework standards contains all resource definitions required to deploy the operator application. This way the OLM can install an operator automatically. If an operator is not built and packaged by following the Operator Framework standards, the OLM will not be able to install nor manage that operator.
- **Introducing OperatorHub:** OperatorHub provides a web interface to discover and publish operators that follow the Operator Framework standards. Both open source operators and commercial operators can be published to the Operator hub. Operator container images can be hosted at different image registries, for example quay.io.

- **Red Hat Marketplace** is a platform that allows access to a curated set of certified softwares packaged as Kubernetes operators that can be deployed on an OpenShift or a Kubernetes cluster. The certified software includes automatic deployments and seamless upgrades for an integrated experience Operators available in the Red Hat Marketplace have gone through a certification process to ensure the software follows best practices and also the containers are scanned for vulnerabilities.

- Cluster operators are regular operators except that they are not managed by the OLM. They are managed by the OpenShift Cluster Version Operator. OpenShift cluster operators provide OpenShift extension APIs and infrastructure services such as:-

  - The OAuth server, which authenticates access to the control plane and extensions APIs.
  - The core DNS server, which manages service discovery inside the cluster.
  - The web console, which allows graphical management of the cluster.
  - The internal image registry, which allow developers to host container images inside the cluster, using either S2I or another mechanism.
  - The monitoring stack, which generates metrics and alerts about the cluster health.

- OpenShift Cluster Version Operator are sometimes called a first-level operator and all cluster operators are also called second-level operators.

- **Operator Terminologies:-**  
  - **Operator:** An application that manages Kubernetes resources
  - **Operator Lifecycle Manager (OLM):** An application that manages Kubernetes operators
  - **Operator Image:** The artifact defined by the Operator Framework that you can publish for consumption by an OLM instance
  - **Operator SDK:** An open source toolkit for building, testing, and packaging operators
  - **Custom Resource Definition (CRD):** An extension of the Kubernetes API that defines the syntax of a custom resource
  - **OperatorHub:** A public web service where you can publish operators that are compatible with the OLM
  - **Operator Catalogue:** A repository for discovering and installing operators
  - **Red Hat Marketplace:** Platform that allows access to certified software packaged as Kubernetes operators that can be deployed in an OpenShift cluster

## 1.7. Summary:-

- Red Hat OpenShift Container Platform is based on Red Hat Enterprise Linux CoreOS, the CRI-O container engine, and Kubernetes.
- RHOCP 4 provides a number of services on top of Kubernetes, such as an internal container image registry, storage, networking providers, and centralized logging and monitoring.
- Operators package applications that manage Kubernetes resources, and the Operator Lifecycle Manager (OLM) handles installation and management of operators.
- OperatorHub.io is an online catalog for discovering operators.
  
# **Chapter 2:** Verifying the Health of a Cluster

## **2.1** Describing OpenShift Installation Methods

- Red Hat OpenShift Container Platform provides two main installation methods:-
    
  - 