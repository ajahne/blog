---
layout: single
title:  "List AWS Subnets with Node.js"
date:   2019-5-17 10:30:00 -04:00
categories: javascript
tags: javascript node nodejs aws amazon ec2 subnet subnets
header:
  image: assets/images/list-aws-subnets-with-nodejs-header.jpg
---
In order to [launch an Amazon EC2 instance]({{ site.baseurl }}{% post_url 2019-4-25-start-stop-terminate-aws-ec2-instance-nodejs %}), we need both the AMI to use and the subnet we want to launch the instance into. This entry will show you how to use Node.js to list the subnets available to you in a particular region.

Please note, it is beyond the scope of this post to define VPCs and subnets, however you can find more information on these concepts in [Amazon's documentation here](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Subnets.html) and in the [additional resources](#additional-resources) below.

Let's list!

```javascript
//load AWS SDK
const AWS = require('aws-sdk');

//setting the region to Oregon
AWS.config.update({region:'us-west-2'});

//create EC2 service object
const ec2 = new AWS.EC2({apiVersion: '2016-11-15'});

//empty params object, needed to pass into describeSubnets function
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
  Subnets: [
    {
      AvailabilityZone: "us-west-2c",
      AvailableIpAddressCount: 251,
      CidrBlock: "10.0.1.0/24",
      DefaultForAz: false,
      MapPublicIpOnLaunch: false,
      State: "available",
      SubnetId: "subnet-9d4a7b6c",
      VpcId: "vpc-a01106c2"
    }
  ]
}
```

From this output we want the `SubnetId`, which we can obtain in the following manner:
```javascript
const subnetId = data.Subnets[0].SubnetId;
```

With the `SubnetId` and the `ImageId` obtained from [describeImages]({{ site.baseurl }}{% post_url 2019-5-15-finding-a-linux-ami-with-nodejs %}), we are now ready to [launch an instance](({{ site.baseurl }}{% post_url 2019-4-25-start-stop-terminate-aws-ec2-instance-nodejs %}))!

## Additional Resources
- [AWS EC2 API](https://docs.aws.amazon.com/AWSJavaScriptSDK/latest/AWS/EC2.html)
- [EC2 describeSubnets](https://docs.aws.amazon.com/AWSJavaScriptSDK/latest/AWS/EC2.html#describeSubnets-property)
