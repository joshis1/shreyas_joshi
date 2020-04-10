---
layout: post
title:  "AWS-Service-Model-Brief"
date:   2020-04-10 16:23:31 +1300
categories: Devops
---
This article is all about starting with AWS and getting to know about AWS Service model.

It is advised that you always used multifactor authentication for security reasons. You could use 
google authenticator app for that purpose.

(https://play.google.com/store/apps/details?id=com.google.android.apps.authenticator2&hl=en_AU)

Next, sign into the AWS console. 

**Setup Alarm for billing**

It is advised that you check the billing alerts like
receive billing alertss, receive free tier usage alerts through email. In order to setup the alarm, choose the service - Cloud watch. In cloud watch service, create alarm and select metric. Some metrics are available only in US East (N. Virginia). So, I will suggest to use that region. After selecting the metric, tell above what cost, AWS should notify you.
I have selected 10 USD. But, you could enter any value you wish. This comes under SNS topic i.e. Simple Notification services. Next, view the alarm. Billing in AWS is on demand. 

**How to navigate to the main page?**

Click AWS logo to navigate to the main page.

**Tools to explore cost services**
There are tools to allow to explore cost services.

**Access Management basics**

Principal - a person or application that can make
an authenticated or anonymous request to perform an
action on a system.

Anonymous request - without login.

Authentication - Authenticating a principal against
an identity. This could via username and password.
Or this could be via API keys.

Identity - Objects that require authentication and
are authorized to access resources.

Authorization - The process of checking and allowing
or denying access to a resource fo ran identity.

**Shared responsibility/security model**
The shared responsibility is divided broadly into
two categories.

1) Customer responsibility - like security in the 
cloud, customer data, platform, application, IAM,
operating system, network and firewall configuration,
encryption, network protection.

2) AWS responsibility - security of the cloud, 
software, compute, storage, database, network,
hardware/aws global infrastructure, regions,
availability zones, edge locations.

Note, AWS doesn't manage inside the cloud.
Customer responsibility is to manage inside the cloud.
AWS is the provider of the cloud.

**Service Models**
{% highlight ruby %}
IaaS - Infrastructure as a service
PaaS - Platform as a service
SaaS - Software as a service
FaaS - Function as a service.

{% endhighlight %}

**System stack**

{% highlight ruby %}
Data
Runtime application 
Operating System 
Virtualisation 
Host/Servers 
Network and Storage 
Data Center 

{% endhighlight %}

Run-time application can be python, java, etc.

The shared responsibility depends on the service
model.

ECS- IaaS - Os, Run-time, application, data.
In IaaS service model, user shares the maximum 
responsibility. However, we get maximum flexibility.

PaaS - Only Data and application is managed by the 
user. E.g. nodejs - data and application
PaaS is used by developers.

SaaS - only Data is managed by the user. Example,
Netflix. This has low maintenance cost since everything is managed by AWS. Another example, is
office 365.

FaaS - This is actually like PaaS - e.g. 
AWS lambda - it provides single function. The
bill comes only when that function is executed.

The service model matters a lot since this impacts
the cost to the company. 

This brings an end to this article.