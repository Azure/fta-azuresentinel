# Pre-requisites

During this part of the session you will taught:

## SIEM Decision Points

* Use Cases
* Role Based Access Control (RBAC)
* Log Analytics decisions
* Data Sources

The reason we cover this is because you, as the security interest team, need to make these decisions in order to effectively incept, configure and use Sentinel as a tool in your environment for your security operations.

At the end of this topic you will be able to accurately describe the need for Use Cases, how you want to establish your Log Analytics deployment, what permissions (RBAC) you need to have in order to use the tool and which data sources you want to connect and the considerations around those (Syslog/CEF forwarders etc).

### Use Cases

As part of our [Azure Sentinel DevOps](https://techcommunity.microsoft.com/t5/azure-sentinel/accelerate-your-azure-sentinel-deployment-with-this-azure-devops/ba-p/1449414) guidance the first section we deal with is defining your use cases. This is important as you move to the cloud, things have changed and are much more dynamic but also amplified by new pillars of threats you are now being exposed to, highlighted below.

**Examples of the new security pillars (not an exhaustive list)**:

| **Potential Use Cases / Attacks** |   |   |   | |
| --- | --- | --- | --- | --- |
| **Tenant Level** | **Subscription Level** | **IaaS** | **PaaS** | **SaaS** |
| Use elevated tenant admin | External account added to subscription | Known hacker/malicious tool/process found | Malicious Key Vault access - keys enumerated | A potentially malicious URL click was detected |
| MFA settings changed | Stale account with access to subscription | Account Password Hash Accessed | Anonymous storage access | Unusual volume of external file sharing |
|   | Attack detection service not configured (ie ASC) | Antimalware disabled | activity from unfamiliar location | Password spray attack |
|   |   | Brute force detected | SQL injection detected |   |
|   |   | Communications with malicious IP | Authentications disabled for App/Web services |   |
|   |   | TOR IP detected |   |   |
|   |   | File less attack technique detected |   |   |
|   |   | DDOS detected |   |   |

[Gartner Research](https://www.gartner.com/en/documents/3950486/how-to-build-security-use-cases-for-your-siem) talk about use cases requiring three things, that they call the "Use Case Triangle". A simple methodology aimed at the following:

**Insight** - examples are the things you're looking to find, like User or Asset behavior.

**Data** - examples are Events and Logs, things you see in your environment.

**Analytics** - this seems simple, *"build rules"* BUT it's not just aimed there. Think about pattern matching or machine learning. Big picture things.

These use cases are important, you need to understand what Insight you're trying to gain with your SIEM, making sure you have the right Data for that Insight and then that you're applying the right Analytics for that Insight.

Having the right uses cases, and making the decisions about the associated data and analytics makes it easier to ensure you're covering all the things you need to cover in your environment. They should reduced the *noise* and allow your analysts to focus on what is important in your environment.

The final point is that they must have a lifecycle, like any methodology in 2020. Plan, Deploy, **Measure Performance**, Tune (if required), Retire and Archive. Threats aren't static and your Security Operations shouldn't be either.

### Log Analytics

You'll see, as soon as you open Azure Sentinel, the first thing you need to do is to select a Log Analytics workspace you want to use. We have a multitude of resources to help you make decisions around Azure Sentinel deployments:

[Best Practices White Paper](https://www.microsoft.com/security/blog/wp-content/uploads/2020/07/Azure-Sentinel-whitepaper.pdf)

[Tech Community Blog](https://techcommunity.microsoft.com/t5/azure-sentinel/best-practices-for-designing-an-azure-sentinel-or-azure-security/ba-p/832574)

[Extend Azure Sentinel across workspaces and tenants](https://docs.microsoft.com/en-us/azure/sentinel/extend-sentinel-across-workspaces-tenants)

The point is, with all of these documents, you need to make decisions about how you're going to configure your Log Analytics workspaces. Our guiding recommended best practice is to have a single workspace, where possible, for the full benefit of the tool. However we understand that there will be issues like data sovereignty and regulatory compliance that will impact these decisions, even billing and cost decisions can impact it.

Whatever the case is you need to make the decision. Centralize as much as possible, having your data going to one location, rather than each team maintaining their own repository, will allow your Security team to start ingesting the data and building patterns while reducing the time it takes for them to find them.