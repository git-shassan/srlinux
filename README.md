# srlinux
The repo provides the kustomization files that can be used to run Nokia's SR-Linux router on a Kubernetes cluster

reference: https://learn.srlinux.dev/get-started/#__tabbed_1_1

### To run:

Set the desired namespace value in kustomization.yaml 

[mano@bastion srlinux]$ oc apply -k ./
namespace/sr-namespace created
serviceaccount/sr-sa created
clusterrolebinding.rbac.authorization.k8s.io/system:openshift:scc:privileged configured
configmap/syed-sr-router-config created
service/srlinux created
Warning: would violate PodSecurity "restricted:latest": privileged (container "srlinux" must not set securityContext.privileged=true), allowPrivilegeEscalation != false (container "srlinux" must set securityContext.allowPrivilegeEscalation=false), unrestricted capabilities (container "srlinux" must set securityContext.capabilities.drop=["ALL"]), runAsNonRoot != true (pod or container "srlinux" must set securityContext.runAsNonRoot=true), seccompProfile (pod or container "srlinux" must set securityContext.seccompProfile.type to "RuntimeDefault" or "Localhost")
deployment.apps/srlinux created
[mano@bastion srlinux]$ 


### Once its running:

[mano@bastion srlinux]$ oc project sr-namespace
Now using project "sr-namespace" on server "https://api.mano-npss.jnpr.bos2.lab:6443".
[mano@bastion srlinux]$ oc get deployment
NAME      READY   UP-TO-DATE   AVAILABLE   AGE
srlinux   1/1     1            1           48s
[mano@bastion srlinux]$ oc get pods
NAME                       READY   STATUS    RESTARTS   AGE
srlinux-5f5b77dfdb-jmwvf   1/1     Running   0          50s
[mano@bastion srlinux]$ oc exec -it srlinux-5f5b77dfdb-jmwvf -- /bin/bash/sr_cli
ERRO[0000] exec failed: unable to start container process: exec: "/bin/bash/sr_cli": stat /bin/bash/sr_cli: not a directory 
command terminated with exit code 255
[mano@bastion srlinux]$ oc exec -it srlinux-5f5b77dfdb-jmwvf -- /bin/bash
[linuxadmin@srlinux-5f5b77dfdb-jmwvf /]$ sr_cli
Using configuration file(s): ['/etc/opt/srlinux/srlinux.rc']
Welcome to the srlinux CLI.
Type 'help' (and press <ENTER>) if you need any help using this.
--{ [FACTORY] + running }--[  ]--
A:srlinux-5f5b77dfdb-jmwvf#  
[FACTORY] Current mode: + running    
