---
layout: single
title:  "Launch, Stop, and Terminate AWS EC2 Instances with Node.js"
date:   2019-6-16 11:53:00 -04:00
categories: javascript
tags: javascript node nodejs aws amazon ec2
header:
  image: assets/images/aws-ec2-nodejs-header.jpg
---
When provisioning and decommissioning Amazon servers in the cloud, we can use the console or we can use code. We're programmers, right? Well let's follow DevOps principles and embrace our coding capabilities to deploy [AWS EC2 infrastructure](https://aws.amazon.com/ec2/) in a scalable way.

Let's build!

**Table of Contents:**
- [Assumptions (aka ensuring you have everything you need)](#assumptions-before-jumping-in)
- That code!
  - [Install the AWS SDK](#install-the-aws-sdk)
  - [Launch an EC2 Instance](#creating-an-aws-ec2-instance)
  - [Stop an EC2 Instance](#stopping-an-aws-ec2-instance)
  - [Terminate an EC2 Instance](#terminating-an-aws-ec2-instance)
- [Conclusion](#conclusion)
- [Additional resources](#additional-resources)

## Assumptions before jumping in:
- You have Node.js installed. [Download at the Node.js website](https://nodejs.org/en/).
- You have created a shared credentials file. For more information, see [loading credentials in Node.js](https://docs.aws.amazon.com/sdk-for-javascript/v2/developer-guide/loading-node-credentials-shared.html).
- You have created a key pair.  For details, see [working with Amazon EC2 Key Pairs](https://docs.aws.amazon.com/sdk-for-javascript/v2/developer-guide/ec2-example-key-pairs.html). You use the name of the key pair in this example.
- You have the `ImageId` of the AMI you want to launch. For details, see [getting an AMI ID]({{ site.baseurl }}{% post_url 2019-5-15-getting-an-ami-id-nodejs %}). You will use the `ImageId` in this example.
- You have the `SubnetId` for the subnet you want to launch the instance into. Check out [this article on listing aws subnets]({{ site.baseurl }}{% post_url 2019-5-28-list-aws-subnets-nodejs %}) for more information. You will need a `SubnetId` to proceed.

OK, now that we are all set to start building, let's get to it!

## Install the AWS SDK
```
npm install aws-sdk
```

That was easy! Onward and upward, now the cool parts!

## Creating an AWS EC2 Instance
First let's  deploy (i.e. create) an EC2 instance.  Here is the full block of code that will get you there!
{% highlight js %}
//load the SDK for JavaScript
const AWS = require('aws-sdk');

//set the region
AWS.config.update({region:'us-west-2'});

//create an ec2 object
const ec2 = new AWS.EC2({apiVersion: '2016-11-15'});

//setup instance params
const params = {
  ImageId: 'ami-#####',
  InstanceType: 't2.micro',
  KeyName: 'My-Key-Pair',
  MinCount: 1,
  MaxCount: 1,
  SubnetId: 'subnet-#####',
  TagSpecifications: [
    {
      ResourceType: "instance",
      Tags: [
        {
          Key: "Name",
          Value: "Node SDK EC2 Creation"
        }
      ]
    }
  ]
};

ec2.runInstances(params, function(err, data) {
  if (err) {
    console.log(err, err.stack); // an error occurred
  } else {
    console.log(data);           // successful response
  }  
});

{% endhighlight %}

OK, let's take a moment to break down some of what we are doing.  I will cut the code into chunks and explain each section. Starting from the top...

{% highlight js %}
//load the SDK for JavaScript
const AWS = require('aws-sdk');

//set the region
AWS.config.update({region:'us-west-2'});

//create an ec2 object
const ec2 = new AWS.EC2({apiVersion: '2016-11-15'});
{% endhighlight %}

First is the setup. What we initially do is load the amazon sdk i.e. `aws-sdk`. Next we set our region. As you probably know, there is a wide array of [AWS regions](https://docs.aws.amazon.com/general/latest/gr/rande.html). I chose the west coast (Oregon), but there are numerous regions you can choose from.  We also create a new `ec2` service object which we utilize later in the code. Cool? Cool!

Next we setup the instance parameters. This is information specific to our EC2 instance(s).

_Note: The `ImageId` and `SubnetId` are placeholders. These values are the ones you obtained from [here]({{ site.baseurl }}{% post_url 2019-5-15-getting-an-ami-id-nodejs %}) and [here]({{ site.baseurl }}{% post_url 2019-5-28-list-aws-subnets-nodejs %})._

{% highlight js %}
//setup instance params
const params = {
  ImageId: 'ami-#####',
  InstanceType: 't2.micro',
  KeyName: 'My-Key-Pair',
  MinCount: 1,
  MaxCount: 1,
  SubnetId: 'subnet-#####',
  TagSpecifications: [
    {
      ResourceType: "instance",
      Tags: [
        {
          Key: "Name",
          Value: "Node SDK EC2 Creation"
        }
      ]
    }
  ]
};
{% endhighlight %}

There are a few things I'd like to point out here. First is the `ImageId`, this is a unique identifier that is particular to the region that you can obtain from AWS, which specifies the [server instance you want to use]({{ site.baseurl }}{% post_url 2019-4-30-finding-a-linux-ami-with-nodejs %}). Second is the instance type. As we are targeting "free-tier" this is set to `t2.micro`.

_Note: be sure to check your region and setup to ensure you are using free-tier. Do **not** send your bills here!_

The `KeyName` is the [key pair you have setup](https://docs.aws.amazon.com/sdk-for-javascript/v2/developer-guide/ec2-example-key-pairs.html).

`MinCount` is the minimum number of instances to launch, while `MaxCount` is (yup, you guessed it) the maximum number of servers to launch. Both of these must be set to 1 or greater. For more details, go [here](https://aws.amazon.com/ec2/faqs/#How_many_instances_can_I_run_in_Amazon_EC2).

I am also [setting the ID]({{ site.baseurl }}{% post_url 2019-5-28-list-aws-subnets-nodejs %}) of the [subnet](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Subnets.html) to launch the instance into.

You will notice I added the `TagSpecifications` to set a tag, which lets me know I created this instance via code. I find this helpful when checking that my code worked!  

Finally, I deploy the instance by calling `runInstances` with the specified `params` and pass in a callback function to handle the response.
{% highlight js %}
ec2.runInstances(params, function(err, data) {
  if (err) {
    console.log(err, err.stack); // an error occurred
  } else {
    console.log(data);           // successful response
  }  
});
{% endhighlight %}


_Do note that you can also utilize promises as well instead of callbacks, as seen [here](https://docs.aws.amazon.com/sdk-for-javascript/v2/developer-guide/ec2-example-creating-an-instance.html). My examples follow the standard callback syntax utilized in the AWS API documentation_.

Now that all the details are outlined, let's launch! Type the following in the command line to run the example:
```
node ec2-create-instances.js
```

This will output a lot of information from the creation of this instance.  To continue on and stop (then terminate) this instance, **be sure to grab the `InstanceId` of the EC2 server we just created!**

## Stopping an AWS EC2 Instance
Great, so we started an instance, now what? Well, one thing we can do is stop said instance (or instances).  As you can see, most of the code is similar to deploying an instance.

{% highlight js %}
//load the SDK for JavaScript
const AWS = require('aws-sdk');

//set the region
AWS.config.update({region:'us-west-2'});

//create an ec2 object
const ec2 = new AWS.EC2({apiVersion: '2016-11-15'});

//setup instance params
const params = {
  InstanceIds: [
    'i-#####'    
  ]
};

ec2.stopInstances(params, function(err, data) {
  if (err) {
    console.log(err, err.stack); // an error occurred
  } else {
    console.log(data);           // successful response
  }  
});
{% endhighlight %}

The key difference (outside of the call to `stopInstances`) is the `params` object, which takes an array of `InstanceIds` to stop.  So, to stop the instance we started, we must add the `InstanceId` into the `params` object.

Once you have entered the instance id, type the following to stop the instance:
```
node ec2-stop-instances.js
```

Boom, instance stopped!

## Terminating an AWS EC2 Instance
So, we stopped the instance, we are done, right? Well, not quite.  Starting an instance provisions our server, but the server is still there when stopped. To fully decommission, we need to terminate the instance.

{% highlight js %}
//load the SDK for JavaScript
const AWS = require('aws-sdk');

//set the region
AWS.config.update({region:'us-west-2'});

//create an ec2 object
const ec2 = new AWS.EC2({apiVersion: '2016-11-15'});

//setup params
const params = {
  InstanceIds: [
    'i-#####'    
  ]
};

ec2.terminateInstances(params, function(err, data) {
  if (err) {
    console.log(err, err.stack); // an error occurred
  } else {
    console.log(data);           // successful response
  }  
});
{% endhighlight %}

As you can see, most of this code is pretty similar to our previous examples and astute readers are already figuring ways to [refactor the code]({{ site.baseurl }}{% post_url 2019-3-29-refactoring-by-martin-fowler-chapter-notes%}) to make it more maintainable, economic, and efficient.

Similar to when we stop the instance, we add the target instance id to the params object.

Once we are ready to terminate, we type the following:
```
node ec2-terminate-instances.js
```

And just like that, we have destroyed our instance.

## Conclusion
In this article, we have utilized Node.js to start, stop, and terminate Amazon EC2 instances. We are now _that much_ closer to automating the deployment of our servers, versioning our infrastructure, embracing DevOps principles, and leveraging IAC to scale and  [accelerate](https://www.amazon.com/Accelerate-Software-Performing-Technology-Organizations/dp/1942788339) our organization. Ain't no stopping us, let's keep pushing!

Check out the additional resources below and happy coding!

## Additional Resources
- [Creating an Amazon EC2 Instance](https://docs.aws.amazon.com/sdk-for-javascript/v2/developer-guide/ec2-example-creating-an-instance.html)
- [EC2 API](https://docs.aws.amazon.com/AWSJavaScriptSDK/latest/AWS/EC2.html)
  - [EC2 Run Instances](https://docs.aws.amazon.com/AWSJavaScriptSDK/latest/AWS/EC2.html#runInstances-property)
  - [EC2 Stop Instances](https://docs.aws.amazon.com/AWSJavaScriptSDK/latest/AWS/EC2.html#stopInstances-property)
  - [EC2 Terminate Instances](https://docs.aws.amazon.com/AWSJavaScriptSDK/latest/AWS/EC2.html#terminateInstances-property)
- [Regions and Availability Zones](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Concepts.RegionsAndAvailabilityZones.html)
- [Ubuntu EC2 AMI Locator](https://cloud-images.ubuntu.com/locator/ec2/)
