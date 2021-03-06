# Cloud Technology

_Unsystematic_ and _incomplete_ lists of *vendors*, *products*, *buzzwords*, and *whatever*.


## Update

I have just discovered the [Cloud Native Interactive Landscape](https://landscape.cncf.io/) which makes this document obsolete.

---

* **TODO** no *headings*, yes *tags*. because *many-to-many* relationship.
* **TODO** wtf is `rook`, `locksmith`, `vulcand`, `Doorman`, `OpenStack`, `Telegraf`, `Chronograf`, `Kapacitor`

---

## A whimsical list of pivotal points

* 2014 [Kubernetes]
* 2013 [Docker]
* 2010 Python [Flask]
* 2007 [Heroku]
* 2005 Python [Django]
* 1990 [Python]

---

* [Cloud Native Computing Foundation (CNCF)][CNCF]
* [Cloud Security Alliance (CSA)][CSA]
* [Serf] by [HashiCorp]&emsp;Decentralized Cluster Membership, Failure Detection, and Orchestration.

## Infrastructure

* [Amazon Web Services][AWS] (or [AWS]) provides computing instances and networking insfrastructure.
* [Google Cloud] is a direct competitor for [AWS].
* [Microsoft Azure][Azure] is also a competitor for [AWS] and [Google Cloud]
* [Joyent] provides managed private clouds, hosted or on-premise.
* [Alibaba Cloud] claims to have more users in Asia Pacific than any other Cloud platform
* [IBM Cloud] has _DB2_ databases and _Watson_ AI facilities easily accessible.
* [Oracle Cloud] presumably is good for ~~getting sued~~ Oracle database? They claim it's much less expensive than [AWS].
* [DigitalOcean] "developer's cloud"
* [Vultr] "the infrastructure cloud"
* [Linode] "developer's cloud"
* [Imply] Cloud &mdash; managed service for Druid-based storage, query and visualization.

## DNS

* [CoreDNS] xx
* [DNSimple] xx
* [NS1] xx

## Infrastructure as Code (IaC)

* [Terraform] by [HashiCorp]
  Terraform allows infrastructure to be expressed as code in a simple, human readable language called HCL (HashiCorp Configuration Language). Terraform CLI reads configuration files and provides an execution plan of changes, which can be reviewed for safety and then applied and provisioned. Extensible providers allow Terraform to manage a broad range of resources, including hardware, IaaS, PaaS, and SaaS services.

* [Atlantis]. Pull request automation for [Terraform]

* [BOSH] by [Cloud Foundry]
  BOSH is a project that unifies release engineering, deployment, and lifecycle management of small and large-scale cloud software. BOSH can provision and deploy software over hundreds of VMs. It also performs monitoring, failure recovery, and software updates with zero-to-minimal downtime.

  While BOSH was developed to deploy Cloud Foundry PaaS, it can also be used to deploy almost any other software (Hadoop, for instance). BOSH is particularly well-suited for large distributed systems. In addition, BOSH supports multiple Infrastructure as a Service (IaaS) providers like VMware vSphere, Google Cloud Platform, Amazon Web Services EC2, Microsoft Azure, OpenStack, and Alibaba Cloud. There is a Cloud Provider Interface (CPI) that enables users to extend BOSH to support additional IaaS providers such as Apache CloudStack and VirtualBox.

* [CloudFormation] Amazon [AWS]
  
  AWS CloudFormation provides a common language for you to model and provision AWS and third party application resources in your cloud environment. AWS CloudFormation allows you to use programming languages or a simple text file to model and provision, in an automated and secure manner, all the resources needed for your applications across all regions and accounts. This gives you a single source of truth for your AWS and third party resources.

  In other words, it's *closed-source*, *vendor-specific* attempt at [Terraform].

## Storage and backup

Apache [Cassandra] is the right choice when you need scalability and high availability without compromising performance. Linear scalability and proven fault-tolerance on commodity hardware or cloud infrastructure make it the perfect platform for mission-critical data. Cassandra's support for replicating across multiple datacenters is best-in-class, providing lower latency for your users and the peace of mind of knowing that you can survive regional outages.

[Ceph] provides CephFS &mdash; POSIX-compliant network file system. Provides *Block*, *File*, and *Object*.

[Gluster] is a free and open source software scalable network file system. POSIX-compliant. Provides *Block*, *File*, and *Object*.

[Elastic Stack] that's Elasticsearch, Kibana, Beats, and Logstash (also known as the ELK Stack). Reliably and securely take data from any source, in any format, then search, analyze, and visualize it in real time. 

[InfluxDB] is the open source time series database component of the *TICK Stack* (Telegraf, InfluxDB, Chronograf, Kapacitor).

[Veeam] modern data protection for modern challenges. Backup.

## Key-value pair store

**!!!** Note how much of very advanced functionality is enabled by the *KV pair stores*

* [etcd] a distributed, reliable key-value store for the most critical data of a distributed system.

* [Consul] by [HashiCorp] is a service mesh solution providing a full featured control plane with service discovery, configuration, and segmentation functionality. Each of these features can be used individually as needed, or they can be used together to build a full service mesh. Consul requires a data plane and supports both a proxy and native integration model. Consul ships with a simple built-in proxy so that everything works out of the box, but also supports 3rd party proxy integrations such as Envoy.
    
  Other than providing a distributed key-value store, it also provides features like:
    
  * Service discovery (with DNS or HTTP) 
  * Health checks for services and nodes
  * Network infrastructure automation
  * Multi-platform service mesh

  Consul is built on top of [Serf]

 * [ZooKeeper] by Apache
    
   ZooKeeper is a centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services. All of these kinds of services are used in some form or another by distributed applications. Each time they are implemented there is a lot of work that goes into fixing the bugs and race conditions that are inevitable. Because of the difficulty of implementing these kinds of services, applications initially usually skimp on them, which make them brittle in the presence of change and difficult to manage. Even when done correctly, different implementations of these services lead to management complexity when the applications are deployed.

## Network

**DDI** is (DNS, DHCP, and IP address) management.

* [OpenFlow](https://en.wikipedia.org/wiki/OpenFlow) is a communications protocol that gives access to the forwarding plane of a network switch or router over the network. It is crucial to the whole *Software-Defined Networking* enterprise.
* [Infoblox] core network services for the multi-cloud organisation.
* [Project Calico] by Tigera is an open source networking and network security solution for containers, VMs, and native host-based workloads.

## Container orchestration

* [Docker Swarm] is a native container orchestration solution from [Docker, Inc][Docker].
* [Kubernetes] is an open-source system for automating deployment, scaling, and management of containerized applications.
* [k3s] is a highly available, certified Kubernetes distribution designed for production workloads in unattended, resource-constrained, remote locations or inside IoT appliances. Optimized for ARM.
* Apache [Mesos] is a *distributed systems kernel*. It allows to program against the datacenter like it’s a single pool of resources (RAM, CPU, etc). It provides functionality that crosses between IaaS and PaaS.
    * D2iQ [MesoSphere] offers a commercial solution on top of Apache Mesos.
    * [DC/OS] (the Distributed Cloud Operating System) by D2iQ. They also provide a commercial version of it.
      is an open-source, distributed operating system based on the Apache [Mesos] distributed systems kernel. DC/OS manages multiple machines in the cloud or on-premises from a single interface; deploys containers, distributed services, and legacy applications into those machines; and provides networking, service discovery and resource management to keep the services running and communicating with each other.

    * [Marathon] is a production-grade container orchestration platform for DC/OS and Apache Mesos.
* [Nomad] by [HashiCorp] is a *cluster manager* and *resource scheduler*. It can manage containers, VMs, individual applications, etc...
* Amazon [ECS] elastic cloud service (not Kubernetes). Offers Fargate service which figures out the provisioning automatically, only container images have to be provided by the customer.

## Operating systems

* [DC/OS]
* [Bottlerocket] open-source OS, started by Amazon. It is purpose-built to run containers. The updates to [Bottlerocket] can be applied and rolled back in an atomic manner, which makes them easy to automate, reducing management overhead and reducing operational costs. [Bottlerocket] integrates with container orchestrators to enable the automated patching of hosts to improve operational costs, manageability, and uptime.

## Service discovery

* [Consul] by [HashiCorp]

## Hosted services and solutions

### Kubernetes

There is a notion of a *certified* hosted Kubernetes platform.

* [Amazon Elastic Kubernetes Service](https://aws.amazon.com/eks/) (Amazon EKS)
* [Azure Kubernetes Service](https://azure.microsoft.com/en-us/services/kubernetes-service/) (AKS)
* [Google Kubernetes Engine](https://cloud.google.com/kubernetes-engine/) (GKE)
* [IBM Cloud Kubernetes Service](https://www.ibm.com/cloud/container-service/)
* [NetApp Project Astra](https://cloud.netapp.com/project-astra)
* [Oracle Container Engine for Kubernetes](https://www.oracle.com/cloud/compute/container-engine-kubernetes.html)
* [OpenShift] by [RedHat]
* [VMWare Tanzu Kubernetes Grid](https://tanzu.vmware.com/kubernetes-grid) (TKG)

## "*Cloud Native*"

In the *Cloud Native* approach, we design a package and run applications on top of our infrastructure (on-premise or cloud) using operations tools like containers, container orchestration, and services like continuous integration, logging, monitoring, etc. Kubernetes integrated with several tools meets our requirements to run *Cloud Native* applications.

[Draft vs Gitkube vs Helm vs Ksonnet vs Metaparticle vs Skaffold](https://hasura.io/blog/draft-vs-gitkube-vs-helm-vs-ksonnet-vs-metaparticle-vs-skaffold-f5aa9561f948/)

* [Helm]

  It is a popular package manager for Kubernetes. Helm packages Kubernetes applications into Charts, with all the artifacts, objects, and dependencies an entire application needs in order to successfully be deployed in a Kubernetes cluster. Using Helm Charts, which are stored in repositories, we can share, install, upgrade, or rollback an application that was built to run on Kubernetes. Helm is a graduated project of [CNCF].
  
* [Draft]

  It is being promoted as a developer tool for cloud-native applications running on Kubernetes, and it allows for an application to be containerized and deployed on Kubernetes.
  
* [Skaffold]

  It is a tool from Google that helps us build, push, and deploy code to the Kubernetes cluster. It supports Helm, and it also provides building blocks and describes customizations for a CI/CD pipeline.
  
* [Argo]

  It is a container-native workflow engine for Kubernetes. Its use cases include running Machine Learning, Data Processing, and CI/CD tasks on Kubernetes.

* [Jenkins X]

  Jenkins is a very popular tool for CI/CD that can be used on Kubernetes as well. But the Jenkins team built a new cloud-native CI/CD tool, Jenkins X, from the ground up. The new tool leverages Docker, Draft, and Helm to deploy a Jenkins CI/CD pipeline directly on Kubernetes, by simplifying and automating full CI/CD pipelines. In addition, Jenkins X automates the preview of pull requests for fast feedback before changes are merged, and then it automates the environment management and the promotion of new application versions between different environments. Jenkins X is a graduated project of [CD Foundation].
  
* [Tekton] by Google is a powerful yet flexible Kubernetes-native open-source framework for creating continuous integration and delivery (CI/CD) systems. It lets you build, test, and deploy across multiple cloud providers or on-premises systems by abstracting away the underlying implementation details.

* [Spinnaker]

  It is an open source multi-cloud continuous delivery platform from Netflix for releasing software changes with high velocity. It supports all the major cloud providers like Amazon Web Services, Microsoft Azure, Google Cloud Platform, and OpenStack. It supports Kubernetes natively. Spinnaker is a graduated project of CD Foundation.

## Serverless (FaaS)

Function as a Service (FaaS): AWS Lambda, Google ?, Azure ?

* [OpenFaaS] makes it simple to deploy both functions and existing code to Kubernetes. Avoid lock-in through the use of Docker.
* [Kubeless]
* [Azure Container Instances]

## REST APIs

* [Swagger] is an open-source software set of tools to design, build, document, and use RESTful web services, developed by [SmartBear Software]. It includes automated documentation, code generation, and test-case generation.
* [Postman] is a collaboration platform for API development.

## GitOps

* [GitLab]

* [Weave Flux] enables continuous delivery of container images, using version control for each step to ensure deployment is reproducible, auditable and revertible.
* [GitKube] is tool for building and deploying docker images on Kubernetes using `git push`.

  After a simple initial setup, users can simply keep git push-ing their repos to build and deploy docker images to Kubernetes automatically. It can be configured to update any k8s deployment with a newly built image using dockerfile present in the repo.
  
* [Tidelift] provides curated catalogs of known-good open source components and the capacity to create private catalogs for the enterprise.

## Communication

* [Gitter] by [GitLab] is a chat and networking platform that helps to manage, grow and connect communities through messaging, content and discovery.
* [Twilio] global SIM for Iot. Phone numbers. SMS. APIs. Contact Centre platform. And more.

## Configuration Management

These tools allow us to define the desired state of the systems in an automated way. At any point in time, we want to have a consistent and desired state of systems and software installed on them. This is also referred to as *Infrastructure as Code (IaC)*.

* [Ansible] is agentless
* [Chef]
* [Puppet] is popular at Google. 
* [Salt] is most obscure of all mentioned. LinkedIn runs it.
* [Bitnami] packaged applications.

Automated *image builders*:

* [Packer] by [HashiCorp]

## Logging, Monitoring, and Security

[cAdvisor] (Container Advisor) provides container users an understanding of the resource usage and performance characteristics of their running containers. It is a running daemon that collects, aggregates, processes, and exports information about running containers. Specifically, for each container it keeps resource isolation parameters, historical resource usage, histograms of complete historical resource usage and network statistics. This data is exported by container and machine-wide.

cAdvisor has native support for [Docker] containers and should support just about any other container type out of the box. We strive for support across the board so feel free to open an issue if that is not the case. cAdvisor's container abstraction is based on [lmctfy]'s so containers are inherently nested hierarchically.

---

* [Codacy] automatically identify issues through static code review analysis. Get notified on security issues, code coverage, code duplication, and code complexity in every commit and pull request, directly from your current workflow.
* [DataDog] provides intelligent application and service monitoring, particularly suited for debugging microservices.
* [flannel] allocates a subnet lease to each host out of a larger, preconfigured address space.
* [Fluentd] is an open source data collector for unified logging layer. Fluentd allows you to unify data collection and consumption for a better use and understanding of data.
* [Grafana] provides pretty dashboards. It is used by thousands of companies to monitor everything from Prometheus & Graphite metrics, logs, applications, power plants, beehives, sourdough starters and custom data sources.
* [New Relic] observability platform
* [PagerDuty] is a SaaS *incident response platform* for IT departments.
* [Prometheus] is an open source tool used for system monitoring and alerting. It is suitable for recording *any purely numeric time-series data*. It is primarily written in Go. It was originally developed by SoundCloud and is now one of the graduated projects at the [CNCF] Foundation.
* [Retrace] by [Stackify]
* [Sentinel]&emsp;_policy as code_ framework for [HashiCorp] Enterprise Products.
* [Splunk] includes a family of products aiming to deliver highly scalable and fast real-time insight into enterprise data. It allows for data aggregation and analysis, with unique investigative methods. Provides dashboards!
* [Styra] provides *declarative authorization* for *Cloud Native* security. It is made by the founders and maintainers of [Open Policy Agent].
* [sysdig] scans for vulnerabilities and provides a view inside containers to alert on anomalous behavior and application health issues. It allows very rapid container and Kubernetes visibility and security onboarding.
* [Vault] by HashiCorp (secrets management)

## Distributed Tracing

With widespread adoption of microservices comes the need to have facilities to troubleshoot unexpected behaviours and latency issues. This may be very hard, due to the distributed nature of modern systems.

Distributed tracing serves to solve this problem.

* Proprietary: [Zipkin], [Dapper], [HTrace], and [X-Trace]
* Open: [OpenTelemetry] is a merger of [OpenTracing] (deprecated) and [OpenCensus] (deprecated). It is a [CNCF] project.
* Open: [Jaeger] is open source, end-to-end distributed tracing tool.

[Wavefront], now called VMware Tanzu Observability (bleurgh).

## Service Mesh

* [Consul] by [HashiCorp] is an open source project aiming to provide a secure multi-cloud service networking through automated network configuration and service discovery.
* [Tanzu] by [VMWare]

### Data Plane

* [Linkerd] is a [CNCF] project. It adds critical security, observability, and reliability features to your Kubernetes stack—no code change required. Zero-trust multi-cluster Kubernetes. It can be installed *per host* or *instance*, as a **replacement for the sidecar deployment**.
* [NGINX]
* [HAProxy]
* [Envoy], a [CNCF] project. It can be set up as a *sidecar proxy* or as an *edge proxy*. **The most popular Serice Mesh proxy today.**
* [Traefik] from [Containous] is the Cloud Native Edge Router (ingress proxy).
* [Maesh] from [Containous] is a straight-forward, easy to configure, and non-invasive service mesh that allows visibility and management of the traffic flows inside any Kubernetes cluster.

### Control Plane

* [Istio] to connect, secure, control, and observe services. It uses an extended version of the [Envoy] proxy, deployed as *sidecars*.
* [Nelson] multi-cloud orchestrator (?)
* [SmartStack]
* [Kuma] is a [CNCF] project and is based on [Envoy]. It was originally created by [Kong]. Can be installed in a *universal* mode, or in a *Kubernetes* mode which injects a *proxy sidecar* into desired *Kubernetes Pods*.

## Algorithms

This is not a *vendor*, but I have no better place to record this for now.

* [Raft] *consensus algorithm* is used by *Docker Swarm Manager* nodes to maintain the cluster state.

<!-- Links used in the document: alphabetically ordered, ignoring case -->
[Alibaba Cloud]: https://www.alibabacloud.com/
[Ansible]: https://www.ansible.com/
[Argo]: https://argoproj.github.io/
[Atlantis]: https://www.runatlantis.io/
[AWS]: https://aws.amazon.com/
[Azure]: https://azure.microsoft.com/en-gb/
[Bitnami]: https://bitnami.com/
[Bosh]: https://bosh.io/
[Bottlerocket]: https://github.com/bottlerocket-os/bottlerocket
[cAdvisor]: https://github.com/google/cadvisor/
[Cassandra]: https://cassandra.apache.org/
[CD Foundation]: https://cd.foundation/
[Ceph]: https://ceph.io/
[Chef]: https://www.chef.io/products/automate
[Cloud Foundry]: https://www.cloudfoundry.org/
[CloudFormation]: https://aws.amazon.com/cloudformation/
[CNCF]: https://www.cncf.io/
[Codacy]: https://www.codacy.com/
[Consul]: https://www.consul.io/
[Containous]: https://containo.us/
[CoreDNS]: https://coredns.io/
[CSA]: https://cloudsecurityalliance.org/
[Dapper]: https://medium.com/@suhadevvenkatesh/dapper-googles-secret-weapon-56e43cd61653
[DataDog]: https://www.datadoghq.com/
[DC/OS]: https://dcos.io/
[Django]: https://www.djangoproject.com/
[DNSimple]: https://dnsimple.com/
[Docker]: https://www.docker.com/
[Docker Swarm]: https://docs.docker.com/engine/swarm/
[Draft]: https://draft.sh/
[Elastic Stack]: https://www.elastic.co/elastic-stack
[Envoy]: https://www.envoyproxy.io/
[etcd]: https://etcd.io/
[flannel]: https://github.com/coreos/flannel#flannel
[Flask]: https://palletsprojects.com/p/flask/
[Fluentd]: https://www.fluentd.org/
[GitKube]: https://gitkube.sh/
[GitLab]: https://about.gitlab.com/
[Gitter]: https://gitter.im/
[Gluster]: https://www.gluster.org/
[Google Cloud]: https://cloud.google.com/
[Grafana]: https://grafana.com/
[HAProxy]: http://www.haproxy.org/
[HashiCorp]: https://www.hashicorp.com/
[Helm]: https://helm.sh/
[Heroku]: https://www.heroku.com/
[IBM Cloud]: https://www.ibm.com/cloud
[Imply]: https://imply.io/
[InfluxDB]: https://www.influxdata.com/products/influxdb-overview/
[Infoblox]: https://www.infoblox.com/
[Istio]: https://istio.io/
[Jaeger]: https://www.jaegertracing.io/
[Jenkins X]: https://jenkins-x.io/
[Joyent]: https://www.joyent.com/
[k3s]: https://k3s.io/
[Kong]: https://konghq.com/
[Kubernetes]: https://kubernetes.io/
[Kuma]: https://kuma.io/
[lmctfy]: https://github.com/google/lmctfy
[Linkerd]: https://linkerd.io/
[Linode]: https://www.linode.com/
[Maesh]: https://containo.us/maesh/
[Marathon]: https://mesosphere.github.io/marathon/
[Mesos]: https://mesos.apache.org/
[Mesosphere]: https://d2iq.com/solutions/mesosphere/dcos
[Nelson]: https://getnelson.io/
[New Relic]: https://newrelic.com/
[NGINX]: https://www.nginx.com/
[NS1]: https://ns1.com/
[OpenCensus]: https://opencensus.io/
[OpenFaaS]: https://www.openfaas.com/
[OpenShift]: https://www.openshift.com/products
[OpenTelemetry]: https://opentelemetry.io/
[OpenTracing]: https://opentracing.io/
[Oracle Cloud]: https://www.oracle.com/uk/cloud/
[Packer]: https://www.packer.io/
[PagerDuty]: https://www.pagerduty.com/
[Postman]: https://www.postman.com/
[Project Calico]: https://www.projectcalico.org/
[Prometheus]: https://prometheus.io/
[Puppet]: https://puppet.com/
[Python]: https://www.python.org/
[Raft]: https://raft.github.io/
[RedHat]: https://www.redhat.com/
[Retrace]: https://stackify.com/retrace/
[Salt]: https://www.saltstack.com/
[Sentinel]: https://www.hashicorp.com/sentinel
[Serf]: https://www.serf.io/
[Skaffold]: https://skaffold.dev/
[SmartBear Software]: https://smartbear.com/
[SmartStack]: https://www.smartstack.co.uk/
[Spinnaker]: https://spinnaker.io/
[Splunk]: https://www.splunk.com/
[Stackify]: https://stackify.com/
[Styra]: https://www.styra.com/
[Swagger]: https://swagger.io/
[sysdig]: https://sysdig.com/
[Tanzu]: https://tanzu.vmware.com/service-mesh
[Tekton]: https://cloud.google.com/tekton
[Terraform]: https://www.terraform.io/
[Tidelift]: https://tidelift.com/
[Tigera]: https://www.tigera.io/
[Traefik]: https://containo.us/traefik/
[Twilio]: https://www.twilio.com/
[Vault]: https://www.vaultproject.io/
[Veeam]: https://www.veeam.com/
[VMWare]: https://www.vmware.com/
[Wavefront]: https://www.wavefront.com/
[Weave Flux]: https://www.weave.works/oss/flux/
[Zipkin]: https://zipkin.io/
[ZooKeeper]: https://zookeeper.apache.org/
