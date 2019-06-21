---
layout: single
title:  "List AWS Subnets with Node.js"
date:   2019-5-28 10:00:00 -04:00
categories: javascript
tags: javascript node nodejs aws amazon ec2 subnet subnets subnetid ami cloud
header:
  image: assets/images/list-aws-subnets-with-nodejs-header.jpg
---
In order to [launch an Amazon EC2 instance]({{ site.baseurl }}{% post_url 2019-6-16-launch-stop-terminate-aws-ec2-instance-nodejs %}), we need both [the AMI to use]({{ site.baseurl }}{% post_url 2019-4-30-finding-a-linux-ami-with-nodejs %}) and the subnet we want to launch the instance into. In this article we will use Node.js to list the subnets available to us in a particular region.

Please note, it is beyond the scope of this post to define VPCs and subnets, however you can find more information on these concepts in [Amazon's documentation here](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Subnets.html) and in the [additional resources](#additional-resources) below.

Let's list!

```javascript
// load AWS SDK
const AWS = require('aws-sdk');

// set the region to Oregon
AWS.config.update({region:'us-west-2'});

// create EC2 service object
const ec2 = new AWS.EC2({apiVersion: '2016-11-15'});

// empty params object, needed to pass into describeSubnets function
const params = {};

ec2.describeSubnets(params, function(err, data) {
  if (err) {
    console.log(err, err.stack); // an error occurred
  } else {
    console.log(data);           // successful response
  }  
});
```

### Example output:
```javascript
data = {
 "Subnets": [
  {
   "AvailabilityZone": "us-west-2a",
   "AvailabilityZoneId": "usw2-az1",
   "AvailableIpAddressCount": 251,
   "CidrBlock": "10.0.0.0/24",
   "DefaultForAz": false,
   "MapPublicIpOnLaunch": true,
   "State": "available",
   "SubnetId": "subnet-9d4a7b6a",
   "VpcId": "vpc-a01106c2",
   "OwnerId": "38918754239506",
   "AssignIpv6AddressOnCreation": false,
   "Ipv6CidrBlockAssociationSet": [],
   "Tags": [],
   "SubnetArn": "arn:aws:ec2:us-west-2:38918754239506:subnet/subnet-9d4a7b6a"
  },   
  {
   "AvailabilityZone": "us-west-2b",
   "AvailabilityZoneId": "usw2-az2",
   "AvailableIpAddressCount": 251,
   "CidrBlock": "10.0.1.0/24",
   "DefaultForAz": false,
   "MapPublicIpOnLaunch": true,
   "State": "available",
   "SubnetId": "subnet-9d4a7b6b",
   "VpcId": "vpc-a01106c2",
   "OwnerId": "38918754239506",
   "AssignIpv6AddressOnCreation": false,
   "Ipv6CidrBlockAssociationSet": [],
   "Tags": [],
   "SubnetArn": "arn:aws:ec2:us-west-2:38918754239506:subnet/subnet-9d4a7b6b"
  },
  {
   "AvailabilityZone": "us-west-2c",
   "AvailabilityZoneId": "usw2-az3",
   "AvailableIpAddressCount": 251,
   "CidrBlock": "10.0.2.0/24",
   "DefaultForAz": false,
   "MapPublicIpOnLaunch": true,
   "State": "available",
   "SubnetId": "subnet-9d4a7b6c",
   "VpcId": "vpc-a01106c2",
   "OwnerId": "38918754239506",
   "AssignIpv6AddressOnCreation": false,
   "Ipv6CidrBlockAssociationSet": [],
   "Tags": [],
   "SubnetArn": "arn:aws:ec2:us-west-2:38918754239506:subnet/subnet-9d4a7b6c"
  }
 ]
}
```

From this output we want the `SubnetId`, which we can obtain with a slight update to our callback function:
```javascript
ec2.describeSubnets(params, function(err, data) {
  if (err) {                      // an error occurred
    console.log(err, err.stack);  
  } else {                        // successful response
    const subnetId = data.Subnets[0].SubnetId;
    console.log(subnetId);        // subnet-9d4a7b6a
  }  
});
```

With the `SubnetId` and the `ImageId` [obtained from describeImages]({{ site.baseurl }}{% post_url 2019-5-15-getting-an-ami-id-nodejs %}), we are now ready to [launch an instance]({{ site.baseurl }}{% post_url 2019-6-16-launch-stop-terminate-aws-ec2-instance-nodejs %})!

## Additional Resources
- [AWS Core Concepts: Analogy and Guide](https://start.jcolemorrison.com/aws-vpc-core-concepts-analogy-guide/)
- [AWS in Plain English](https://www.expeditedssl.com/aws-in-plain-english)
- [Intro to VPC](https://medium.com/tensult/intro-to-vpc-548b69f1bd1f)
- [AWS EC2 API](https://docs.aws.amazon.com/AWSJavaScriptSDK/latest/AWS/EC2.html)
- [EC2 describeSubnets](https://docs.aws.amazon.com/AWSJavaScriptSDK/latest/AWS/EC2.html#describeSubnets-property)
