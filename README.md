
---

# GCP Secure and Isolated Environment Setup

### ![High-Level Architecture Diagram](images/ARD.png)


## Overview

This project involves setting up a secure and isolated environment on Google Cloud Platform (GCP) for a new application using CloudSQL, GKE (Google Kubernetes Engine), and Redis, all within a custom VPC. The architecture is designed to enhance security, optimize costs, and ensure high availability.

## High-Level Architecture

### Networking Setup:
The environment uses a **custom Virtual Private Cloud (VPC)** with dedicated subnets for different components to ensure network isolation. The components involved are:

- **Google Kubernetes Engine (GKE)**: The application workloads run on GKE within a dedicated subnet.
- **CloudSQL**: Managed relational database service in its own isolated subnet.
- **Redis**: Caching layer also deployed in its own subnet.
  
The network design includes:

- **Private IPs**: All resources (GKE, CloudSQL, Redis) leverage private IPs to avoid exposure to the public internet.
- **Firewall Rules**: Custom firewall rules are configured to allow only the necessary traffic between the components. For instance, GKE has restricted access to CloudSQL and Redis, and only specific sources can access the resources.
- **VPC Peering**: Used for connecting the components, ensuring internal traffic stays isolated within the VPC.
- **VPC Flow Logs**: Enabled to capture and analyze network traffic within the VPC.

## Security

### Key Security Measures:
- **IAM Policies**: Role-based Identity and Access Management (IAM) policies are implemented to enforce **least-privilege access**, ensuring users and services only have the permissions they need.
- **Encryption**:
  - **Data at Rest**: All data stored in CloudSQL, Redis, and GKE is encrypted using **Google-managed encryption keys**.
  - **Encryption in Transit**: **TLS** (Transport Layer Security) is enforced to ensure that all data transmitted over the network is secure.
- **API Access Control**: The GKE API access is restricted to only authorized networks, ensuring that only trusted systems can interact with the GKE cluster.
- **Cloud Monitoring and Alerts**: 
  - **Stackdriver** is utilized for monitoring the infrastructure and setting up alerts to proactively detect and respond to any anomalies.
  - **VPC Flow Logs** are used to monitor and analyze network traffic, providing visibility into any unauthorized access or issues.

## Cost Optimization and High Availability

### Strategies for Cost Optimization and High Availability:
- **Preemptible VMs**: Preemptible VMs are used for non-critical GKE workloads, offering significant cost savings while ensuring that critical workloads are unaffected by VM termination.
- **Auto-scaling**: GKE and CloudSQL are configured with autoscaling to dynamically adjust resource usage based on demand, ensuring efficient resource allocation and cost savings.
- **Multi-Zonal Deployments**: To enhance fault tolerance and ensure high availability, both CloudSQL and GKE are deployed across multiple zones. This configuration ensures that if one zone experiences an issue, resources in other zones can take over.
- **Redis High-Availability Replication**: Redis is configured with high-availability replication to prevent downtime in case of node failures.
- **Committed-Use Discounts**: Google Cloud's **committed-use contracts** are used to reduce costs for CloudSQL and Redis, offering significant discounts in exchange for long-term usage commitments.
- **Automated Backups**: Regular automated backups are configured for both CloudSQL and Redis to safeguard against data loss and ensure business continuity.
- **Budget Alerts**: Cloud Monitoring is used to set up budget alerts, helping to track costs and prevent budget overruns while maintaining efficiency.

## Summary

This setup ensures a **secure** environment by leveraging **private networking**, **IAM policies**, and **encryption**. Cost optimization is achieved through **preemptible VMs**, **autoscaling**, and **committed-use discounts**, while **high availability** is ensured using **multi-zonal deployments** and **Redis replication**.

---

**Evaluation Criteria**:

- Demonstrated understanding of **GCP services** and **networking** principles.
- Critical thinking in the areas of **security** and **cost optimization**.

---

