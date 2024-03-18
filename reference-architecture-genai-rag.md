---

copyright:
  years: 2024
lastupdated: "2024-03-06"

subcollection: pattern-genai-rag

authors:
- name: Ana Biazetti

# The release that the reference architecture describes
version: 1.0

# Use if the reference architecture has deployable code.
# Value is the URL to land the user in the IBM Cloud catalog details page for the deployable architecture.
# See https://test.cloud.ibm.com/docs/get-coding?topic=get-coding-deploy-button
deployment-url:

docs: /docs/pattern-genai-rag

content-type: reference-architecture

---
<!--
The following line inserts all the attribute definitions. Don't delete.
-->
{{site.data.keyword.attribute-definition-list}}

<!--
Don't include "reference architecture" in the following title.
Specify a title based on a use case. If the architecture has a module
or tile in the IBM Cloud catalog, match the title to the catalog. See
https://test.cloud.ibm.com/docs/solution-as-code?topic=solution-as-code-naming-guidance.
-->

# RAG Pattern for WatsonX on IBM Cloud <!-- H1 -->
{: #genai-rag}
{: toc-content-type="reference-architecture"}
{: toc-version="1.0"}

<!--
The IDs, such as {: #title-id} are required for publishing this reference architecture in IBM Cloud Docs. Set unique IDs for each heading. Also include
the toc attributes on the H1, repeating the values from the YAML header.
 -->

<!-->:information_source: **Tip:** For more information about this template, see [Creating reference architectures](https://test.cloud.ibm.com/docs/writing?topic=writing-reference-architectures).-->

:information_source:

This reference architecture will summarize the best practices and Architecture Decisions for Watsonx RAG Pattern deployment on IBM Cloud.

AI hold the promise to revolutionize life and business but raises concerns in trust, security, and regulatory compliance. Understanding Gen AI and its infrastructure is vital for navigating this complex landscape. This reference architecture will showcase how IBM Cloud and WatsonX provide a secure environment for deploying and governing Gen AI RAG pattern applications. 

Retrieval Augmented Generation (RAG) pattern where the AI power natural language search query gets relevant content from a company's data. A use case could include an insurance company virtual assistant. Prospective clients can interact with the virtual agent and ask questions about insurance.


## Architecture diagram
{: #architecture-diagram}

![Architecture.](ref-arch.svg "Architecture"){: caption="Figure 1. Reference Architecture" caption-side="bottom"}

If you have a list or text to describe the diagram, include it here.

## Design concepts
{: #design-concepts}

Below is a map that covers design considerations and architecture decisions for the following aspects and domains:
* **Data:** Artifical Intelligence
* **Compute:** Virtual Servers
* **Storage:** Primary storage
* **Networking:** Enterprise connectivity, BYOIP / Edge gateways, Load balancing, Domain name services
* **Security:** Data secuirty, Identity & access, Application security, Infrastructure & endpoints, and Governance, risk & compliance
* **DevOps:** Build & test, Delivery pipeline, Code repository
* **Resiliency:** High availability
* **Service Management:** Monitoring, Logging, Auditing/tracking, Automated deployment

![heatmap](heatmap.svg "Current diagram"){: caption="Figure 2. Figure 2. Architecture design scope" caption-side="bottom"}

## Requirements
{: #requirements}

The following table outlines the requirements that are addressed in this architecture.

| Aspect | Requirements |
| -------------- | -------------- |
| Data            | Data residency requirements require that the customer’s data not leave the region. |
| Compute            | Provide properly isolated compute resources with adequate compute capacity for the applications. |
| Storage            | Provide storage that meets the application and database performance requirements. |
| Networking         | Deploy workloads in isolated environment and enforce information flow policies. \n Provide secure, encrypted connectivity to the cloud’s private network for management purposes. \n Distribute incoming application requests across available compute resources. \n Support failover of application to alternate site in the event of planned or unplanned outages \n Provide public and private DNS resolution to support use of hostnames instead of IP addresses. |
| Security           | Ensure all operator actions are executed securely through a bastion host. \n Protect the boundaries of the application against denial-of-service and application-layer attacks. \n Encrypt all application data in transit and at rest to protect from unauthorized disclosure. \n Encrypt all backup data to protect from unauthorized disclosure. \n Encrypt all security data (operational and audit logs) to protect from unauthorized disclosure. \n Encrypt all data using customer managed keys to meet regulatory compliance requirements for additional security and customer control. \n Protect secrets through their entire lifecycle and secure them using access control measures. |
| DevOps            | THIS NEEDS TO BE UPDATED |
| Resiliency         | Support application availability targets and business continuity policies. \n Ensure availability of the application in the event of planned and unplanned outages. \n Provide highly available compute, storage, network, and other cloud services to handle application load and performance requirements. \n Backup application data to enable recovery in the event of unplanned outages. \n Provide highly available storage for security data (logs) and backup data. \n Automate recovery tasks to minimize down time |
| Service Management | Monitor system and application health metrics and logs to detect issues that might impact the availability of the application. \n Generate alerts/notifications about issues that might impact the availability of applications to trigger appropriate responses to minimize down time. \n Monitor audit logs to track changes and detect potential security problems. \n Provide a mechanism to identify and send notifications about issues found in audit logs. |
{: caption="Table 1. Requirements" caption-side="bottom"}

## Components
{: #components}

Update the following table below with components that are unique to this architecture. Introduce the table with a sentence. For example, "The following table outlines the products or services used in the architecture for each aspect."

| Aspects | Architecture components | How the component is used |
| -------------- | -------------- | -------------- |
| Data | WatsonX Assistance | Conversational artificial intelligence platform |
|  | Watson Discovery | Automates the discovery of information and insights with advanced Natural Language Processing and Understanding. |
| Compute | Virtual Servers for VPC | Web, App, and database servers |
| Storage | Cloud Object Storage | Web app static content, backups, logs (application, operational, and audit logs) |
|  | VPC Block Storage | Web app storage if needed |
| Networking | VPC Virtual Private Network (VPN) | Remote access to manage resources in private network |
|  | Virtual Private Endpoint (VPE) | For private network access to Cloud Services, e.g., Key Protect, COS, etc. |
|  | VPC Load Balancers | Application Load Balancing for web servers, app servers, and database servers |
|  | Direct Link 2.0 | Seamlessly connect on-premises resources to cloud resources. |
|  | Transit Gateway (TGW) | Connects the Workload and Management VPCs within a region.
|  | Cloud Internet Services (CIS) | Global load balancing between regions. Public DNS resolution. |
| Security | IAM | IBM Cloud Identity & Access Management |
|  | BYO Bastion Host on VPC VSI | Remote access with Privileged Access Management |
|  | Hyper Protect Crypto Services (HPCS) | Hardware security module (HSM) and Key Management Service |
|  | App ID | Add authentication to web and mobile apps. |
|  | Secrets Manager | Certificate and Secrets Management |
|  | Security and Compliance Center (SCC) | Define policy as code, implement controls for secure data and workload deployments, and assess security and compliance posture. |
| DevOps | Continuous Integration (CI) | 	A pipeline that tests, scans and builds the deployable artifacts from the application repositories. |
|  | Continuous Deployment (CD) | A pipeline that generates all of the evidence and change request summary content. |
|  | Container Registry | Highly available, and scalable private image registry |
| Resiliency | 	VPC VSIs, VPC Block across multiple zones in two regions | Web, app, database high availability and disaster recovery |
| Service Management | IBM Cloud Monitoring | Apps and operational monitoring |
|  | IBM Log Analysis | Apps and operational logs |
|  | Activity Tracker Event Routing | Audit logs |
{: caption="Table 2. Components" caption-side="bottom"}

## Compliance
{: #compliance}

This reference architecture utilizes the Security and Compliance Center (SCC) which defines policy as code, implement controls for secure data and workload deployments, and assess security and compliance posture. For this reference architecture two profiles are used. The **IBM Cloud Framework for Financial Services** and **AI ICT Guardrails**. A profile is a grouping of controls that can be evaluated for compliance.


<!-- ## Next steps
{: #next-steps}

_Optional section._ Include links to your deployment guide or next steps to get started with the architecture.


:exclamation: **Important:** Rename this file `<architecture-name>.md`. For deployable architectures, `<architecture-name>` is the same as the deployable architecture name. -->