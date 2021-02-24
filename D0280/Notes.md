# **Chapter 1:** Describing the Red Hat OpenShift Container Platform

## **1.1.** Red Hat OpenShift Container Platform Features

- Container orchestration is a fundamental enabler of digital transformation initiatives. However, as monolithic applications transition to containerized services, it can be tedious to manage these applications with legacy infrastructure. Red Hat OpenShift Container Platform (RHOCP) allows developers and IT organizations to better manage application life cycles.

    Red Hat OpenShift Container Platform is a containerized application platform that allows enterprises to manage and scale applications utilizing container deployments. OpenShift provides predefined application environments, based upon Kubernetes, to support DevOps principles such as reduced time to market, infrastructure-as-code, continuous integration (CI), and continuous delivery (CD).

    Similar to Linux distributions(RHEl, Ubuntu), OpenShift is a Kubernetes distribution. RHOCP is based on the Kubernetes open source project and extends the platform with features that bring a robust, flexible, and scalable container platform to customer data centers, enabling developers to run their workload in a high availability environment.

- **Kubernetes vs OpenShift:** A lot of functionality from Kubernetes depends on external components, such as container registry server, ingress controllers, storage plug-ins, network plug-ins, authentication plug-ins, access control and network isolation.

    OpenShift is a Kubernetes distribution that provides many of these components already integrated and configured, and managed by operators. Which means openShift provides a number of services on top of Kubernetes, such as a web console, an internal container image registry, storage, networking providers, and centralized logging and monitoring.

    OpenShift also adds to Kubernetes a series of extension APIs and custom resources. For example, build configurations for the Source-to-Image process, and route resources to manage external access to the cluster.

- The Red Hat OpenShift product family includes a set of solutions to improve the delivery of business applications in a variety of environments ( Red Hat OpenShift Container Platform, Red Hat OpenShift Dedicated, Red Hat OpenShift Online, Red Hat OpenShift Kubernetes Engine, Red Hat Code Ready Containers)

- **OpenShift Cluster provide three types of load balancers:-**

  - an external load balancer, which manages access to the OpenShift API 
  - the HAProxy load balancer, for external access to applications 
  - The internal load balancer, which uses Netfilter rules for internal access to applications and services.

  The technology that external load balancers use is dependent on the cloud provider that runs your cluster.

  Route resources use HAProxy for load-balancing and to manage external access to the cluster.

  Service resources use Netfilter rules for load-balancing and to manage traffic from inside the cluster.

- RHOCP ships with an advanced monitoring solution, based on Prometheus, which gathers hundreds of metrics about your cluster. This solution interacts with an alerting system that allows you to obtain detailed information about your cluster activity and health. **OpenShift uses metrics from Prometheus to dynamically scale application pods.**

- RHOCP ships with an advanced aggregated logging solution, based on Elasticsearch, which allows long-term retention of logs from cluster nodes and containers.

- Kubernetes adds an abstraction layer between the storage back end and the storage consumption. As such, applications can consume long-lived, short-lived, block, and file-based storage using unified storage definitions that are independent of the storage back end. This way your applications are not dependent on particular cloud provider storage APIs.

    RHOCP embeds a number of storage providers that allow for automatic provisioning of storage on popular cloud providers and virtualization platforms, and so cluster administrators do not need to manage the fine details of proprietary storage arrays.

- **OperatorHub:** Red Hat, in collaboration with AWS, Google Cloud, and Microsoft, launched the OperatorHub, accessible at <https://operatorhub.io>. The platform is a public repository and marketplace for operators compatible with OpenShift and other distributions of Kubernetes that include the OLM.

- **Red Hat Marketplace** is a platform that allows access to a curated set of certified softwares packaged as Kubernetes operators that can be deployed on an OpenShift or a Kubernetes cluster. The certified software includes automatic deployments and seamless upgrades for an integrated experience Operators available in the Red Hat Marketplace have gone through a certification process to ensure the software follows best practices and also the containers are scanned for vulnerabilities.

## **1.3.** Describing the Architecture of OpenShift

- The architecture of OpenShift is based on the declarative nature of Kubernetes. Declarative architectures allow for self-optimizing and self-healing systems that are easier to manage than imperative architectures.

- A Kubernetes cluster consists of a set of nodes that run the kubelet system service and a container engine. OpenShift runs exclusively the CRI-O container engine.

    Some nodes in the cluster are **control plane nodes** that run the REST API, the etcd database, and the platform controllers. OpenShift configures its control plane nodes so that they are not schedulable to run end-user application pods and are dedicated to running the control plane services. OpenShift schedules end-user application pods to be executed on the worker nodes.

- Unlike many container platforms that focus on cloud-native, stateless applications, OpenShift also supports stateful applications that do not follow the standard **Twelve-Factor App** methodology.

    OpenShift supports **stateful applications** by offering a comprehensive set of storage capabilities and supporting operators. OpenShift ships with integrated storage plug-ins and storage classes that rely on the underlying cloud or virtualization platform to provide dynamically provisioned storage.

    For example, if you install OpenShift on Amazon Web Services (AWS), your OpenShift cluster comes pre-configured with a default storage class that uses AWS EBS service automatically to provision storage volumes on-demand. Users can deploy an application that requires persistent storage, such as a database, and OpenShift automatically creates an EBS volume to host the application data.

    OpenShift cluster administrators can later define additional storage classes that use different EBS service tiers. For example, you could have one storage class for high-performance storage that sustains a high input-output operations per second (IOPS) rate, and another storage class for low-performance, low-cost storage. Cluster administrators can then allow only certain applications to use the high-performance storage class, and configure data archiving applications to use the low-performance storage class.

## **1.5.** Describing Cluster Operators

- A Kubernetes application is an app that is both deployed on Kubernetes and managed using the Kubernetes APIs and kubectl or oc tooling.
  
- Operators are a method of packaging, deploying, and managing a kubernetes application. They act like an extension of the software vendor’s engineering team, watching over an OpenShift Container Platform environment and using its current state to make decisions in real time. Operators are designed to handle upgrades seamlessly, react to failures automatically, and not take shortcuts, such as skipping a software backup process to save time.
  
- Kubernetes operators are applications that invoke the Kubernetes API directly to manage Kubernetes resources. operators, unlike common applications, require direct access to the Kubernetes resources, they usually require custom security settings.

    Operators usually define custom resources (CR) that store their settings and configurations. An OpenShift administrator manages an operator by editing its custom resources. The syntax of a custom resource is defined by a custom resource definition (CRD).

    The purpose of an operator is to automate tasks that a human administrator (or human operator) would perform to deploy, update, and manage an application.

- You can develop operators using your preferred programming language. Technically you do not need a special-purpose SDK to develop an operator. All you need is the ability to invoke REST APIs and consume secrets that contain access credentials to the Kubernetes APIs.

- The Operator Framework is a family of tools and capabilities to deliver on the customer experience described above. It is not just about writing code; testing, delivering, and updating Operators is just as important. The Operator Framework components consist of open source tools to tackle these problems. The Operator Framework makes these tasks easier than coding directly to low-level Kubernetes APIs by providing the following components:-

  - **Operator Software Development Kit (Operator SDK):** Provides a set of Golang libraries and source code examples that implement common patterns in operator applications. It also provides a container image and playbook examples that allow you to develop operators using Ansible. The Operator SDK assists Operator authors in bootstrapping, building, testing, and packaging their own Operator based on their expertise without requiring knowledge of Kubernetes API complexities.
  
  - **Operator Life Cycle Manager (OLM):** Provides an application that manages the deployment, resource utilization, updates, and deletion of operators that have been deployed through an operator catalog. The OLM itself is an operator that comes preinstalled with OpenShift. Hence, OLM can be said as "_An operator for the operators_".

    The Operator Framework also defines a set of recommended practices for implementing operators and CRDs and a standard way of packaging an operator manifest as a container image, that allows an operator to be distributed using an operator catalog. The most common form of an operator catalog is an image registry server.

    An operator container image that follows the Operator Framework standards contains all resource definitions required to deploy the operator application. This way the OLM can install an operator automatically. If an operator is not built and packaged by following the Operator Framework standards, the OLM will not be able to install nor manage that operator.

  - **Operator Registry:** The Operator Registry stores cluster service versions (CSVs) and custom resource definitions (CRDs) for creation in a cluster and stores Operator metadata about packages and channels. It runs in a Kubernetes or OpenShift cluster to provide this Operator catalog data to OLM.


  - **OperatorHub:** OperatorHub is a web console for cluster administrators to discover and select Operators to install on their cluster, that follow the Operator Framework standards. It is deployed by default in OpenShift Container Platform. OperatorHub also provides a web interface to publish operators. Both open source operators and commercial operators can be published to the Operator hub. Operator container images can be hosted at different image registries, for example quay.io.

  - **Operator Metering:** Operator Metering collects operational metrics about Operators on the cluster for Day 2 management and aggregating usage metrics.

- **Cluster operators:** OpenShift Container Platform includes a default set of Operators called _Cluster Operators_, that are required for proper functioning of the cluster. These are regular operators except that they are not managed by the OLM. They are managed by the OpenShift Cluster Version Operator. OpenShift cluster operators provide OpenShift extension APIs and infrastructure services such as:-

  - The OAuth server, which authenticates access to the control plane and extensions APIs.
  - The core DNS server, which manages service discovery inside the cluster.
  - The web console, which allows graphical management of the cluster.
  - The internal image registry, which allow developers to host container images inside the cluster, using either S2I or another mechanism.
  - The monitoring stack, which generates metrics and alerts about the cluster health.

  **Extra Notes:**
  - As a cluster administrator, you can install application Operators from the OperatorHub using the OpenShift Container Platform web console or the CLI. You can then subscribe the Operator to one or more namespaces to make it available for developers on your cluster. Application Operators are managed by Operator Lifecycle Manager (OLM).

  - Default OpenShift Container Platform cluster Operators are managed by the Cluster Version Operator (CVO) and they do not have a Subscription object. Application Operators are managed by Operator Lifecycle Manager (OLM) and they have a Subscription object.

  - OpenShift Cluster Version Operator are sometimes called a first-level operator and all cluster operators are also called second-level operators.

- **Operator Terminologies:-**  
  - **Operator:** An application that manages Kubernetes resources
  - **Operator Lifecycle Manager (OLM):** An application that manages Kubernetes operators
  - **Operator Image:** The artifact defined by the Operator Framework that you can publish for consumption by an OLM instance
  - **Operator SDK:** An open source toolkit for building, testing, and packaging operators
  - **Custom Resource Definition (CRD):** An extension of the Kubernetes API that defines the syntax of a custom resource
  - **OperatorHub:** A public web service where you can publish operators that are compatible with the OLM
  - **Operator Catalogue:** A repository for discovering and installing operators (OperatorHub is an operator catalogue, which only contains operators that are compatible with the OLM)
  - **Red Hat Marketplace:** Platform that allows access to certified software packaged as Kubernetes operators that can be deployed in an OpenShift cluster

## 1.7. Summary:-

- Red Hat OpenShift Container Platform is based on Red Hat Enterprise Linux CoreOS, the CRI-O container engine, and Kubernetes.
- RHOCP 4 provides a number of services on top of Kubernetes, such as an internal container image registry, storage, networking providers, and centralized logging and monitoring.
- Operators package applications that manage Kubernetes resources, and the Operator Lifecycle Manager (OLM) handles installation and management of operators.
- OperatorHub.io is an online catalog for discovering operators.

<br/>
  
# **Chapter 2:** Verifying the Health of a Cluster

## **2.1.** Describing OpenShift Installation Methods

- Red Hat OpenShift Container Platform provides two main installation methods:-
    
  - **Full-stack Automation:** With this method, the OpenShift installer provisions all compute, storage, and network resources from a cloud or virtualization provider. You provide the installer with minimum data, such as credentials to a cloud provider and the size of the initial cluster, and then the installer deploys a fully functional OpenShift cluster.
  
  - **Pre-existing Infrastructure:** With this method, you configure a set of compute, storage, and network resources and the OpenShift installer configures an initial cluster using these resources. You can use this method to set up an OpenShift cluster using bare-metal servers and cloud or virtualization providers that are not supported by the full-stack automation method.

- At the time of the Red Hat OpenShift Container Platform 4.5 release, the set of cloud providers supported for the full-stack automation method includes Amazon Web Services (AWS), Google Cloud Platform (GCP), Microsoft Azure, and Red Hat OpenStack Platform using the standard Intel architecture (x86). Supported virtualization providers and architectures for full-stack automation include VMware, Red Hat Virtualization, IBM Power, and IBM System Z.

- **Comparing Installation methods:** Certain features of OpenShift require using the full-stack automation method, for example, cluster automatic scaling. However, it is expected that future releases might relax such requirements.

    Using the full-stack automation method, all nodes of the new cluster run Red Hat Enterprise Linux CoreOS (RHEL CoreOS). Using the pre-existing infrastructure method, worker nodes can be set up using Red Hat Enterprise Linux (RHEL), but the control plane (master nodes) still requires RHEL CoreOS.

## **2.5.** Introducing OpenShift Dynamic Storage

- Containers have ephemeral storage by default. For example, when a container is deleted, all the files and data inside it are deleted also. To preserve the files, containers offer **two main ways of maintaining persistent storage: volumes and bind mounts**. Volumes are the preferred OpenShift way of managing persistent storage. Developers working with containers on a local system can mount a local directory into a container using a bind mount.
  
- Volumes are managed manually by the administrator or dynamically through a storage class.

- OpenShift cluster administrators use the Kubernetes persistent volume framework to manage persistent storage for the users of a cluster. There are two ways of provisioning storage for the cluster: static and dynamic. Static provisioning requires the cluster administrator to create persistent volumes manually. Dynamic provisioning uses storage classes to create the persistent volumes on demand.
  
- A persistent volume claim (PVC) belongs to a specific project. To create a PVC, you must specify the access mode and size, among other options. Once created, a PVC cannot be shared between projects. Developers use a PVC to access a persistent volume (PV). Persistent volumes are not exclusive to projects and are accessible across the entire OpenShift cluster. When a persistent volume binds to a persistent volume claim, the persistent volume cannot be bound to another persistent volume claim.

- If a PVC cannot find a PV that matches all criteria, the PVC enters a pending state and waits until an appropriate PV becomes available. A cluster administrator can manually create the PV or a storage class can dynamically create the PV. A persistent volume claim that does not specify a storage class uses the default storage class. A bound persistent volume can be mounted as a volume to a specific mount point in the pod (for example, /var/lib/pgsql for a PostgreSQL database).

- To add a volume to an application create a _PersistentVolumeClaim_ resource and add it to the application as a volume. Create the persistent volume claim using either a Kubernetes manifest or the oc set volumes command.

- OpenShift defines three access modes that are summarized below:-
  - **ReadWriteMany (RWX):** Kubernetes can mount the volume as read-write on many nodes.
  - **ReadOnlyMany(ROX):** Kubernetes can mount the volume as read-only on many nodes.
  - **ReadWriteOnce(RWO):** Kubernetes can mount the volume as read-write on only a single node.

## **2.7.** Summary

- Red Hat OpenShift Container Platform provides two main installation methods: full-stack automation, and pre-existing infrastructure.

- Future releases are expected to add more cloud and virtualization providers, such as VMware, Red Hat Virtualization, and IBM System Z.

- An OpenShift node based on Red Hat Enterprise Linux CoreOS runs very few local services that would require direct access to a node to inspect their status. Most of the system services run as containers, the main exceptions are the CRI-O container engine and the Kubelet.

- The oc get node, oc adm top, oc adm node-logs, and oc adm debug commands provide troubleshooting information about OpenShift nodes.


# **Chapter 3:** Configuring Authentication and Authorization

## **3.1.** Configuring Identity Providers

- There are several OpenShift resources related to authentication and authorization:-

  - **User:** users are entities that interact with the API server. Assign permissions by adding roles to the user directly or to the groups of which the user is a member.
  - **Identity:** The identity resource keeps a record of successful authentication attempts from a specific user and identity provider. Any data concerning the source of the authentication is stored on the identity. Only a single user resource is associated with an identity resource. 
  - **Service Account:** In OpenShift, applications can communicate with the API independently when user credentials cannot be acquired. To preserve the integrity of a regular user's credentials, credentials are not shared and service accounts are used instead. Service accounts enable you to control API access without the need to borrow a regular user's credentials. 
  - **Group:** Groups represent a specific set of users. Users are assigned to one or to multiple groups. Groups are leveraged when implementing authorization policies to assign permissions to multiple users at the same time. For example, if you want to allow twenty users access to objects within a project, then it is advantageous to use a group instead of granting access to each of the users individually. OpenShift Container Platform also provides system groups or virtual groups that are provisioned automatically by the cluster. 
  - **Role:**      A role defines a set of permissions that enables a user to perform API operations over one or more resource types. You grant permissions to users, groups, and service accounts by assigning roles to them. 

  User and identity resources are usually not created in advance. They are usually created automatically by OpenShift after a successful interactive log in using OAuth.

- Authentication and authorization are the two security layers responsible for enabling user interaction with the cluster. When a user makes a request to the API, the API associates the user with the request. The authentication layer authenticates the user. Upon successful authentication, the authorization layer decides to either honor or reject the API request. The authorization layer uses role-based access control (RBAC) policies to determine user privileges.

- The OpenShift API has two methods for authenticating requests:-

  - OAuth Access Tokens
  - X.509 Client Certificates 

  If the request does not present an access token or certificate, then the authentication layer assigns it the **system:anonymous** virtual user, and the **system:unauthenticated** virtual group.

- The OpenShift Container Platform provides the Authentication operator, which runs an OAuth server. The OAuth server provides OAuth access tokens to users when they attempt to authenticate to the API. An identity provider must be configured and available to the OAuth server. The OAuth server uses an identity provider to validate the identity of the requester. The server reconciles the user with the identity and creates the OAuth access token for the user. OpenShift automatically creates identity and user resources after a successful login.

- OpenShift OAuth server can be configured to use many identity providers such as HTPasswd, Keystone, LDAP, GitHub or OpenID Connect etc. The OAuth custom resource must be updated with your desired identity provider. You can define multiple identity providers, of the same or different kinds, on the same OAuth custom resource.

- Before you can configure an identity provider and manage users, you must access your OpenShift cluster as a cluster administrator. A newly-installed OpenShift cluster provides two ways to authenticate API requests with cluster administrator privileges:-

  - Authenticate as the kubeadmin virtual user. Successful authentication grants an OAuth access token.
  - Use the kubeconfig file, which embeds an X.509 client certificate that never expires.
  
  To create additional users and grant them different access levels, you must configure an identity provider and assign roles to your users.

- The cluster-wide cluster-admin role grants cluster administration privileges to users and groups. This role enables the user to perform any action on any resources within the cluster. The following example assigns the cluster-admin role to the student user. 

  ```bash
  [user@demo ~]$ oc adm policy add-cluster-role-to-user cluster-admin student
  ```

## **3.3.** Defining and Applying Permissions Using RBAC

- Role-based access control (RBAC) is a technique for managing access to resources in a computer system. In Red Hat OpenShift, RBAC determines if a user can perform certain actions within the cluster or project. There are two types of roles that can be used depending on the user's level of responsibility: cluster and local.

- **Authorization Process:** Authorization is a separate step from authentication. The authorization process is managed by rules, roles, and bindings.

  RBAC Object  | Description
  -------------|------------
  Rule  | Allowed actions for objects or groups of objects.
  Role  | Sets of rules. Users and groups can be associated with multiple roles.
  Binding  | Assignment of users or groups to a role.

- **RBAC Scope:** RHOCP defines two groups of roles and bindings depending on the user's scope and responsibility: cluster roles and local roles. Cluster role bindings take precedence over local role bindings.

    Role Level  | Description
    -------------|------------
    Cluster Role | Users or groups with this role level can manage the OpenShift cluster.
    Local Role | Users or groups with this role level can only manage elements at a project level.

- Cluster administrators can use the **oc adm policy** command to both add and remove cluster roles and namespace roles.

- Project administrators can use the **oc policy** command to add and remove namespace roles. 

- OpenShift ships with a set of default cluster roles that can be assigned locally or to the entire cluster. You can modify these roles for fine-grained access control to OpenShift resources, but additional steps are required that are outside the scope of this course.

  Default roles  | Description
  ---------------|------------
  admin | Users with this role can manage all project resources, including granting access to other users to access the project. The admin role gives a user access to project resources such as quotas and limit ranges, and also the ability to create new applications.
  basic-user | Users with this role have read access to the project.
  cluster-admin | Users with this role have superuser access to the cluster   resources. These users can perform any action on the cluster, and have full   control of all projects.
  cluster-status | Users with this role can get cluster status information.
  edit  | Users with this role can create, change, and delete common   application resources from the project, such as services and deployment   configurations. These users cannot act on management resources such as limit   ranges and quotas, and cannot manage access permissions to the project. he edit role gives a user sufficient access to act as a developer inside the project, but working under the constraints configured by a project administrator. 
  self-provisioner | Users with this role can create new projects. This is a   cluster role, not a project role.
  view | Users with this role can view project resources, but cannot modify   project resources. 
  

- Interaction with OpenShift Container Platform is associated with a user. An OpenShift Container Platform user object represents a user who can be granted permissions in the system by adding roles to that user or to a user's group via rolebindings. User Types are:-

  - **Regular Users:** This is the way most interactive OpenShift Container Platform users are represented. Regular users are represented with the User object. This type of user represents a person that has been allowed access to the platform. Examples of regular users include user1 and user2. 
  - **System Users:** Many of these are created automatically when the infrastructure is defined, mainly for the purpose of enabling the infrastructure to securely interact with the API. System users include a cluster administrator (with access to everything), a per-node user, users for routers and registries to use, and various others. An anonymous system user is used by default for unauthenticated requests. Examples of system users include: system:admin, system:openshift-registry, and system:node:node1.example.com. 
  - **Regular Users:** These are special system users associated with projects; some are created automatically when the project is first created, and project administrators can create more for the purpose of defining access to the contents of each project. Service accounts are often used to give extra privileges to pods or deployment configurations. Service accounts are represented with the ServiceAccount object. Examples of service account users include system:serviceaccount:default:deployer and system:serviceaccount:foo:builder. 

  Every user must authenticate before they can access OpenShift Container Platform. API requests with no authentication or invalid authentication are authenticated as requests by the anonymous system user. After successful authentication, policy determines what the user is authorized to do.

  ## **3.6.** Summary

 - A newly-installed OpenShift cluster provides two authentication methods that grant administrative access: the kubeconfig file and the kubeadmin virtual user.

- The HTPasswd identity provider authenticates users against credentials stored in a secret. The name of the secret, and other settings for the identity provider, are stored inside the OAuth custom resource.

- To manage user credentials using the HTPasswd identity provider, you must extract data from the secret, change that data using the htpasswd command, and then apply the data back to the secret.

- Creating OpenShift users requires valid credentials, managed by an identity provider, plus user and identity resources.

- Deleting OpenShift users requires deleting their credentials from the identity provider, and also deleting their user and identity resources.

- OpenShift uses role-based access control (RBAC) to control user actions. A role is a collection of rules that govern interaction with OpenShift resources. Default roles exist for cluster administrators, developers, and auditors.

- To control user interaction, assign a user to one or more roles. A role binding contains all of the associations of a role to users and groups.

- To grant a user cluster administrator privileges, assign the cluster-admin role to that user.


# **Chapter 4:** Configuring Application Security

## **4.1.** Managing Sensitive Information with Secrets

- Modern applications are designed to loosely couple code, configuration, and data. Configuration files and data are not hard-coded as part of the software. Instead, the software loads configuration and data from an external source. This enables deploying an application to different environments without requiring a change to the application source code.

- A secret can store any type of data. Data in a secret is Base64-encoded, not stored in plain text. Secret data is not encrypted; you can decode the secret from Base64 format to access the original data.

- Although secrets can store any type of data, Kubernetes and OpenShift support different types of secrets. Different types of secret resources exist, including service account tokens, SSH keys, and TLS certificates. When you store information in a specific secret resource type, Kubernetes validates that the data conforms to the type of secret.

- **NOTE**: You can encrypt the Etcd database, although this is not the default setting. When enabled, Etcd encrypts the following resources: secrets, configuration maps, routes, OAuth access tokens, and OAuth authorize tokens. Enabling Etcd encryption is outside the scope of this class.

- Secrets can be exposed to pods in two ways:-
  - Secrets as Pod Environment Variables
  - Secrets as Files in a Pod

- A secret can be mounted to a directory within a pod. A file is created for each key in the secret using the name of the key. The content of each file is the decoded value of the secret.

- The container image can dictate the location of the mount point and the expected file names. For example, a container image running NGINX can specify the SSL certificate location and the SSL certificate key location in the /etc/nginx/nginx.conf configuration file. If the expected files are not found, then the container might fail to run.
  
- If the mount point already exists in the pod, then any existing files at the mount point are obscured by the mounted secret. The existing files are not visible and are not accessible. 

- The main features of secrets include:-
  
  - Secret data can be shared within a project namespace.

  - Secret data is referenced independently of secret definition. Administrators can create and manage a secret resource that other team members can reference in their deployment configurations.

  - Secret data is injected into pods when OpenShift creates a pod. You can expose a secret as an environment variable or as a mounted file in the pod.

  - If the value of a secret changes during pod execution, the secret data in the pod does not update. After a secret value changes, you must create new pods to inject the new secret data.

  - Any secret data that OpenShift injects into a pod is ephemeral. If OpenShift exposes sensitive data to a pod as environment variables, then those variables are destroyed when the pod is destroyed.

  - Secret data volumes are backed by temporary file storage. If a secret is mounted as a file in the pod, then the file is also destroyed when the pod is destroyed. A stopped pod does not contain secret data.

  - If a pod requires access to sensitive information, then create a secret for the information before you deploy the pod. 

- Two primary use cases for secrets are storing credentials and securing communication between services. 
  - **Credentials:**  Store sensitive information, such as passwords and user names, in a secret.

    If an application expects to read sensitive information from a file, then you mount the secret as a data volume to the pod. The application can read the secret as an ordinary file to access the sensitive information. Some databases, for example, read credentials from a file to authenticate users.

    Some applications use environment variables to read configuration and sensitive data. You can link secret variables to pod environment variables in a deployment configuration.

  - **Transport Layer Security (TLS) and Key Pairs:** Use a TLS certificate and key to secure communication to a pod. A TLS secret stores the certificate as _tls.crt_ and the certificate key as _tls.key_. Developers can mount the secret as a volume and create a pass through route to the application.

## **4.3.** Controlling Application Permissions with Security Context Constraints

- **Security Context Constraints (SCCs):** Red Hat OpenShift provides security context constraints (SCCs), a security mechanism that restricts access to resources, but not to operations in OpenShift. 

- SCCs limits the access: From a running pod in OpenShift To the host environment. SCCs controls:-
  - Running privileged containers.
  - Requesting extra capabilities for a container
  - Using host directories as volumes.
  - Changing the SELinux context of a container.
  - Changing the user ID.

- You can run the `oc get scc` command as a cluster administrator to list the SCCs defined by OpenShift. OpenShift provides eight SCCs:-
  - anyuid
  - hostaccess
  - hostmount-anyuid
  - hostnetwork
  - node-exporter
  - nonroot
  - privileged
  - restricted
  
  **Note:** To get additional information about an SCC, use the oc describe command. For example:-

  ```bash
  oc describe scc anyuid
  ```

- Most pods created by OpenShift use the SCC named restricted, which provides limited access to resources external to OpenShift. Use the oc describe command to view the security context constraint that a pod uses. For example:-

  ```bash
  oc describe pod <pod-name> \
             -n openshift-console | grep scc
  ```

- **Privileged Containers:** Some containers developed by the community might require relaxed security context constraints to access resources that are forbidden by default, such as file systems, runtime environment of the host, sockets, or to access a SELinux context. For example, the S2I builder containers are a class of privileged containers that require access beyond the limits of their own containers. These containers can pose security risks because they can use any resources on an OpenShift node. Use SCCs to enable access for privileged containers by creating service accounts with privileged access.

- Container images downloaded from public container registries, such as Docker Hub, might fail to run using the restricted SCC. For example, a container image that requires running as a specific user ID can fail because the restricted SCC runs the container using a random user ID. A container image that listens on port 80 or port 443 can fail for a related reason. The random user ID used by the restricted SCC cannot start a service that listens on a privileged network port (port numbers less than 1024). Use the scc-subject-review subcommand to list all the security context constraints that can overcome the limitations of a container.

  ```bash
  oc get pod podname -o yaml | oc adm policy scc-subject-review -f -
  ```

- For the _anyuid_ SCC, the run as user strategy is defined as _RunAsAny_, which means that the pod can run as any user ID available in the container. This strategy allows containers that require a specific user to run the commands using a specific user ID.

- To change the container to run using a different SCC, you must create a service account bound to a pod. Use the `oc create serviceaccount` command to create the service account, and use the `-n` option if the service account must be created in a namespace different than the current one.

  ```bash
  oc create serviceaccount service-account-name
  ```

  To associate the service account with an SCC, use the `oc adm policy` command. Use the `-z` option to identify a service account, and use the `-n` option if the service account exists in a namespace different than the current one.

  ```bash
  oc adm policy add-scc-to-user <scc-name> -z service-account
  ```

  **NOTE:** Assigning an SCC to a service account or removing an SCC from a service account must be performed by a cluster administrator. Allowing pods to run with a less restrictive SCC can make your cluster less secure. Use with caution.

- Modify an existing deployment or deployment configuration to use the service account using the oc set serviceaccount command. If the command succeeds, then the pods associated with the deployment or deployment configuration redeploy.

  ```bash
  oc set serviceaccount deployment/deployment-name service-account-name
  ```


## **4.6.** Summary

- Secret resources allow you to separate sensitive information from application pods. You expose secrets to an application pod either as environment variables or as ordinary files.

- OpenShift uses security context constraints (SCCs) to define allowed pod interactions with system resources. By default, pods operate under the restricted context which limits access to node resources. 


# **Chapter 5:** Configuring OpenShift Networking for Applications

## **5.1.** Troubleshooting OpenShift Software-defined Networking

- OpenShift implements a software-defined network (SDN) to manage the network infrastructure of the cluster and user applications. Software-defined networking is a networking model that allows you to manage network services through the abstraction of several networking layers. It decouples the software that handles the traffic, called the control plane, and the underlying mechanisms that route the traffic, called the data plane. Among the many features of SDN, open standards enable vendors to propose their solutions, centralized management, dynamic routing, and tenant isolation. 

- To learn more about **control plane** and **data plane**, click [here](https://www.geeksforgeeks.org/difference-between-control-plane-and-data-plane/)

- In OpenShift Container Platform, the SDN satisfies the following five requirements:-
  - Managing the network traffic and network resources programmatically, so that the organization teams can decide how to expose their applications.

  - Managing communication between containers that run in the same project.

  -  Managing communication between pods, whether they belong to a same project or run in separate projects.

  -  Managing network communication from a pod to a service.

  -  Managing network communication from an external network to a service, or from containers to external networks. 


> ###########################################
> ###########################################

# **Chapter 7:** Describing Cluster Updates

## **7.1.** Introducing Cluster Updates

- Red Hat OpenShift Container Platform 4 adds many new features by using Red Hat Enterprise Linux CoreOS. Red Hat released a new software distribution system that provides the best upgrade path to update your cluster and the underlying operating system. This new distribution system is one of the significant **benefits of OpenShift 4 architectural changes, enabling clusters to upgrade Over-the-Air (OTA).**

- This software distribution system for OTA manages the controller manifests, cluster roles, and any other resources necessary to update a cluster to a particular version. This feature ensures that a cluster runs the latest available version seamlessly. OTA also enables a cluster to use new features as they become available, including the latest bug fixes and security patches. OTA substantially decreases downtime due to upgrades. Red Hat hosts and manages this service at https://cloud.redhat.com and hosts cluster images at https://quay.io.

- OTA enables faster updates by allowing the skipping of intermediary versions. For example, you can update from 4.5.1 to 4.5.3, thus bypassing 4.5.2.

- You use a single interface (https://cloud.redhat.com) to manage the life cycle of all your OpenShift clusters The service defines upgrade paths that correspond to cluster eligibility for certain updates.

- Update paths belong to upgrade channels. A channel can be visualized as a representation of the upgrade path. The channel controls the frequency and stability of updates. The OTA policy engine represents channels as a series of pointers to particular versions within the upgrade path.

- A channel name consists of three parts: the tier (release candidate, fast, and stable), the major version (4), and the minor version (.2). Example channel names include: stable-4.5, fast-4.5, and candidate-4.5. Each channel delivers patches for a given cluster version.

- **Candidate Channel:** The candidate channel delivers updates for testing the feature acceptance for the next version of OpenShift Container Platform. The features are subject to further checks and are promoted to the fast or stable channels when they meet the quality standards.

  You use this channel to have access to the latest features of the product as they get released. This channel is suited for development and pre-production environments. 

- **Fast Channel:** The fast channel delivers updates as soon as they are available. This channel is best suited for QA environments. This channel is supported by Red Hat and can be applied to production environments.

- **Stable Channel:**  The stable channel contains delayed updates, which means that it delivers only minor updates for a given cluster version. This channel is suited for production environments, as the releases in that channel are tested by Red Hat SREs and support services.

  Red Hat support and site reliability engineering (SRE) teams monitor operational clusters with new fast updates. If operational clusters pass additional testing and validation, updates in the fast channel are enabled in the stable channel. If Red Hat observes operational issues from a fast channel update, then that update is skipped in the stable channel.

- **NOTES:**  The stable and fast channels are classified as General Availability (GA), whereas the candidate channel (release candidate channel) is not supported by Red Hat.

  To ensure the stability of the cluster and the proper level of support, you should only switch from a stable channel to a fast channel, and vice versa. Although it is possible to switch from a stable channel or fast channel to a candidate channel, it is not recommended. The candidate channel is best suited for testing feature acceptance and assisting in qualifying the next version of OpenShift Container Platform.

- **EXAMPLE:** The following describes how these upgrade paths would apply to Red Hat OpenShift Container Platform version 4.5:-

  - When using the stable-4.5 channel, you can upgrade your cluster from 4.5.0 to 4.5.1 or 4.5.2. If an issue is discovered in the 4.5.3 release, then you cannot upgrade to that version. When a patch becomes available in the 4.5.4 release, you can update your cluster to that version. T

  - The fast-4.5 channel can deliver 4.5.1 and 4.5.2 updates but not 4.6.1. Administrators must specifically choose a different minor version channel, such as fast-4.6, in order to upgrade to a new release in a new minor version.

  - The candidate-4.5 channel allows you to install the latest features of OpenShift. With this channel, you can upgrade to all z-stream releases, such as 4.5.1, 4.5.2, 4.5.3, and so on. You use this channel to have access to the latest features of the product as they get released.

- **Changing the Update Channel:** You can change the update channel to stable-4.5, fast-4.5, or candidate-4.5 using the web console or the OpenShift CLI client.

- **Describing OTA:** OTA follows a client-server approach. Red Hat hosts the cluster images and the update infrastructure. One feature of OTA is the generation of all possible update paths for your cluster. OTA gathers information about the cluster and your entitlement to determine the available upgrade paths. The web console sends a notification when a new update is available.

- Red Hat hosts both the cluster images and a "watcher", which automatically detects new images that are pushed to Quay. The Cluster Version Operator (CVO) receives its update status from that watcher. The CVO starts by updating the cluster components via their operators, and then updates any extra components that the Operator Lifecycle Manager (OLM) manages.

- Telemetry allows Red Hat to determine the update path(upgrade channels). The cluster uses Prometheus-based telemetry to report on the state of each cluster operator. The data is anonymized and sent back to Red Hat servers that advise cluster administrators about potential new releases.

- You can update the cluster via the web console, or from the command-line. Updating via the web console is easier than using the command-line. The **Administration → Cluster** Settings page displays an Update Status of Update available when a new update is available. From this page, click **Update now** to begin the process.
  
- **Points To Remember**
  - Be sure to update all operators installed through the Operator Lifecycle Manager (OLM) to the latest version before updating the OpenShift cluster.

  - The CVO starts by updating the cluster components via their operators, and then updates any extra components that the Operator Lifecycle Manager (OLM) manages.

  - The CVO orchestrates updating the cluster and The OLM orchestrates updates to any operators running in the cluster.
  
  - Red Hat does not support reverting your cluster to a previous version, or rollback. Red Hat only supports upgrading to a newer version

  - If an upgrade fails, the operator stops and reports the status of the failing component. Rolling your cluster back to a previous version is not supported. If your upgrade fails, contact Red Hat support.

## **7.3.** Summary

- One of the major benefits of OpenShift 4 architectural changes is that you can update your clusters Over-the-Air (OTA).

- Red Hat provides a new software distribution system that ensures the best path for updating your cluster and the underlying operating system.

- There are three distribution channels:-
  - The stable channel delivers delayed updates.
  - The fast channel delivers updates are soon as they are available.
  - The candidate channel delivers updates for testing feature acceptance in the next version of OpenShift Container Platform. 

- Red Hat does not support reverting your cluster to a previous version. Red Hat only supports upgrading to a newer version. 
