## Overview

Orthanc handles sensitive data and must be hosted on secure platforms. The motive of **Orthweb** project is to accelerate Orthanc deployment on Amazon Web Services (AWS) platform. The Orthweb project includes:

1. A prescriptive architecture optimized for hosting Orthanc. The architecture is opinionated but suitable for common scenarios. The architecture design is discussed in the [Infrastructure](../design/infrastructure.md) section.

2. The implementation artifact for the prescriptive architecture with Infrastructure-as-Code template in [Terraform](https://www.terraform.io/). The **Orthanc Terraform template** is available in the [orthweb](https://github.com/digihunch/orthweb) GitHub repository.

3. A baseline Orthanc configuration with key plugins such as advanced authorization and KeyCloak. The artifact for configuration management is available in the [orthanc-config](https://github.com/digihunchinc/orthanc-config) GitHub repository.

Since the cloud operation model varies significantly from organization to organization, each user may need different parts of this project to facilitate their Orthanc deployment.

## Use case

If you have an AWS account without networking foundation for Orthanc, the template in [Orthweb](https://github.com/digihunch/orthweb) suits exactly to your needs. Then you may use the automation artifact in [orthanc-config](https://github.com/digihunchinc/orthanc-config) to configure Orthanc. 

If you have pre-created networking layer (e.g. VPC, subnets), then you only need to create virtual machine with relevant dependencies before installing Orthanc. You can use **Orthweb** as a reference implementation to understand how the application interact with underlying cloud resources, and potentially reuse some Terraform [modules](https://github.com/digihunch/orthweb/tree/main/terraform/modules). 

To let Terraform create resources in AWS, it needs sufficient permissions for deployment. Such permission for deployment usually requires administrator-level access.

## Toolings

Orthweb is based on numerous open-source tools. Here are the rationales behind the choice of tools.

**Terraform** is a widely used infrastructure-as-code utility. The templates are written in Hashicorp Configuration Language(HCL), which strikes a good balance between declarativeness and level of abstraction. However, you do need to securely store [Terraform state](https://developer.hashicorp.com/terraform/language/state), and be wary of its [workflow nuances](https://itnext.io/pains-in-terraform-collaboration-249a56b4534e). 

**Docker** is a simple way to host container workload. The **Orthweb** solution uses `Docker Compose` to orchestrate several containers of different purposes which is widely used by application developers. [Amazon ECS](https://aws.amazon.com/ecs/) is an alternative with some [limitations](https://github.com/digihunch/orthweb/issues/1#issuecomment-852669561) and concerns on platform lock-in.

**PostgreSQL** is the choice of database amongst all the database engines that Orthanc supports. It is feature rich and supports analytical workloads. AWS has two flavours of managed PostgreSQL: `RDS for PostgreSQL` and `Aurora PostgreSQL`. The Orthweb solutions works with the former. 

**Nginx Proxy** is a widely adopted reverse proxy to handle incoming requests. There are several alternative reverse proxy technologies. From 2022 to 2024, **Orthweb** uses Envoy Proxy. Since 2024, Orthweb switched back to Nginx as the default reverse proxy because it is the popular choice in the Orthanc user community.

**Amazon S3** is a scalable, feature-rich object storage platform well integrated with other AWS cloud services. S3 is the de-facto standard for object storage and Orthanc can store DICOM objects using S3 plugin. The pre-compiled binary for S3 plugin has been included the Orthanc release since 2022.


## Getting Started

If you just want to start deploying Orthanc, skip to the [Deployment](../deployment/preparation.md) section. Otherwise, in the next section, we will discuss the architecture design, how to use and what to expect from the **Orthweb** solution.