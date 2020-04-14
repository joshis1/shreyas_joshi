---
layout: post
title:  "AWS-well-architected-elasticity"
date:   2020-04-14 14:25:31 +1000
categories: Devops
---
This article is all about AWS well architected framework and general concept about elasticity.

There are five pillars of well architected framework.

{% highlight ruby %}
 1. Security
 2. Reliability
 3. Performance efficiency
 4. Operational excellence
 5. Cost optimization
{% endhighlight %}

reference - [AWS-Well-Architected](https://d1.awsstatic.com/whitepapers/architecture/AWS_Well-Architected_Framework.pdf)

**Security - Design Principles**  
Security pillar includes the ability to protect information, systems, and assets while delivering business value through risk assessement and mitigation
stratgies. 

{% highlight ruby %}
1. Implement a strong identity foundation
2. Enable traceability
3. Apply security at all layers
4. Automate security best practices
5. Protect data in transit and at rest.
6. Prepare for security events.
{% endhighlight %}

**Reliability - Design Principles**  
Reliability pillar includes the ability of a system to recover from infrastructure or service disruptions, dynamically acquire computing resources to meet demand, and mitigate disruptions, such as misconfigurations or transient network issues.

{% highlight ruby %}
1. Test recovery procedures
2. Automatically recover from failure
3. Scale horizontally to increase aggregate system availability
4. Stop guessing capacity
5. manage change in automation
{% endhighlight %}

**Performance Efficiency - Design Principles**  
Performance efficiency pillar includes the ability to use
computing resources efficiently to meet system requirements and to maintain that efficiency as demand changes and technology evolve.
{% highlight ruby %}
1. Democratize advanced technologies
2. go global in minutes
3. use serverless architecture
4. experiment more often
5. mechanical sympathy
{% endhighlight %}

**Operational Excellence - Design Principles**  
The operational excellence pillar includes the ability to run and monitor systems to deliver business value and to continually improve supporting processes and procedures.
{% highlight ruby %}
1. Perform operations as code
2. Annotate documentation
3. Make frequent, small, reversible changes.
4. Refine operations procedures frequently
5. Anticipate failure
6. Learn from all operational features.
{% endhighlight %}

**Cost optimization - Design Principles**  
The cost optimization pillar includes the ability to avoid
or eliminate uneeded cost or sub optional resources.
{% highlight ruby %}
1. Adopt a consumption model.
2. Measure overall efficiency.
3. Stop spending money on data center operations.
4. Analyze and attribute expenditure.
5. Use managed services to reduce cost of ownership.
{% endhighlight %}

**Elasticity**  
It is also known as automated horizontal scaling. The elastic scaling is where automation and horizontal scaling are used in conjunction to match capacity with demand. Demand is rarely so linear - it can increase or decrease often in a rapid and sudden way. An efficient platform should scale OUT and IN matching demands on that system. It allows performance efficiency and cost optimization.

This brings an end to this article.