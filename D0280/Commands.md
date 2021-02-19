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