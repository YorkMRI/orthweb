# Orthweb - Orthanc on AWS
<a href="https://www.orthanc-server.com/"><img style="float" align="right" src="docs/assets/images/orthanc_logo.png"></a>

[![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?logo=docker&logoColor=white)](https://www.docker.com/)
[![Terraform](https://img.shields.io/badge/terraform-%235835CC.svg?logo=terraform&logoColor=white)](https://www.terraform.io/)
[![Postgres](https://img.shields.io/badge/postgres-%23316192.svg?logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![envoybadge](https://img.shields.io/badge/envoyproxy-%23ac6199.svg?logo=envoyproxy&logoColor=white)](https://www.envoyproxy.io/)
[![Linux](https://img.shields.io/badge/Linux-FCC624?logo=linux&logoColor=black)](https://aws.amazon.com/amazon-linux-2)
[![AWS](https://img.shields.io/badge/AWS-%23FF9900.svg?logo=amazon-aws&logoColor=white)](https://portal.aws.amazon.com/)
[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![Latest Release](https://img.shields.io/github/v/release/digihunch/orthweb)](https://github.com/digihunch/orthweb/releases/latest) 
## Overview

**[Orthweb](https://github.com/digihunch/orthweb)** helps imaging IT administrators operationalize **[Orthanc](https://www.orthanc-server.com/)** on AWS. The [documentation](https://digihunch.github.io/orthweb/) provides a step-by-step guide for deployment and discussions about the architecture.

Imaging IT administrators host Orthanc on a secure cloud platform. A large organization typically have a shared IT service team build their own platform with multi-VPC networking infrastructure on AWS, commonly known as a [landing zone](https://www.digihunch.com/2022/12/landing-zone-in-aws/). Each department in the organization deploys their own applications on their assigned portion of the network. 

However, many Orthanc adopters are smaller organizations such as startups, research entities and independent health facilities (IHFs) with minimal support from their parent organizations for cloud platform. To fill this gap and accelerate deployment of Orthanc in the cloud, **Orthweb** project was [created](https://www.digihunch.com/2020/11/medical-imaging-web-server-deployment-pipeline/) in 2020.

<img align="middle" src="docs/assets/images/Overview.png">
<br/><br/>

The **Orthweb** template provisions its own self-contained infrastrcture stack in a single AWS account. It does not rely upon an established network infrastructure platform. The network infrastructure layer provisioned in the project contains a single VPC with multiple subnets, along with required endpoints. The infrastructure layer also contains encryption keys, managed database service and S3 storage. The infrastrcture footprint is small but secure. It aims to comply with regulatory requirements such as HIPPA. However, regulatory auditing is the responsibility of the Orthanc adopter. 
<br/><br/>

The **Orthweb** project uses **Terraform** for infrastructure as code. It also automates the installation and configuration of Orthanc application, using server's [bootstrapping](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/bootstrap_container_instance.html) script. Bring your own AWS account, **Orthweb** can typically set up Orthanc server within 30 minutes and start to serve HTTP and DICOM traffic. The project also takes into account other operational aspects, such as high availability, resiliency and automation in the configuration of **Orthanc** application with Docker, using the official [Orthanc image](https://hub.docker.com/r/orthancteam/orthanc). For those considering hosting Orthanc on Kubernetes, check out our sister project [Korthweb](https://github.com/digihunch/korthweb).
