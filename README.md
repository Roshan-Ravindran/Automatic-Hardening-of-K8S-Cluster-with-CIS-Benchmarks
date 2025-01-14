## Securenetes

## Table of Contents

- [ABSTRACT](#1-abstract)
- [INTRODUCTION](#2-introduction)
- [CIS KUBERNETES BENCHMARKS](#3-cis-kubernetes-benchmarks)
- [NEED FOR KUBERNETES SECURITY](#4-need-for-kubernetes-security)
- [KUBERNETES COMPONENTS](#5-kubernetes-components)
  - [Master Node](#51-master-node)
  - [Worker Node](#52-worker-node)
  - [Pod](#53-pod)
  - [Service](#54-service)
  - [Volume](#55-volume)
- [PROPOSED SOLUTION](#7-proposed-solution)
  - [Overview](#71-overview)
  - [Details](#72-details)
  - [Analysis](#73-analysis)
  - [Limitations](#74-limitations)
- [ARCHITECTURE](#8-architecture)
- [ENVIRONMENT SETUP](#9-environment-setup)
- [REMEDIATED CONTROLS](#10-remediated-controls)
- [OUTPUT](#11-output)
- [CONCLUSION](#12-conclusion)
- [FUTURE SCOPE](#13-future-scope)

## 1. ABSTRACT

Automatic hardening of a Kubernetes environment with CIS benchmarks is a crucial aspect of securing
containerized applications in today's complex IT landscape. CIS (Center for Internet Security)
benchmarks provide industry-standard guidelines for the secure configuration of various technologies,
including Kubernetes. By leveraging automation tools and scripts, organizations can automatically
apply these benchmarks to their Kubernetes clusters, ensuring that the environment adheres to
recommended security practices. This process involves scanning the cluster's components, such as the
master nodes, worker nodes, and network configurations, against the CIS benchmarks, and identifying
any deviations or vulnerabilities. Automated remediation techniques can then be employed to address
these issues by adjusting the configuration settings to align with the recommended security controls.
This approach offers several advantages, including reducing the risk of misconfigurations, ensuring
consistent security across the cluster, and streamlining the hardening process at scale. Furthermore,
automatic hardening with CIS benchmarks helps organizations stay compliant with security regulations
and best practices, mitigating potential security breaches and protecting sensitive data within the
Kubernetes environment. By embracing this automated approach, organizations can proactively
strengthen the security posture of their Kubernetes deployments and enhance the overall resilience of
their containerized applications.

## 2. INTRODUCTION

In the rapidly evolving landscape of cloud computing, Kubernetes has emerged as the de facto
orchestration platform for managing containerized applications. However, with its widespread
adoption, Kubernetes clusters have become a prime target for security threats. The complexity and
dynamic nature of Kubernetes environments make manual security hardening a daunting and fallible
task. With the development of an advanced tool that automates the correction of security vulnerabilities
in Kubernetes clusters, this project aims to address these issues head-on. The application will
automatically apply the required patches to bring the cluster into compliance with best practices after
scanning it for deviations from the CIS benchmarks. In addition to saving a great deal of time and
money, this proactive strategy lowers the likelihood that human error may result in security breaches.
The goal of this project is to automate the hardening process to provide a solution that makes managing
Kubernetes security easier, guarantees uniform application of security standards, and strengthens
clusters against the constant threat of cyberattacks.

## 3. CIS KUBERNETES BENCHMARKS

The CIS Kubernetes benchmarks, developed by the Center for Internet Security (CIS), are a
comprehensive resource for securing your Kubernetes environments. They go beyond basic security
measures and aim to harden your clusters against a wide range of threats.

Here's a deeper dive into what they offer:

- Security Best Practices: The benchmarks act as a guide, outlining recommended
  configurations for various elements of your Kubernetes setup. This includes control plane
  components, worker nodes, etcd (distributed key-value store), and network policies.
- Reduced Risk: By following the CIS recommendations, you can significantly reduce the attack
  surface of your Kubernetes clusters. This lowers the risk of vulnerabilities and
  misconfigurations that could be exploited by malicious actors.

- Multiple Levels: The benchmarks come in two levels, Level 1 (L1) and Level 2 (L2). L
  focuses on essential security requirements that are widely applicable and have minimal impact
  on functionality. L2 builds on L1 with more advanced security controls, offering a stronger
  security posture but potentially requiring more configuration effort.
- Version Specific: The CIS benchmarks are tailored to specific Kubernetes versions. This
  ensures the recommendations consider the security landscape and potential vulnerabilities
  relevant to that version.
- Wide Applicability: While designed for the open-source Kubernetes distribution, the CIS
  benchmarks are intended to be broadly applicable across various Kubernetes distributions
  offered by cloud providers or vendors like Google Kubernetes Engine (GKE) or Amazon
  Elastic Kubernetes Service (EKS).

Following the CIS Kubernetes benchmarks can significantly improve the security posture of your
Kubernetes deployments. They provide a structured approach to securing your clusters and reducing
the risk of attacks.

## 4. NEED FOR KUBERNETES SECURITY

As organizations adopt Kubernetes for container orchestration, ensuring robust security measures
becomes imperative. The need for Kubernetes security arises from several factors, including:

- Complexity: Kubernetes is a sophisticated and dynamic orchestration platform with multiple
  components and configurations. This complexity introduces potential security vulnerabilities
  and requires comprehensive security measures.
- Containerized Environments: Kubernetes operates in a containerized environment, where
  multiple containers run on shared resources. Ensuring the isolation and security of these
  containers is critical to prevent unauthorized access and data breaches.
- Network Security: Kubernetes clusters require secure network configurations to protect
  against unauthorized network access, data interception, and malicious activities.
- Access Control: Proper authentication and authorization mechanisms are necessary to control
  access to Kubernetes resources and prevent unauthorized actions or privilege escalation.
- Configuration Management: Correctly configuring Kubernetes components and resources
  are essential to prevent misconfigurations that can lead to security gaps and vulnerabilities.

By implementing CIS Benchmarks, organizations can address these security challenges and establish a
strong security foundation for their Kubernetes clusters. Compliance with the benchmarks helps
mitigate risks, reduce vulnerabilities, and align deployments with industry-recognized best practices.

## 5. KUBERNETES COMPONENTS

### 5.1 Master Node

The master node serves as the control plane for the Kubernetes cluster. It consists of several key
components. The API Server acts as the central communication hub, receiving and processing requests
from users, administrators, and other components. etcd is a distributed key-value store that maintains
the cluster's configuration data and the desired state of the system. The Controller Manager manages

various controllers responsible for maintaining the desired state of the cluster, including node
management, replication, and resource allocation. The Scheduler is responsible for assigning pods to
nodes based on resource requirements, policies, and constraints.

### 5.2 Worker Node

The worker node, also known as a minion, is where the actual workloads in the form of containers are
executed. Each worker node runs several components. The Kubelet is an agent that communicates with
the master node, manages the node's resources, and ensures that containers are running as intended.
Container runtime, such as Docker or containerd, is responsible for pulling container images and
running them as containers. The Kube-proxy is a network proxy that enables communication between
services and manages network routing on the node.

### 5.3 Pod

A pod is the smallest deployable unit in Kubernetes. It represents a single instance of a running process
in the cluster. Pods encapsulate one or more containers, shared storage, and network resources. They
are co-located and co-scheduled on the same worker node, enabling them to communicate with each
other through localhost. Pods are considered disposable and can be easily scaled, replaced, or
rescheduled based on the cluster's needs.

### 5.4 Service

Services provide a stable network endpoint to expose a group of pods. They enable load balancing and
service discovery within the cluster. A service abstracts the underlying pods and allows other
components to access them using a consistent DNS name or IP address. By defining a service,
developers can decouple the application logic from the specifics of the underlying pod instances,
making the application more resilient and scalable.

### 5.5 Volume

Volumes enable persistent storage in Kubernetes. They provide a way for containers within pods to
store and access data beyond the lifespan of the containers themselves. Volumes can be attached to pods
and mounted into containers, allowing data to be shared and persisted across restarts or migrations.
Kubernetes supports various types of volumes, including local storage, network-attached storage, and
cloud provider-specific storage options.

## 7. PROPOSED SOLUTION

### 7.1 Overview

This project is about the tool created which is named as Securenetes that audits the Kubernetes Cluster
for CIS Benchmarks. From the audit analysis, the tool will perform remediation on both master and
worker nodes that can be automatically performed.

### 7.2 Details

Initially, kube-bench is iteratively installed on all the nodes. The tool ingests security audit reports
generated by Kube-bench within the cluster. These reports act as a roadmap, highlighting areas where
the cluster configuration falls short of CIS benchmarks security best practices. All remediating functions
were formulated for each control which of those are included in source code. With this information, the
tool takes control and automatically applies the necessary remediation actions on each worker nodes
and master through paramiko client. This may involve adjusting configurations, modifying access
controls, or updating security policies like:

Restrictive file permissions of API Server, Controller Manager, Scheduler pod
specification prevents unauthorized modifications to these services.

- Proper permissions (600) and ownership (root:root) are necessary because these files contain
  files contain authentication information.

Enforcing certificate-based authentication within the cluster.

- Explicitly mapping certificates to each component in the cluster would ensure no
  unauthorized certificates allow spoofed requests.

Minimizing the admission of containers that share unnecessary information.

- Not exposing the host information like process ID, namespace would prevent process
  inspection and privilege escalation.

The tool takes in three arguments namely:

- --include-auto which remediates only the controls that be performed automatically irrespective
  of any configuration or dependencies in any Kubernetes environment.
- --include-all that does automatic remediation and as well as provide remediating steps for
  certain controls that can be only remediated manually. These controls are marked as “Manual”

```
or “Operator Dependent.” because they depend on context, use case, or factors determined by
the cluster operator.
```

- --exempt argument takes input of controls ID’s that needs to be excluded from automatic
  remediation.

### 7.3 Analysis

One of the many benefits of the suggested technology is that it automates the enforcement of CIS
benchmarks. Ensuring uniform compliance across clusters and reducing the likelihood of human
mistake greatly enhances overall security posture. Second, by automating the hardening process, the
tool increases productivity. Compared to manual configuration, this saves a significant amount of time
and resources, allowing IT personnel to concentrate on other important duties. Last but not least, the
tool's scalability allows it to efficiently manage big clusters with hundreds or even thousands of worker
nodes. Because of this, it's a solution that will stand the test of time for businesses operating more
complex containerized systems.

### 7.4 Limitations

The first development phase will give priority to fixing security flaws found in CIS benchmark failures.
This guarantees a solid base for cluster security. Everyone recognize that in order to address a broader
spectrum of security concerns, the tool's scope needs to be expanded in subsequent generations. In a
similar vein, isolated Kubernetes clusters will be used for the initial testing. Although this is a useful
beginning point, additional testing on more intricate Kubernetes systems would be necessary later on
to guarantee full operation.

## 8. ARCHITECTURE

## 9. ENVIRONMENT SETUP

i) Install the pre-requisites:

- Kubectl – to interact with Kubernetes cluster from CLI.
- Kops - simplifies tasks related to cluster creation, configuration, and maintenance.

ii) Make sure to have the private key of nodes in particular directory so the tool can access them
while using paramiko client to SSH.

iii) Configure the CLI to assume the role with permissions to access the nodes if they were hosted
on cloud and assure that the state holder storages are accessible when buckets are used as
etcd storage.

iv) Validate the cluster from CLI to make sure that the cluster is ready and accessible.

## 10. REMEDIATED CONTROLS

Below are the controls that can be remediated automatically on master node and the exact remediated
function is included in the source code.

Benchmark Controls Remediation Commands

1.1.1 Ensure that the API server pod specification
file permissions are set to 600 or more restrictive.

```
sudo chmod 600 /etc/kubernetes/manifests/kube-
apiserver.manifest
```

1.1.2 Ensure that the API server pod specification
file ownership is set to root:root.

```
sudo chown root:root
/etc/kubernetes/manifests/kube-apiserver.manifest
```

1.1.2 Ensure that the API server pod specification
file ownership is set to root:root.

```
sudo chmod 600 /etc/kubernetes/manifests/kube-
controller-manager.manifest
```

1.1.4 Ensure that the controller manager pod
specification file ownership is set to root:root.

```
sudo chown root:root
/etc/kubernetes/manifests/kube-controller-
manager.manifest
```

1.1.5 Ensure that the scheduler pod specification file
permissions are set to 600 or more restrictive.

```
sudo chmod 600 /etc/kubernetes/manifests/kube-
scheduler.manifest
```

1.1.6 Ensure that the scheduler pod specification file
ownership is set to root:root.

```
sudo chown root:root
/etc/kubernetes/manifests/kube-scheduler.manifest
```

1.1.19 Ensure that the Kubernetes PKI directory and
file ownership is set to root:root.

```
sudo chown -R root:root /etc/kubernetes/pki/
```

1.2.2 Ensure that the --token-auth-file parameter is
not set.

```
Remove --token-auth-file=<filename> from
/etc/kubernetes/manifests/kube-apiserver.manifest
```

1.2.4 Ensure that the --kubelet-https argument is set
to true.

```
Add --kubelet-https=true in in
/etc/kubernetes/manifests/kube-apiserver.manifest
```

1.2.5 Ensure that the --kubelet-client-certificate and
--kubelet-client-key arguments are set as
appropriate.

```
Add kubelet-client-
certificate=/srv/kubernetes/kube-apiserver/kubelet-
api.crt && kubelet-client-
key=/srv/kubernetes/kube-apiserver/kubelet-
api.key
```

1.2.6 Ensure that the --kubelet-certificate-authority
argument is set as appropriate.

```
Add --kubelet-certificate-
authority=/srv/kubernetes/ca.crt
```

1.2.7 Ensure that the --authorization-mode
argument is not set to AlwaysAllow.

```
Ensure --authorization-mode=AlwaysAllow is not
present instead it can have values like Node,RBAC
```

1.2.8 Ensure that the --authorization-mode
argument includes Node.

```
Ensure --authorization-mode=Node is present
```

1.2.9 Ensure that the --authorization-mode
argument includes RBAC.

```
Ensure --authorization-mode=RBAC is present
```

1.2.11 Ensure that the admission control plugin
AlwaysAdmit is not set.

```
Remove --enable-admission-plugins parameter or
set value that does not include AlwaysAdmit
```

1.2.14 Ensure that the admission control plugin
ServiceAccount is set.

```
Ensure --disable-admission-plugins=ServiceAccount
is not present
```

1.2.15 Ensure that the admission control plugin
NamespaceLifecycle is set.

```
Ensure --disable-admission-
plugins=NamespaceLifecycle is not present
```

1.2.16 Ensure that the admission control plugin
NodeRestriction is set.

```
Ensure --enable-admission-plugins=NodeRestriction
is present
```

1.2.17 Ensure that the --secure-port argument is not
set to 0.

```
Ensure --secure-port is non-zero
```

1.2.18 Ensure that the --profiling argument is set to
false.

```
Ensure --profiling=false
```

1.2.19 Ensure that the --audit-log-path argument is
set.

```
Add --audit-log-path=/var/log/apiserver/audit.log
```

1.2.20 Ensure that the --audit-log-maxage argument
is set to 30 or as appropriate.

```
Add --audit-log-maxage=
```

1.2.21 Ensure that the --audit-log-maxbackup
argument is set to 10 or as appropriate.

```
Add --audit-log-maxbackup=
```

1.2.22 Ensure that the --audit-log-maxsize argument
is set to 100 or as appropriate.

```
Add --audit-log-maxsize=
```

1.2.24 Ensure that the --service-account-lookup
argument is set to true.

```
Add --service-account-lookup=true
```

1.2.25 Ensure that the --service-account-key-file
argument is set as appropriate.

```
Add --service-account-key-
file=/srv/kubernetes/kube-apiserver/service-
account.pub
1.2.26 Ensure that the --etcd-certfile and --etcd-
keyfile arguments are set as appropriate.

Add --etcd-certfile=/srv/kubernetes/kube-
apiserver/etcd-client.crt && --etcd-
keyfile=/srv/kubernetes/kube-apiserver/etcd-
client.key
1.2.27 Ensure that the --tls-cert-file and --tls-private-
key-file arguments are set as appropriate.

Add --tls-cert-file=/srv/kubernetes/kube-
apiserver/server.crt && --tls-private-key-
file=/srv/kubernetes/kube-apiserver/server.key
1.2.28 Ensure that the --client-ca-file argument is set
as appropriate.


Add --client-ca-file=/srv/kubernetes/ca.crt
```

1.2.29 Ensure that the --etcd-cafile argument is set
as appropriate.

```
Add --etcd-cafile=/srv/kubernetes/kube-
apiserver/etcd-ca.crt
```

1.3.2 Ensure that the --profiling argument is set to
false.

```
Set --profiling=false in
/etc/kubernetes/manifests/kube-controller-
manager.manifest
```

1.3.3 Ensure that the --use-service-account-
credentials argument is set to true.

```
Set --use-service-account-credentials=true in
/etc/kubernetes/manifests/kube-controller-
manager.manifest
```

1.3.4 Ensure that the --service-account-private-key-
file argument is set as appropriate.

```
Set --service-account-private-key-
file=/srv/kubernetes/kube-controller-
manager/service-account.key in
/etc/kubernetes/manifests/kube-controller-
manager.manifest
```

1.3.5 Ensure that the --root-ca-file argument is set
as appropriate.

```
Set --root-ca-file=/srv/kubernetes/ca.crt in
/etc/kubernetes/manifests/kube-controller-
manager.manifest
```

1.3.6 Ensure that the RotateKubeletServerCertificate
argument is set to true.

```
Set --feature-
gates=RotateKubeletServerCertificate=true in
/etc/kubernetes/manifests/kube-controller-
manager.manifest
```

1.3.7 Ensure that the --bind-address argument is set
to 127.0.0.1.

```
Set --bind-address=127.0.0.1 in
/etc/kubernetes/manifests/kube-controller-
manager.manifest
```

1.4.1 Ensure that the --profiling argument is set to
false.

```
Set --profiling=false in
/etc/kubernetes/manifests/kube-scheduler.manifest
```

1.4.2 Ensure that the --bind-address argument is set
to 127.0.0.1.

```
Set --bind-address=127.0.0.1 in
/etc/kubernetes/manifests/kube-scheduler.manifest
```

Below are the controls that can be remediated automatically on worker nodes and the exact remediated
function is included in the source code.

Benchmark Controls Remediation Commands

4.1.1 Ensure that the kubelet service file permissions
are set to 600 or more restrictive.

```
sudo chmod 600
/lib/systemd/system/kubelet.service
```

4.1.2 Ensure that the kubelet service file ownership
is set to root:root.

```
sudo chown root:root
/lib/systemd/system/kubelet.service
```

4.1.5 Ensure that the --kubeconfig kubelet.conf
file permissions are set to 600 or more restrictive.

```
sudo chmod 600 /var/lib/kubelet/kubelet.conf
```

4.1.6 Ensure that the --kubeconfig kubelet.conf
file ownership is set to root:root.

```
sudo chown root:root
/var/lib/kubelet/kubelet.conf
```

4.1.9 If the kubelet config.yaml configuration file is
being used validate permissions set to 600 or more
restrictive.

```
sudo chmod 600 /var/lib/kubelet/kubeconfig
```

4.1.10 If the kubelet config.yaml configuration file is
being used validate file ownership is set to root:root.

```
sudo chown root:root /var/lib/kubelet/kubeconfig
```

4.2.1 Ensure that the --anonymous-auth argument is
set to false.

```
Add --anonymous-auth=false in
/lib/systemd/system/kubelet.service
```

4.2.2 Ensure that the --authorization-mode
argument is not set to Always Allow.

```
Add --authorization-mode=Webhook in
/lib/systemd/system/kubelet.service
```

4.2.3 Ensure that the --client-ca-file argument is set
as appropriate.

```
Add --client-ca-file=/srv/kubernetes/ca.crt in
/lib/systemd/system/kubelet.service
```

4.2.6 Ensure that the --protect-kernel-defaults
argument is set to true.

```
Add --protect-kernel-defaults=true in
/lib/systemd/system/kubelet.service
```

4.2.7 Ensure that the --make-iptables-util-chains
argument is set to true.

```
Add --make-iptables-util-chains=true in
/lib/systemd/system/kubelet.service
```

4.2.11 Ensure that the --rotate-certificates argument
is not set to false.

```
Remove --rotate-certificates=false in
/lib/systemd/system/kubelet.service
```

For the other controls, those can be remediated only manually because not all infrastructure would need
those controls to be implemented. Manual controls involve assessing security posture based on factors
beyond readily available configuration data and involve security policy decisions best left to human
judgment.

## 11. OUTPUT

Username and location of private key to access the node are given as the input:

Failed Benchmarks for Worker Node:

Example of Control 4.2.7 before remediation:

The CIS Kubernetes Benchmark recommendation 4.2.7 focuses on the --make-iptables-util-chains
argument for the Kubelet configuration. To comply with this benchmark, ensure that the
makeIPTablesUtilChains field is set to true in the Kubelet configuration file. This setting directs
Kubelet to create and manage iptables utility chains, which are necessary for network traffic
management and security within a Kubernetes cluster.

Output of /lib/system/system/kubelet.service file

After remediation:

Output of /lib/system/system/kubelet.service file

Now, --make-iptables-util-chains argument is set to true in kubelet service file.

Failed Benchmarks for Master Node:

Example of Control 1.2.19 before remediation:

The CIS Kubernetes Benchmark recommendation to “ensure that the audit log path argument is set”
refers to a security measure for Kubernetes clusters. Specifically, it involves setting the --audit-log-path
argument in the API server pod specification file, typically found at /etc/kubernetes/manifests/kube-
apiserver.yaml on the Control Plane node.

Output of API Server Pod Specification File:

After Remediation:

Output of API Server Pod Specification File:

Now, the argument audit log path is set to a particular location where the audit logs of API Server are
stored.

## 12. CONCLUSION

By integrating the straightforward and adaptable solution within their Kubernetes environments,
organizations can effectively fortify their clusters by implementing the recommended controls from the
CIS Kubernetes Benchmarks. This solution automates the remediation process for non-compliant
configurations across the entire infrastructure, guided by predefined rules. Such an automated strategy
markedly improves the organization’s overall security compliance rating and bolsters its defenses
against cyber threats.

Additionally, the solution offers flexibility by allowing customization of remediation actions. This
ensures organizations can adapt to specific needs and accommodate future changes to the CIS
Benchmarks. This adaptability helps organizations stay up-to-date with evolving security requirements
and maintain a robust Kubernetes security posture.

With this solution, organizations can confidently administer their Kubernetes clusters, elevate security
compliance, and mitigate potential risks posed by cyber threats, thereby ensuring a secure and resilient
operation within their cloud-native ecosystems.

#### Contributions Welcome

- Manual Controls: Develop a mechanism to handle security controls that cannot be
  automatically remediated. Implement a risk assessment module that categorizes controls based
  on their impact and complexity, allowing for manual intervention when necessary.
- Adaptable Solution: Design a more adaptable solution that can perform remediation for other
  industry security standards like NIST, PCI DSS, HIPAA, SOC2, etc. This would involve
  creating a generic framework that can be customized based on the specific security standard.
- Granular Remediation: Implement more granular remediation action test conditions. This
  would allow for automatic remediation based on resource criticality, avoiding remediation on
  very critical resources in production. This could involve integrating with resource management
  tools to identify critical resources.
- GUI Interface: Develop a graphical user interface (GUI) to provide users with a more intuitive
  way to interact with the tool. The GUI could allow users to view the current state of their
  Kubernetes environment's compliance with CIS benchmarks, initiate remediation actions, and
  configure the tool's settings. This would make the tool more accessible to a wider range of
  users, even those who are not familiar with the command line.

#### Acknowledgements

Contributors

- [Danush Adhitya Muthuvel](https://github.com/danushadhitya)
- [Prasanna Venkatesan Aravindan](https://github.com/prasanna7401)
