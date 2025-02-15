---

title: Plan reports & monitoring deployment
description: Describes how to plan and execute implementation of reporting and monitoring.
services: active-directory
author: gargi-sinha
manager: martinco
ms.service: active-directory
ms.topic: conceptual
ms.workload: identity
ms.subservice: report-monitor
ms.date: 01/20/2023
ms.author: sarahlipsey
ms.reviewer: plenzke 
# Customer intent: For an Azure AD administrator to monitor logs and report on access 
ms.collection: M365-identity-device-management
---

# Azure Active Directory reporting and monitoring deployment dependencies

Your Azure Active Directory (Azure AD) reporting and monitoring solution depends on legal, security, operational requirements, and your environment's processes. Use the following sections to learn about design options and deployment strategy.

## Benefits of Azure AD reporting and monitoring

Azure AD reporting has a view, and logs, of Azure AD activity in your environment: sign-in and audit events, also changes to your directory.

Use data output to:

* determine how your apps and services are used.
* detect potential risks affecting the health of your environment.
* troubleshoot issues preventing your users from getting their work done.
* gain insights by seeing audit events of changes to your Azure AD directory.

Azure AD monitoring enables you to route your logs generated by Azure AD reporting to different target systems. You can then either retain it for long-term use or integrate it with third-party Security Information and Event Management (SIEM) tools to gain insights into your environment.

With Azure AD monitoring, you can route logs to:

* an Azure storage account for archival purposes.
* Azure Monitor logs, where you can analyze the data, create dashboards, and alert on specific events.
* an Azure event hub where you can integrate with your existing SIEM tools such as Splunk, Sumologic, or QRadar.

### Prerequisites

You'll need an Azure AD premium license to access the Azure AD sign-in logs.

For detailed feature and licensing information, see the [Azure Active Directory pricing guide](https://www.microsoft.com/security/business/identity-access-management/azure-ad-pricing).

To deploy Azure AD monitoring and reporting you'll need a user who is a Global Administrator or Security Administrator for the Azure AD tenant.

* [Azure Monitor data platform](../../azure-monitor/data-platform.md)
* [Azure Monitor naming and terminology changes](../../azure-monitor/terminology.md)
* [How long does Azure AD store reporting data?](./reference-reports-data-retention.md)
* An Azure storage account that you have `ListKeys` permissions for. We recommend that you use a general storage account and not a Blob storage account. For storage pricing information, see the [Azure Storage pricing calculator](https://azure.microsoft.com/pricing/calculator/?service=storage).
* An Azure Event Hubs namespace to integrate with third-party SIEM solutions.
* An Azure Log Analytics workspace to send logs to Azure Monitor logs.

## Plan and deploy an Azure AD reporting and monitoring deployment project

Reporting and monitoring are used to meet your business requirements, gain insights into usage patterns, and increase your organization's security posture. In this project, you'll define the audiences that will consume and monitor reports, and define your Azure AD monitoring architecture.

## Stakeholders, communications, and documentation

When technology projects fail, they typically do so due to mismatched expectations on effect, outcomes, and responsibilities. To avoid these pitfalls, [ensure that you're engaging the right stakeholders](../fundamentals/active-directory-deployment-plans.md). Also ensure that stakeholder roles in the project are well understood by documenting the stakeholders and their project input and responsibilities.

Stakeholders need to access Azure AD logs to gain operational insights. Likely users include security team members, internal or external auditors, and the identity and access management operations team.

Azure AD roles enable you to delegate the ability to configure and view Azure AD Reports based on your role. Identify who in your organization needs permission to read Azure AD reports and what role would be appropriate for them. 

The following roles can read Azure AD reports:

* Global Administrator
* Security Administrator
* Security Reader
* Reports Reader

Learn More About [Azure AD Administrative Roles](../roles/permissions-reference.md). Always apply the concept of least privileges to reduce the risk of an account compromise. Consider implementing [Privileged Identity Management](../privileged-identity-management/pim-configure.md) to further secure your organization.

### Engage stakeholders

Successful projects align expectations, outcomes, and responsibilities. See, [Azure Active Directory deployment plans](../fundamentals/active-directory-deployment-plans.md). Document and communicate stakeholder roles that require input and accountability.

### Communications plan

Tell your users when, and how, their experience will change. Provide contact information for support.

* What, if any, SIEM tools you're using.
* Your Azure infrastructure, including existing storage accounts and monitoring being used.
* Your organizational retention policies for logs, including any applicable compliance frameworks required. 

### Business use cases

To better prioritize the use cases and solutions, organize the options by "required for solution to meet business needs," "nice to have to meet business needs," and "not applicable."

### Considerations

* **Retention** - Log retention: store audit logs and sign in logs of Azure AD longer than 30 days
* **Analytics** - Logs are searchable with analytic tools
* **Operational and security insights** - Provide access to application usage, sign-in errors, self-service usage, trends, etc.
* **SIEM integration** - Integrate and stream Azure AD sign-in logs and audit logs to SIEM systems

### Monitoring solution architecture

With Azure AD monitoring, you can route Azure AD activity logs and retain them for long-term reporting and analysis to gain environment insights, and integrate it with SIEM tools. Use the following decision flow chart to help select an architecture.

   ![Decision matrix for business-need architecture.](media/reporting-deployment-plan/deploy-reporting-flow-diagram.png)

#### Archive logs in a storage account

You can keep logs longer than the default retention period by routing them to an Azure storage account.

   > [!IMPORTANT]
   > Use this archival method if there is no need to integrate logs with a SIEM system, or no need for ongoing queries and analysis. You can use on-demand searches.

Learn more:

* [How long does Azure AD store reporting data?](./reference-reports-data-retention.md)
* [Tutorial: Archive Azure AD logs to an Azure storage account](./quickstart-azure-monitor-route-logs-to-storage-account.md)

#### Stream logs to storage and SIEM tools

* [Integrate Azure AD logs with Azure Monitor logs](./howto-integrate-activity-logs-with-log-analytics.md).
* [Analyze Azure AD activity logs with Azure Monitor logs](../reports-monitoring/howto-analyze-activity-logs-log-analytics.md).
* Learn how to [stream logs to an event hub](./tutorial-azure-monitor-stream-logs-to-event-hub.md).
* Learn how to [Archive Azure AD logs to an Azure Storage account](./quickstart-azure-monitor-route-logs-to-storage-account.md).
* [Integrate Azure AD logs with Splunk by using Azure Monitor](./howto-integrate-activity-logs-with-splunk.md)
* [Integrate Azure AD logs with SumoLogic by using Azure Monitor](./howto-integrate-activity-logs-with-sumologic.md)

## Next steps

- Consider implementing [Privileged Identity Management](../privileged-identity-management/pim-configure.md) 
- Consider implementing [Azure role-based access control](../../role-based-access-control/overview.md)
- [Learn more about report retention policies](./reference-reports-data-retention.md).
- [Analyze Azure AD activity logs with Azure Monitor logs](./howto-analyze-activity-logs-log-analytics.md)

