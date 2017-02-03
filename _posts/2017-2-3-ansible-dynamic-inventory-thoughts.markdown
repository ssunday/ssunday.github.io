---
layout: post
title: Ansible Dynamic Inventory Thoughts
description: My experience and feelings
date: 3/2/2017
categories: ["DevOps", "Ansible"]
---

My DevOps experience is varied but limited. I've done some Chef, packer, and now Ansible. The latter of which is my most recent dive into scripting deployments and probably the most enjoyable.

What Ansible was being used for in my case was to:

1. Deploy Infrastructure Stack onto AWS. In this case, a single EC2 instance with an Elastic IP address and an RDS.
2. Deploy an application that communicates with that database onto the server and properly get it running.

No, Ansible was not strictly used for the creation of the stack, though that was a possiblility. Cloudformation templates were created using [Troposphere](https://github.com/cloudtools/troposphere) and then executed through Ansible. I didn't touch most of this process, so I can't speak on its extreme details.

But I can talk about the communication process between AWS and the script for deploying the application. Typically, with Ansible, you specify a inventory file that basically holds the information concerning the end-points for where the deployment is targeted against. That's all well and good if nothing ever changes or if the stack already exists.

But in this case, we were creating a stack then running another script to set-up the application. We could have manually modified the inventory with the newly-generated end points and hosts, but that's more than kind of horrible. This is software. There is a tool for this issue somewhere.

For Ansible, that tool/concept is *[Dynamic Inventory]*(http://docs.ansible.com/ansible/intro_dynamic_inventory.html). The AWS EC2 one listed on the Ansible Docs is the one I used for this deployment.

Basically, how it works is by using the currently configured AWS Profile (I set up a specific profile and ran the command using it), and gets information about the AWS account. Like running servers, RDS instances, Route 53 configuration, and so on. It returns it as a JSON dump of the information that can be accessed through a Playbook, granted you've loaded in the dynamic inventory file when you execute the playbook.

Now, using that information to make a deployment script target a specific server requires leveraging the information returned by the Dynamic Inventory script. So this information is returned in key/value pairs. Values being either metadata or, more importantly, the end-point of the instance. The keys can be the name, the host, or, the most valuable in my experience, *tag names.* If you have worked with AWS in the past, you can assign tags to basically anything. This is where that comes in handy.

Say you tag a server name as `app-staging`. Using that you can refer to the host in the Ansible playbook as `tag_Name_app_staging`. Then the dynamic inventory will use that to determine the end point for the script. I used the `host_vars/` directory to store these host tag names for each environment (staging, production, etc) and dynamically loaded the particular file in by passing the `env` in as an extra var on the command line.

I liked this approach as I was looking for a way to conditionally deploy staging/production environment without having to write some new playbook or anything that complex. With an extra var, it is basically the same as a `RAILS_ENV` or something. The sheer power of it coupled with Dynamic Inventory basically allows me to deploy any environment without touching anything. It's fabulous. Truly simplified deployment.

I really recommend Ansible after this experience. It is such a flexible system with great community support backing it. If I had to start a deployment from scratch, I'd probably choose Ansible.
