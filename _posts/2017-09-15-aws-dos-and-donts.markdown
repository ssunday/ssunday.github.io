---
layout: post
title: "AWS Do's and Don'ts"
description: How to actually use AWS
date: 15/9/2017
categories: ["DevOps", "AWS"]
---

So.

You’re [migrating to the cloud](https://8thlight.com/solutions/cloud-migration-aws/).

Simple, right? Everything is basically the same. You've got a server with an operating system of your choice. Nothing’s really different. Just launch an EC2 instance on AWS, do everything you’ve always done, and **boom**. Done. You’re certifiably *in the cloud*.

Yeah. No. That’s not how it works.

Using EC2 for everything—database, load balancers, Redis, and so on—isn’t using AWS or the cloud effectively. You’re just paying for servers that happen to be hosted by Amazon. By using the most basic AWS cloud offering, you’re limiting your potential and neglecting the power of AWS and the cloud.

By all means, you can work it like that. But it’s not necessarily going to be cost-effective, nor is it the most efficient way of using AWS.

So you may ask, how should I be using AWS, if not in the way described above?

Well, it’s very simple.

**Actually use AWS for all it's worth.**

Some concrete examples:

- **DO:** Use RDS instead of putting a database on an EC2 instance. Amazon tells you to do that themselves!

- **DON'T:** Make your security groups open to the world.
- **DO:** Open only certain ports to certain groups or IP addresses in your security groups.

- **DON'T:** Use a programmatic load balancer when you could use an Elastic Load Balancer.
- **DO:** Use [Amazon Certificate Manager](https://aws.amazon.com/certificate-manager/) to make websites and applications more secure over HTTPS. It’s free! Just put in the domain(s) you want a cert for and Amazon will send a verification email. Click the link and then associate the cert with the Elastic Load Balancer or Elastic Beanstalk stack, among other available AWS services, of your choice, and then you’re good to go.

- **DO:** Enable [CloudWatch alarms](http://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/AlarmThatSendsEmail.html) for your resources.
- **DON'T:** Assume AWS will tell you when things break.

- **DO:** Make backups! (In general). There are a variety of ways to take backups of your resources in AWS. For example, RDS can automatically create snapshots for you, you can manually create EBS snapshots on the web console, and you can schedule EBS snapshots [using Cloudwatch](http://docs.aws.amazon.com/AmazonCloudWatch/latest/events/TakeScheduledSnapshot.html).
- **DO:** Use names for resources! Can you imagine how hard it would be finding something if it isn’t named properly? Don’t imagine it. **Avoid naming things vaguely or not naming them at all**!
- **DON'T:** Rely on IP addresses on servers. If you need a static IP address for a server, assign an [Elastic IP](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html) to it. Otherwise, if you stop and start the server, the IP address will change.

- **DO:** Look into Amazon’s own AMIs for your servers. They aren’t as costly as some other AMIs provided by third parties, and they also come bundled with basic software.
- **DON'T:** Be complacent. AMIs can be taken off the marketplace, and if you want to spin up a copy server, you may have to try another AMI, which might be problematic. Make sure that your AMIs are all still available.
- **DO**: Alternatively, research if making your own AMI is right for your software stack. Instead of installing software to be used by your app every time you spin up an instance, bake it into a custom AMI to save deploy time and to not run into issues with AMIs being taken off the marketplace.

- **DON'T:** Spend time developing deployment scripts for simple applications when you could just use [Elastic Beanstalk](https://aws.amazon.com/elasticbeanstalk/) instead.
- **DO:** If you can't use ElasticBeanstalk, still invest in some form of deployment scripts and configuration management! Yes, you can just copy a server’s data and make a new one, but if you want to scale or be nimble in dealing with outages or whatnot, having a deployment framework in place is essential.
- **DO:** Make your servers disposable. You should be able to spin up new ones and replace old ones within a short period of time. If a server has hardware maintenance at a period of time, and you can’t handle that time frame, you need to be able to adapt and put something else in place.

The list can go on and on and on.

Some of it is just good DevOps practice, which Amazon doesn’t do for you (excluding some aspects of Elastic Beanstalk). Put Continuous Integration in place, document, enable logging and alarms, and have secure applications. That's what you should be doing anyway. AWS doesn't change that.

The rest of it is just being savvy about AWS resources. Comparing cost and choosing which options are best for your business and application. Basically, being a smart consumer. AWS is one super store of options, and not all of them are created equal. Be a discerning buyer. Look at a wide selection of options instead of going to what feels familiar. Different can be an improvement and, importantly, cheaper.

AWS has so much potential to change a business. But it doesn't just come on a silver platter named Elastic Compute Cloud. You have to *work* to integrate it into your app ecosphere. Only then can you really be in the cloud.
