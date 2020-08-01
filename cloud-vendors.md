# Cloud technology vendors

This is an **incomplete** list of Cloud-related technology providers, both hardware and software. It is continuously updated as I find new vendors.

* **TODO** change categories to labels because a tree is not a good representation for a complex landscape of technology vendors

## Infrastructure

* [Amazon Web Services (AWS)](https://aws.amazon.com/)
* [Google Cloud](https://cloud.google.com/)
* [Microsoft Azure](https://azure.microsoft.com/en-gb/)
* [Joyent](https://www.joyent.com/) provides managed private clouds, hosted or on-premise.

## Container orchestration

* [Kubernetes](https://kubernetes.io/) is an open-source system for automating deployment, scaling, and management of containerized applications.
* [k3s](https://k3s.io/) is a highly available, certified Kubernetes distribution designed for production workloads in unattended, resource-constrained, remote locations or inside IoT appliances. Optimized for ARM.

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

&mdash; Oliver Frolovs, 2020