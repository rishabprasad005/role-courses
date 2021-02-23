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

- Red Hat, in collaboration with AWS, Google Cloud, and Microsoft, launched the **OperatorHub**, accessible at <https://operatorhub.io>. The platform is a public repository and marketplace for operators compatible with OpenShift and other distributions of Kubernetes that include the OLM.

    **Red Hat Marketplace** is a platform that allows access to certified software packaged as Kubernetes operators that can be deployed in an OpenShift cluster. The certified software includes automatic deployments and seamless upgrades for an integrated experience.

## **1.3.** Describing the Architecture of OpenShift

- The architecture of OpenShift is based on the declarative nature of Kubernetes. Declarative architectures allow for self-optimizing and self-healing systems that are easier to manage than imperative architectures.

- A Kubernetes cluster consists of a set of nodes that run the kubelet system service and a container engine. OpenShift runs exclusively the CRI-O container engine.

    Some nodes in the cluster are **control plane nodes** that run the REST API, the etcd database, and the platform controllers. OpenShift configures its control plane nodes so that they are not schedulable to run end-user application pods and are dedicated to running the control plane services. OpenShift schedules end-user application pods to be executed on the worker nodes.

- Unlike many container platforms that focus on cloud-native, stateless applications, OpenShift also supports stateful applications that do not follow the standard **Twelve-Factor App** methodology.

    OpenShift supports **stateful applications** by offering a comprehensive set of storage capabilities and supporting operators. OpenShift ships with integrated storage plug-ins and storage classes that rely on the underlying cloud or virtualization platform to provide dynamically provisioned storage.

    For example, if you install OpenShift on Amazon Web Services (AWS), your OpenShift cluster comes pre-configured with a default storage class that uses AWS EBS service automatically to provision storage volumes on-demand. Users can deploy an application that requires persistent storage, such as a database, and OpenShift automatically creates an EBS volume to host the application data.

    OpenShift cluster administrators can later define additional storage classes that use different EBS service tiers. For example, you could have one storage class for high-performance storage that sustains a high input-output operations per second (IOPS) rate, and another storage class for low-performance, low-cost storage. Cluster administrators can then allow only certain applications to use the high-performance storage class, and configure data archiving applications to use the low-performance storage class.

## **1.5.** Describing Cluster Operators

- Kubernetes operators are applications that invoke the Kubernetes API directly to manage Kubernetes resources. operators, unlike common applications, require direct access to the Kubernetes resources, they usually require custom security settings.

    Operators usually define custom resources (CR) that store their settings and configurations. An OpenShift administrator manages an operator by editing its custom resources. The syntax of a custom resource is defined by a custom resource definition (CRD).

    The purpose of an operator is to automate tasks that a human administrator (or human operator) would perform to deploy, update, and manage an application.

- You can develop operators using your preferred programming language. Technically you do not need a special-purpose SDK to develop an operator. All you need is the ability to invoke REST APIs and consume secrets that contain access credentials to the Kubernetes APIs.

- The Operator Framework is an open source toolkit for building, testing, and packaging operators. The Operator Framework makes these tasks easier than coding directly to low-level Kubernetes APIs by providing the following components:-

  - **Operator Software Development Kit (Operator SDK):** Provides a set of Golang libraries and source code examples that implement common patterns in operator applications. It also provides a container image and playbook examples that allow you to develop operators using Ansible. 
  - **Operator Life Cycle Manager (OLM):** Provides an application that manages the deployment, resource utilization, updates, and deletion of operators that have been deployed through an operator catalog. The OLM itself is an operator that comes preinstalled with OpenShift. Hence, OLM can be said as "_An operator for the operators_".

    The Operator Framework also defines a set of recommended practices for implementing operators and CRDs and a standard way of packaging an operator manifest as a container image, that allows an operator to be distributed using an operator catalog. The most common form of an operator catalog is an image registry server.

    An operator container image that follows the Operator Framework standards contains all resource definitions required to deploy the operator application. This way the OLM can install an operator automatically. If an operator is not built and packaged by following the Operator Framework standards, the OLM will not be able to install nor manage that operator.
- **Introducing OperatorHub:** OperatorHub provides a web interface to discover and publish operators that follow the Operator Framework standards. Both open source operators and commercial operators can be published to the Operator hub. Operator container images can be hosted at different image registries, for example quay.io.

- **Red Hat Marketplace** is a platform that allows access to a curated set of certified softwares packaged as Kubernetes operators that can be deployed on an OpenShift or a Kubernetes cluster. The certified software includes automatic deployments and seamless upgrades for an integrated experience Operators available in the Red Hat Marketplace have gone through a certification process to ensure the software follows best practices and also the containers are scanned for vulnerabilities.

- **Cluster operators** are regular operators except that they are not managed by the OLM. They are managed by the OpenShift Cluster Version Operator. OpenShift cluster operators provide OpenShift extension APIs and infrastructure services such as:-

  - The OAuth server, which authenticates access to the control plane and extensions APIs.
  - The core DNS server, which manages service discovery inside the cluster.
  - The web console, which allows graphical management of the cluster.
  - The internal image registry, which allow developers to host container images inside the cluster, using either S2I or another mechanism.
  - The monitoring stack, which generates metrics and alerts about the cluster health.

  **Note:**  OpenShift Cluster Version Operator are sometimes called a first-level operator and all cluster operators are also called second-level operators.

- Extra Notes:-
  - Operators are a method of packaging, deploying, and managing an OpenShift Container Platform application. They act like an extension of the software vendor’s engineering team, watching over an OpenShift Container Platform environment and using its current state to make decisions in real time. Operators are designed to handle upgrades seamlessly, react to failures automatically, and not take shortcuts, such as skipping a software backup process to save time.

  - OpenShift Container Platform 4.5 includes a default set of Operators that are required for proper functioning of the cluster. These default Operators are managed by the Cluster Version Operator (CVO).

  - As a cluster administrator, you can install application Operators from the OperatorHub using the OpenShift Container Platform web console or the CLI. You can then subscribe the Operator to one or more namespaces to make it available for developers on your cluster. Application Operators are managed by Operator Lifecycle Manager (OLM).

  - Default OpenShift Container Platform cluster Operators are managed by the Cluster Version Operator (CVO) and they do not have a Subscription object. Application Operators are managed by Operator Lifecycle Manager (OLM) and they have a Subscription object.

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