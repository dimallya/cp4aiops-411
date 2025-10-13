# Observers #

## Configuring Kubernetes Observer jobs ##

Doc Ref: https://www.ibm.com/docs/en/cloud-paks/cloud-pak-aiops/4.10.1?topic=jobs-kubernetes-observer 

### Prerequisites ###

**1. Create cluster role access**

For clusterole access, create a configuration file called `asm-k8s-observer.yaml` with the custom cluster role asm:kubernetes-observer, in the target Kubernetes/OpenShift environment where applications are deployed. 


```
kind: ClusterRole
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  annotations:
    rbac.authorization.kubernetes.io/autoupdate: "true"
  name: asm:kubernetes-observer
rules:
- apiGroups: [""]
  resources: [ "pods", "namespaces", "nodes", "services", "endpoints", "persistentvolumes", "persistentvolumeclaims"]
  verbs: ["get", "list", "watch"]
- apiGroups: ["apps"]
  resources: ["replicasets", "deployments", "statefulsets", "daemonsets"]
  verbs: ["get", "list", "watch"]
```
Run the following commannd to create clusterrole access
```
oc create -f asm-k8s-observer.yaml
```

**2. Create the service account in the target environment**

Execute the following command by <namespace> with the name of your namespace. Ex: cp4aiops
```
oc create serviceaccount asm-k8s-account -n <namespace>
```
To verify that the service account exists, run the following command
```
oc get serviceaccount
```
**3. Bind the asm:kubernetes-observer ClusterRole to the asm-k8s-account service account**

Execute following command by replacing {namespace} with the value of namespace 
```
oc create clusterrolebinding asm-k8s --clusterrole=asm:kubernetes-observer --serviceaccount={namespace}:asm-k8s-account
```
Important: The service account and the cluster role binding need to be created in the same namespace.

**4. Obtain the Kubernetes service account token**
```oc create token asm-k8s-account```

Where 'asm-k8s-account' is a service account. This is the only step required for Kubernetes on OpenShift Version 4.16 (and later).

**5. Ensure kubeconfig.yml file is in the correct format for load job**
Follow the instructions in this section: https://www.ibm.com/docs/en/cloud-paks/cloud-pak-aiops/4.10.1?topic=jobs-kubernetes-observer#kubernetes-observer-kubeconfig-load-job-prerequisites



### Procedure ###

**1. Accessing the Observer Configuration UI**

Expand **Define**, click **Integrations**, and then click the **Manage observer jobs** tab.

Click **Configure, schedule, and manage observer jobs**. The Observer jobs page is displayed.

Here, you can add a new job, or view, search for, or sort existing jobs by job name, observer name, job status or job type.  

**2. Create Load job with required parameters**

Provide required [parameters](https://www.ibm.com/docs/en/cloud-paks/cloud-pak-aiops/4.10.1?topic=jobs-kubernetes-observer#load-job-parameters) for Load job and click on **Run job**



## Defining Application ##

1. For creation of various Resource/Topology Group Templates follow the steps provided in [Lab](https://ibm.github.io/waiops-tech-jam/labs/cloud-pak-aiops/topology-lab/topology-templates/)

2. For creation application topology from resource groups follow the steps provided in [Lab](https://ibm.github.io/waiops-tech-jam/labs/cloud-pak-aiops/topology-lab/topology-applications/)


