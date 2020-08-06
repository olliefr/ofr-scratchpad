# Cloud technology vendors

This is an **incomplete** list of Cloud-related technology providers, both hardware and software. It is continuously updated as I find new vendors.

* **TODO** change categories to labels because a tree is not a good representation for a complex landscape of technology vendors

## Infrastructure

* [Amazon Web Services (AWS)](https://aws.amazon.com/) has *Amazon EC2: Elastic Compute Cloud*
* [Google Cloud](https://cloud.google.com/)
* [Microsoft Azure](https://azure.microsoft.com/en-gb/)
* [Joyent](https://www.joyent.com/) provides managed private clouds, hosted or on-premise.

## Network

* [OpenFlow](https://en.wikipedia.org/wiki/OpenFlow) is a communications protocol that gives access to the forwarding plane of a network switch or router over the network. It is crucial to the whole *Software-Defined Networking* enterprise.

## Container orchestration

* [Docker Swarm](https://docs.docker.com/engine/swarm/) is a native container orchestration solution from [Docker, Inc](https://www.docker.com/).
* [Kubernetes](https://kubernetes.io/) is an open-source system for automating deployment, scaling, and management of containerized applications.
* [k3s](https://k3s.io/) is a highly available, certified Kubernetes distribution designed for production workloads in unattended, resource-constrained, remote locations or inside IoT appliances. Optimized for ARM.
* Apache [Mesos](https://mesos.apache.org/) is a *distributed systems kernel*. It allows to program against the datacenter like it’s a single pool of resources (RAM, CPU, etc). It provides functionality that crosses between IaaS and PaaS.
    * D2iQ [MesoSphere](https://d2iq.com/solutions/mesosphere/dcos) offers a commercial solution on top of Apache Mesos.
    * [DC/OS](https://dcos.io/) has been open-sourced by D2iQ. They also provide a commercial version of it.
    * [Marathon](https://mesosphere.github.io/marathon/) is a production-grade container orchestration platform for DC/OS and Apache Mesos.
* Hashicorp [Nomad] is a cluster manager and resource scheduler. Containers, VMs, individual applications, etc...
* Amazon [ECS] elastic cloud service (not Kubernetes). Offers Fargate service which figures out the provisioning automatically, only container images have to be provided by the customer.

## Service discovery

* Hashicorp [Consul](https://www.hashicorp.com/products/consul)

## Hosted services and solutions

### Kubernetes

There is a notion of a *certified* hosted Kubernetes platform.

* [Amazon Elastic Kubernetes Service](https://aws.amazon.com/eks/) (Amazon EKS)
* [Azure Kubernetes Service](https://azure.microsoft.com/en-us/services/kubernetes-service/) (AKS)
* [Google Kubernetes Engine](https://cloud.google.com/kubernetes-engine/) (GKE)
* [IBM Cloud Kubernetes Service](https://www.ibm.com/cloud/container-service/)
* [NetApp Project Astra](https://cloud.netapp.com/project-astra)
* [Oracle Container Engine for Kubernetes](https://www.oracle.com/cloud/compute/container-engine-kubernetes.html)
* [RedHat OpenShift](https://www.openshift.com/products)
* [VMWare Tanzu Kubernetes Grid](https://tanzu.vmware.com/kubernetes-grid) (TKG)

## "*Cloud Native*"

In the *Cloud Native* approach, we design a package and run applications on top of our infrastructure (on-premise or cloud) using operations tools like containers, container orchestration, and services like continuous integration, logging, monitoring, etc. Kubernetes integrated with several tools meets our requirements to run *Cloud Native* applications.

[Draft vs Gitkube vs Helm vs Ksonnet vs Metaparticle vs Skaffold](https://hasura.io/blog/draft-vs-gitkube-vs-helm-vs-ksonnet-vs-metaparticle-vs-skaffold-f5aa9561f948/)

* [Helm](https://helm.sh/)

  It is a popular package manager for Kubernetes. Helm packages Kubernetes applications into Charts, with all the artifacts, objects, and dependencies an entire application needs in order to successfully be deployed in a Kubernetes cluster. Using Helm Charts, which are stored in repositories, we can share, install, upgrade, or rollback an application that was built to run on Kubernetes. Helm is a graduated project of [CNCF](https://www.cncf.io/).
  
* [Draft](https://draft.sh/)

  It is being promoted as a developer tool for cloud-native applications running on Kubernetes, and it allows for an application to be containerized and deployed on Kubernetes.
  
* [Skaffold](https://skaffold.dev/)

  It is a tool from Google that helps us build, push, and deploy code to the Kubernetes cluster. It supports Helm, and it also provides building blocks and describes customizations for a CI/CD pipeline.
  
* [Argo](https://argoproj.github.io/)

  It is a container-native workflow engine for Kubernetes. Its use cases include running Machine Learning, Data Processing, and CI/CD tasks on Kubernetes.

* [Jenkins X](https://jenkins-x.io/)

  Jenkins is a very popular tool for CI/CD that can be used on Kubernetes as well. But the Jenkins team built a new cloud-native CI/CD tool, Jenkins X, from the ground up. The new tool leverages Docker, Draft, and Helm to deploy a Jenkins CI/CD pipeline directly on Kubernetes, by simplifying and automating full CI/CD pipelines. In addition, Jenkins X automates the preview of pull requests for fast feedback before changes are merged, and then it automates the environment management and the promotion of new application versions between different environments. Jenkins X is a graduated project of [CD Foundation](https://cd.foundation/).

* [Spinnaker](https://spinnaker.io/)

  It is an open source multi-cloud continuous delivery platform from Netflix for releasing software changes with high velocity. It supports all the major cloud providers like Amazon Web Services, Microsoft Azure, Google Cloud Platform, and OpenStack. It supports Kubernetes natively. Spinnaker is a graduated project of CD Foundation.

## GitOps

* [Weave Flux](https://www.weave.works/oss/flux/) enables continuous delivery of container images, using version control for each step to ensure deployment is reproducible, auditable and revertible.
* [GitKube](https://gitkube.sh/) is tool for building and deploying docker images on Kubernetes using `git push`.

  After a simple initial setup, users can simply keep git push-ing their repos to build and deploy docker images to Kubernetes automatically. It can be configured to update any k8s deployment with a newly built image using dockerfile present in the repo.
    
# Configuration Management

These tools allow us to define the desired state of the systems in an automated way. At any point in time, we want to have a consistent and desired state of systems and software installed on them. This is also referred to as *Infrastructure as Code (IaaC)*.

* [Ansible](https://www.ansible.com/)
* [Chef](https://www.chef.io/products/automate)
* [Puppet](https://puppet.com/)
* [Salt](https://www.saltstack.com/)

## Monitoring and Security

* [DataDog](https://www.datadoghq.com/) provides intelligent application and service monitoring, particularly suited for debugging microservices.
* [sysdig](https://sysdig.com/) scans for vulnerabilities and provides a view inside containers to alert on anomalous behavior and application health issues. It allows very rapid container and Kubernetes visibility and security onboarding.
* Hashicorp [Vault](https://www.vaultproject.io/) secrets management

## Algorithms

This is not a *vendor*, but I have no better place to record this for now.

* [Raft consensus algorithm](https://raft.github.io/) is used by *Docker Swarm Manager* nodes to maintain the cluster state.

&mdash; Oliver Frolovs, 2020