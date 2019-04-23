---
layout: single
title:  "Starting, stopping, and terminating AWS EC2 instances with Node.js"
date:   2019-4-21 12:30:00 -0400
categories: javascript
tags: javascript node nodejs aws amazon ec2
header:
  image: assets/images/aws-ec2-nodejs-header.jpg
---

Outline
- purpose of this post
- Assumptions
- Examples
  - start
  - stop
  - terminate
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

## Terminating an AWS EC2 Instance
