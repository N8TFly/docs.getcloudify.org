+++
title = "Cloudify Premium Trial"
description = "Installing the Cloudify trial manager"
weight = 10
alwaysopen = false
+++

{{%children style="h2" description="true"%}}

 Cloudify Premium Trial provides a fully functional Premium manager as a Docker container image. This page describes the complete setup flow to get an activated Cloudify trial manager.

## Step 1: Install the Cloudify Manager as a Docker container

The easiest way to deploy Cloudify trial manager is as a Docker container. This tutorial assumes that you have [Docker](https://docs.docker.com/install) installed on a local or a remote machine.

Open your terminal and create/start the Docker container (requires password)
```
sudo docker run --name cfy_manager_local -d --restart unless-stopped -v /sys/fs/cgroup:/sys/fs/cgroup:ro --tmpfs /run --tmpfs /run/lock --security-opt seccomp:unconfined --cap-add SYS_ADMIN -p 80:80 -p 8000:8000 cloudifyplatform/premium-cloudify-manager-aio:latest
```

Verify that your manager is running by browsing to [localhost](http://localhost) when running locally, or to the hosting machine IP when the Docker server is remote, the Cloudify login page should be displayed.

![login-page.png]( /images/ui/login/login-page.png )



## Step 2: Activate your Trial

A Cloudify license is provided to all Cloudify Premium subscribed customers by Cloudify support. Cloudify Premium trial customers receive their trial license via email upon trial request. Request your free 60 day trial at https://cloudify.co/download/#trial.  
To activate your Cloudify manager submit your license through either the Cloudify management console (UI) or via the Cloudify CLI.
Cloudify allows for multiple user interfaces; in this tutorial we will demonstrate the usage of the Cloudify management console (web UI) and the Cloudify command line (cfy). The following steps demonstrate both approaches.  

#### Activating Cloudify using the UI

1. Go to localhost in your browser to see the Cloudify UI. Login and password are both _admin_.
1. Submit your Cloudify subscription/trial key. Learn more [here](https://docs.cloudify.co/latest/install_maintain/installation/manager-license/#product-activation).

#### Activating Cloudify using the CLI

Save the Cloudify subscription/trial file you received to a local folder.
Copy the subscription file to the container by running:

```
docker cp <file path on local system> cfy_manager_local:/tmp/license.yaml
```

e.g. docker cp C:\Users\John\Downloads\my-license.yaml docker-cfy-manager:/tmp/

Apply the license by running:

```
docker exec -it cfy_manager_local sh -c "cfy license upload /tmp/license.yaml"
```


___



#### Congratulations! you now have your Cloudify manager ready.

What's next?
Go ahead and examine our example based tutorials to learn about Cloudify basics:

* [Level 1: Infra Provisioning Basics]({{< relref "trial_getting_started/examples/basic/_index.md" >}}) - Learn how to setup basic infrastructure in AWS, Azure, GCP, and Openstack.
* [Level 2: Setup Your First Service]({{< relref "trial_getting_started/examples/first_service/_index.md" >}}) - Learn how to setup a simple service topology consisting of a simple web service , and application running on a VM. These examples also explain the setup of all essential peripherals (Security group, network interfaces, etc.) in AWS, Azure, GCP, and Openstack.
* [Level 3: Use Automation Tools]({{< relref "trial_getting_started/examples/automation_tools/_index.md" >}}) - Learn how to create infrastructure objects and services through orchestration of orchestrators and automation tools such as AWS CloudFormation, Azure ARM, and Terraform.
* [Level 4: Multi-Cloud Orchestration]({{< relref "trial_getting_started/examples/multi_cloud/_index.md" >}}) - Learn how to design your service topology such that it is abstracted from the infrastructure layer and can be deployed on any infra using a single, flexible template.






By downloading Cloudify, you agree to the [End User License Agreement](https://cloudify.co/license). Cloudify is available for a 60-day evaluation period.

Read about the differences between our [Cloudify versions](https://cloudify.co/product/community-enterprise-editions).