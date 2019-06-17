---
layout: single
title:  "Getting an AMI ImageId with Node.js"
date:   2019-6-1 2:15:00 -04:00
categories: javascript
tags: javascript node nodejs aws ami amazon ec2
header:
  image: assets/images/get-aws-ami-id-nodejs-header.jpg
---
In order to [launch an Amazon EC2 instance]({{ site.baseurl }}{% post_url 2019-4-25-start-stop-terminate-aws-ec2-instance-nodejs %}), we need both the `ImageId` from [the AMI we want to use]({{ site.baseurl }}{% post_url 2019-5-15-finding-a-linux-ami-with-nodejs %}) and [the SubnetId]({{ site.baseurl }}{% post_url 2019-5-17-list-aws-subnets-nodejs %}) to launch the instance into.

In this article we illustrate how to get the `ImageId` from a Linux [Amazon Machine Image (AMI)](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AMIs.html) with Node.js.  I have also included an additional example, which shows how we can sort the results to easily get the most recent AMI.

Let's code!

```javascript
// load AWS SDK
const AWS = require('aws-sdk');

// set the region to Oregon
AWS.config.update({region:'us-west-2'});

// create EC2 service object
const ec2 = new AWS.EC2({apiVersion: '2016-11-15'});

// get the current Amazon Linux 2 AMIs
const params = {
  Filters: [
    {
      Name: 'name',
      Values: [
        'amzn2-ami-hvm-2.0.????????-x86_64-gp2'
      ]
    },
    {
      Name: 'state',
      Values: [
        'available'
      ]
    },
  ],
  Owners: [
    'amazon',
  ]  
 };

ec2.describeImages(params, function(err, data) {
  if (err) {                      // an error occurred
    console.log(err, err.stack);  
  } else {                        // successful response
    console.log(data);
  }  
});
```

### Example output:
```javascript
data = {
  "Images": [
    {
      "Architecture": "x86_64",
      "CreationDate": "2019-01-14T19:17:25.000Z",
      "ImageId": "ami-032509850cf9ee54e",
      "ImageLocation": "amazon/amzn2-ami-hvm-2.0.20190115-x86_64-gp2",
      "ImageType": "machine",
      "Public": true,
      "OwnerId": "137112412989",
      "ProductCodes": [],
      "State": "available",
      "BlockDeviceMappings": [
       {
        "DeviceName": "/dev/xvda",
        "Ebs": {
         "DeleteOnTermination": true,
         "SnapshotId": "snap-04359c6bb66cf4243",
         "VolumeSize": 8,
         "VolumeType": "gp2",
         "Encrypted": false
        }
       }
      ],
      "Description": "Amazon Linux 2 AMI 2.0.20190115 x86_64 HVM gp2",
      "EnaSupport": true,
      "Hypervisor": "xen",
      "ImageOwnerAlias": "amazon",
      "Name": "amzn2-ami-hvm-2.0.20190115-x86_64-gp2",
      "RootDeviceName": "/dev/xvda",
      "RootDeviceType": "ebs",
      "SriovNetSupport": "simple",
      "Tags": [],
      "VirtualizationType": "hvm"
     }
  ]
}
```

From this output we want the `ImageId`, which we can easily obtain with a slight update to our callback function:
```javascript
ec2.describeImages(params, function(err, data) {
  if (err) {                      // an error occurred
    console.log(err, err.stack);  
  } else {                        // successful response
    const imageId = data.Images[0].ImageId;
    console.log(imageId);         // ami-032509850cf9ee54e
  }  
});
```

Now that we have an AMI `ImageId`, [let's grab a SubnetId]({{ site.baseurl }}{% post_url 2019-5-17-list-aws-subnets-nodejs %}), and then [launch an EC2 instance]({{ site.baseurl }}{% post_url 2019-4-25-start-stop-terminate-aws-ec2-instance-nodejs %})!

## Bonus - Sorting AMIs by creation date
When we describe all the images available to us, the results are ordered arbitrarily. If we want to obtain the most recent AMI we can sort by `CreationDate`. In the following example, I have added a function `sortByCreationDate` that does just that.

```javascript
// load AWS SDK
const AWS = require('aws-sdk');

// set the region to Oregon
AWS.config.update({region:'us-west-2'});

// create EC2 service object
const ec2 = new AWS.EC2({apiVersion: '2016-11-15'});

// get the current Amazon Linux 2 AMIs
const params = {
  Filters: [
    {
      Name: 'name',
      Values: [
        'amzn2-ami-hvm-2.0.????????-x86_64-gp2'
      ]
    },
    {
      Name: 'state',
      Values: [
        'available'
      ]
    },
  ],
  Owners: [
    'amazon',
  ]  
 };

// sorts the array of images by creation date
// the most recent AMIs will appear first
function sortByCreationDate(data) {
  const images = data.Images;
  images.sort(function(a,b) {
    const dateA = a['CreationDate'];
    const dateB = b['CreationDate'];
    if (dateA < dateB) {
      return -1;
    }
    if (dateA > dateB) {
      return 1;
    }
    // dates are equal
    return 0;
  });

  // arrange the images by date in descending order
  images.reverse();
}

ec2.describeImages(params, function(err, data) {
  if (err) {                      // an error occurred
    console.log(err, err.stack);  
  } else {                        // successful response
    sortByCreationDate(data);
    const imageId = data.Images[0].ImageId;
    console.log(imageId);         // ami-0cb72367e98845d43
  }  
});
```

As you can see in the above snippet, we obtain the `ImageId` in the exact same way as before, however the first element of the `Images` array will always be the most recent AMI! This is useful if we want to [launch instances]({{ site.baseurl }}{% post_url 2019-4-25-start-stop-terminate-aws-ec2-instance-nodejs %}) with the latest and greatest architecture.

## Additional Resources
- [Finding a Linux AMI with Node.js]({{ site.baseurl }}{% post_url 2019-5-15-finding-a-linux-ami-with-nodejs %})
- [AWS EC2 API](https://docs.aws.amazon.com/AWSJavaScriptSDK/latest/AWS/EC2.html)
- [EC2 describeImages](https://docs.aws.amazon.com/AWSJavaScriptSDK/latest/AWS/EC2.html#describeImages-property)
- [MDN: Array.prototype.sort](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)
