---
layout: post
title: "Ansible and AWS: Painless Deployment"
description: AWS/Ansible working together for the good of the world
date: 14/3/2017
categories: ["DevOps", "Ansible"]
---

[Ansible](https://www.ansible.com/) is a fantastic way to orchestrate deployments that aren't exactly trivial. In a complex deployment, there are dozens of players and they all need to act at a specific moment. It is no wonder then that Ansible calls the deployment scripts `playbooks`.

It makes it sound so artistic. You are specifying what roles to play on what hosts, sequencing in a proper fashion and then at the end of that journey, tada! Your system is (hopefully) up and running as you want it.

And sometimes that system will be running on [Amazon Web Services (AWS)](https://aws.amazon.com/).

And sometimes you want your infrastructure deployment process also scripted in Ansible. There are a few ways to go about doing this.

The simplest way to do this is through Ansible itself. Ansible comes with the [EC2 Module](http://docs.ansible.com/ansible/ec2_module.html), which allows you to deploy to an AWS account. The access/secret keys can be configured through profiles/[Boto](https://aws.amazon.com/sdk-for-python/) or in the task itself (please do the latter). Having that configured, you can have a task that *literally spins up an EC2 Instance*. It can look something like this:

{% raw  %}
```YAML
- ec2:
  key_name: "{{ app_key }}"
  group: server
  instance_type: "{{ ec2_instance_type }}"
  region: "{{ ec2_aws_region }}"
  group: "{{ security_group_id }}"
  image: "{{ amazon_ami }}"
  wait: yes
  wait_timeout: 500
  instance_tags:
    name: {{ app_name }}-server
  monitoring: yes
  volumes:
    - device_name: /dev/sda1
      volume_size: "{{ ebs_volume_size }}"
      delete_on_termination: true
  vpc_subnet_id: "{{ vpc_submit_id }}"
  assign_public_ip: yes
```
{% endraw  %}

So that's one way to do it.

Another way, for more complicated deployments, is using [Troposphere](https://github.com/cloudtools/troposphere) templates as Ansible templates. Troposphere makes [AWS Cloudformation](https://aws.amazon.com/cloudformation/) stacks. I would pepper this blog posts with examples, but the Troposphere repository I previously linked has some fantastic examples that are quite complex and descriptive.

I recommend Troposphere for creating highly customizable and extensive templates for AWS infrastructure deployment. The Ansible modules can get you the basics, but, for configuring nearly all aspects of a stack in a template, Troposphere wins.

So either using Ansible's modules or Troposphere templates, you create your AWS stack. Congratulations! You can now spin up servers/databases with a single command/playbook.

But now you need to deploy to these servers in a completely separate playbook. This poses a mild conundrum. Ansible comes with the basic assumption that the servers being deployed have the same end-point. The hosts are not going to be the same every time. Traditionally, you specify the IP or DNS endpoints for a particular host in the inventory file...but that's not going to work. Unless you want to edit the inventory every time you do another AWS deploy. I really don't know why you would want to. An easy solution exists.

And that solution is [Ansible Dynamic Inventory](http://docs.ansible.com/ansible/intro_dynamic_inventory.html).

With Dynamic Inventory set up, you can access a variety of information about your AWS account's instances and databases. This is traditionally used for pulling in the correct host to deploy to based on something tagged on the server. To do this, you'll need some basic information about the instances you are deploying to—as in their tag names or any 'metadata' related to the EC2 Instances. This is where AWS tags really come in handy.

If you want to deploy to a server named `app`, you could define the host like this:

```YAML
hosts: tag_Name_app
```

And that will run the playbook on the EC2 Instance that has a `Name` tag (a tag with a key of `Name`) set with a value of `app`.

This also works if you have a few servers deployed under the same AWS CloudFormation stack. You use the AWS CloudFormation Stack name as the host and it will deploy to all servers under that stack.

It looks ugly, but it gets the job done:

```YAML
host_name: tag_aws_cloudformation_stack_name_app_server
```

To actually access these resources, you'll have to configure a default AWS Profile for Boto to use. This can be done in the Dynamic Inventory settings file. Or you could use whatever one you want by prefixing every playbook command with `AWS_PROFILE=your-profile`. Otherwise, the default AWS profile will be used, which might not be right. Tip: Don't actually have a default AWS profile (i.e put in dummy credentials) so you'll never accidentally deploy to someone else's account.

Whichever way you set up  your AWS profile, you will be able to access your AWS resources through your Ansible playbooks. So when all this is settled, you should be able to:

- Deploy to AWS using Ansible scripts
- Deploy to newly created AWS resources without modifying any files

Basically, you can potentially launch your app with 1-2 Ansible commands, depending on how you set up your playbooks.

Welcome to the world of infrastructure as code and scripted deployment!
