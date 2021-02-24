# Persistent Volume and Persistent Volume Claim

1. **oc set volumes:** To add a volume to an application
    ```
    oc set volumes deployment/example-application \
        --add \
        --name example-storage \
        --type pvc \
        --claim-class nfs-storage \
        --claim-mode rwo \
        --claim-size 15Gi \
        --mount-path /var/lib/example-app \
        --claim-name example-storage
    ```

    The command creates a persistent volume claim resource and adds it to the application as a volume within the pod.

2. **oc delete:** To delete the persistent volume claim. The storage class will reclaim the volume after the PVC is removed
    ```
    oc delete pvc/example-pvc-storage
    ```

3. **oc get storageclass:** To view available storage classes


# Assigning Administrative Privileges

The cluster-wide cluster-admin role grants cluster administration privileges to users and groups. This role enables the user to perform any action on any resources within the cluster. The following example assigns the cluster-admin role to the student user. 

  ```bash
  [user@demo ~]$ oc adm policy add-cluster-role-to-user cluster-admin student
  ```

# Extract file-data from secret

Extract the file data from the secret to the ~/DO280/labs/auth-provider/htpasswd file.

```bash
oc extract secret/localusers -n openshift-config \
    --to ~/DO280/labs/auth-provider/ --confirm
```

# Managing RBAC Using the CLI

Cluster administrators can use the oc adm policy command to both add and remove cluster roles and namespace roles.

To add a cluster role to a user, use the add-cluster-role-to-user subcommand:

```bash
[user@demo ~]$ oc adm policy add-cluster-role-to-user cluster-role username
```

For example, to change a regular user to a cluster administrator, use the following command:

```bash
[user@demo ~]$ oc adm policy add-cluster-role-to-user cluster-admin username

```

To remove a cluster role from a user, use the remove-cluster-role-from-user subcommand:

```bash
[user@demo ~]$ oc adm policy remove-cluster-role-from-user cluster-role username
```

For example, to change a cluster administrator to a regular user, use the following command:

```bash
[user@demo ~]$ oc adm policy remove-cluster-role-from-user cluster-admin username
```

Rules are defined by an action and a resource. For example, the create user rule is part of the cluster-admin role. You can use the oc adm policy who-can command to determine if a user can execute an action on a resource. For example:

```bash
[user@demo ~]$ oc adm policy who-can delete user
```

Project administrators can use the oc policy command to add and remove namespace roles.

Add a specified role to a user with the add-role-to-user subcommand. For example:

```bash
[user@demo ~]$ oc policy add-role-to-user role-name username -n project
```

For example, to add the user dev to the role basic-user in the wordpress project:

```bash
[user@demo ~]$ oc policy add-role-to-user basic-user dev -n wordpress
```


# Creating a secret

1. Create a generic secret containing key-value pairs from literal values typed on the command line:

    ```bash
    oc create secret generic secret_name \
             --from-literal key1=secret1 \
             --from-literal key2=secret2
    ```

2. Create a generic secret using key names specified on the command line and values from files:

    ```bash
    oc create secret generic ssh-keys \
              --from-file id_rsa=/path-to/id_rsa \
              --from-file id_rsa.pub=/path-to/id_rsa.pub
    ```

3. Create a TLS secret specifying a certificate and the associated key:

    ```bash
    oc create secret tls secret-tls \
              --cert /path-to-certificate \
              --key /path-to-key
    ```

# Creating a ConfigMap

1. The syntax for creating a configuration map closely matches the syntax for creating a secret. Key-value pairs can be entered on the command line or the content of a file can be used as the value of a specified key:

    ```bash
    oc create configmap my-config \
              --from-literal key1=config1 \
              --from-literal key2=config2
    ```
