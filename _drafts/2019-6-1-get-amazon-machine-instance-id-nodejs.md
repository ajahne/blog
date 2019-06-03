---
layout: single
title:  "Get AWS AMI ID with Node.js"
date:   2019-6-1 2:15:00 -04:00
categories: javascript
tags: javascript node nodejs aws ami amazon ec2
header:
  image: assets/images/get-aws-ami-id-nodejs-header.jpg
---
In order to [launch an Amazon EC2 instance]({{ site.baseurl }}{% post_url 2019-4-25-start-stop-terminate-aws-ec2-instance-nodejs %}), we need both [the AMI to use]({{ site.baseurl }}{% post_url 2019-5-15-finding-a-linux-ami-with-nodejs %}) and the SubnetId to launch the instance into.

In this article we illustrate how to get the ImageId from an an Amazon Machine Image (AMI) with Node.js.  I have also included an additional example, which shows how we can sort the results to ensure we get the most

Let's code!

```javascript
//load AWS SDK
const AWS = require('aws-sdk');

//set the region, going to perform tests in Oregon
AWS.config.update({region:'us-west-2'});

//create EC2 service object
const ec2 = new AWS.EC2({apiVersion: '2016-11-15'});

//get the current Amazon Linux 2 AMIs
const params = {
  DryRun:false,
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
     "CreationDate": "2019-05-09T00:58:10.000Z",
     "ImageId": "ami-0cb72367e98845d43",
     "ImageLocation": "amazon/amzn2-ami-hvm-2.0.20190508-x86_64-gp2",
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
        "SnapshotId": "snap-05f1f2daed90efa18",
        "VolumeSize": 8,
        "VolumeType": "gp2",
        "Encrypted": false
       }
      }
     ],
     "Description": "Amazon Linux 2 AMI 2.0.20190508 x86_64 HVM gp2",
     "EnaSupport": true,
     "Hypervisor": "xen",
     "ImageOwnerAlias": "amazon",
     "Name": "amzn2-ami-hvm-2.0.20190508-x86_64-gp2",
     "RootDeviceName": "/dev/xvda",
     "RootDeviceType": "ebs",
     "SriovNetSupport": "simple",
     "Tags": [],
     "VirtualizationType": "hvm"
    }
  ]
}
```

From this output we want the `ImageId`, which we can obtain in the following manner:
```javascript
const imageId = data.Images[0].ImageId; //ami-0cb72367e98845d43
```

Now that we have an AMI `ImageId`, [let's grab a SubnetId]({{ site.baseurl }}{% post_url 2019-5-17-list-aws-subnets-nodejs %}), and then [launch an EC2 instance]({{ site.baseurl }}{% post_url 2019-4-25-start-stop-terminate-aws-ec2-instance-nodejs %})!

## Bonus - Sorting AMIs by creationDate
When we describe all the images available to us, the results are ordered arbitrarily. If we want to obtain the most recent AMI we can sort by `creationDate`. Code time...

```javascript
//load AWS SDK
const AWS = require('aws-sdk');

//set the region, going to perform tests in Oregon
AWS.config.update({region:'us-west-2'});

//create EC2 service object
const ec2 = new AWS.EC2({apiVersion: '2016-11-15'});

//get the current Amazon Linux 2 AMIs
const params = {
  DryRun:false,
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

//sorts the array of images by creation date
//the most recent AMIs will appear first
function sortByCreationDate(data) {
  data.Images.sort(function(a,b) {
    const dateA = a["CreationDate"];
    const dateB = b["CreationDate"];
    if (dateA < dateB) {
      return -1;
    }
    if (dateA > dateB) {
      return 1;
    }
    //dates are equal
    return 0;
  });

  //reverse so we have the images sorted by date in descending order
  images.reverse();
}

ec2.describeImages(params, function(err, data) {
  if (err) {                      // an error occurred
    console.log(err, err.stack);  
  } else {                        // successful response
    sortByCreationDate(data);
    console.log(data);
  }  
});
```

## Additional Resources
- [Finding a Linux AMI with Node.js]({{ site.baseurl }}{% post_url 2019-5-15-finding-a-linux-ami-with-nodejs %})
- [AWS EC2 API](https://docs.aws.amazon.com/AWSJavaScriptSDK/latest/AWS/EC2.html)
- [EC2 describeSubnets](https://docs.aws.amazon.com/AWSJavaScriptSDK/latest/AWS/EC2.html#describeSubnets-property)
