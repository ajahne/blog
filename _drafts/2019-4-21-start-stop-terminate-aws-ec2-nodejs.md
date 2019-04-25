---
layout: single
title:  "Starting, stopping, and terminating AWS EC2 instances with Node.js"
date:   2019-4-21 12:30:00 -0400
categories: javascript
tags: javascript node nodejs aws amazon ec2
header:
  image: assets/images/aws-ec2-nodejs-header.jpg
---
When provisioning and decommissioning Amazon servers in the cloud, we can use the console or we can use code. We're programmers, right? Well let's follow DevOps principles and embrace our coding capabilities to deploy AWS EC2 infrastructure in a scalable way.

Let's build!

**Table of Contents**
- Assumptions (i.e. ensure your environment is setup)
- That code!
  - Start an EC2 Instance
  - Stop an EC2 Instance
  - Terminate an EC2 Instance
- Conclusion
- Additional resources  

## Assumptions before jumping in:
- You have Node.js installed. [Download at the Node.js website](https://nodejs.org/en/).
- You have created a shared credentials file. For more information, see [loading credentials in Node.js](https://docs.aws.amazon.com/sdk-for-javascript/v2/developer-guide/loading-node-credentials-shared.html).
- You have created a key pair.  For details, see [Working with Amazon EC2 Key Pairs](https://docs.aws.amazon.com/sdk-for-javascript/v2/developer-guide/ec2-example-key-pairs.html). You use the name of the key pair in this example.

OK, now that we are all set to start building, let's get to it!

## Install the AWS SDK
```
npm install aws-sdk
```

That was easy! Onward and upward, now the cool parts!

## Creating an AWS EC2 Instance
{% highlight js %}
//load the SDK for JavaScript
const AWS = require('aws-sdk');

//set the region
AWS.config.update({region:'us-west-2'});

//create an ec2 object
const ec2 = new AWS.EC2({apiVersion: '2016-11-15'});

//setup instance params
const params = {
  DryRun: true,
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

Type the following in the command line to run the example
```
node ec2-create-instances.js
```

## Stopping an AWS EC2 Instance
{% highlight js %}
//load the SDK for JavaScript
const AWS = require('aws-sdk');

//set the region
AWS.config.update({region:'us-west-2'});

//create an ec2 object
const ec2 = new AWS.EC2({apiVersion: '2016-11-15'});

//setup instance params
const params = {
  DryRun: true,
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

To run, type
```
node ec2-stop-instances.js
```

## Terminating an AWS EC2 Instance
{% highlight js %}
//load the SDK for JavaScript
const AWS = require('aws-sdk');

//set the region
AWS.config.update({region:'us-west-2'});

//create an ec2 object
const ec2 = new AWS.EC2({apiVersion: '2016-11-15'});

//setup params
const params = {
  DryRun: true,
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

To run, type
```
node ec2-terminate-instances.js
```

## Additional Resources
- [Creating an Amazon EC2 Instance](https://docs.aws.amazon.com/sdk-for-javascript/v2/developer-guide/ec2-example-creating-an-instance.html)
- [EC2 API](https://docs.aws.amazon.com/AWSJavaScriptSDK/latest/AWS/EC2.html)
  - [EC2 Run Instances](https://docs.aws.amazon.com/AWSJavaScriptSDK/latest/AWS/EC2.html#runInstances-property)
  - [EC2 Stop Instances](https://docs.aws.amazon.com/AWSJavaScriptSDK/latest/AWS/EC2.html#stopInstances-property)
  - [EC2 Terminate Instances](https://docs.aws.amazon.com/AWSJavaScriptSDK/latest/AWS/EC2.html#terminateInstances-property)
- [Regions and Availability Zones](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Concepts.RegionsAndAvailabilityZones.html)
- [Ubuntu EC2 AMI Locator](https://cloud-images.ubuntu.com/locator/ec2/)
