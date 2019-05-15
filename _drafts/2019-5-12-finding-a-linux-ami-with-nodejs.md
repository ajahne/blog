---
layout: single
title:  "Finding a Linux AMI with Node.js"
date:   2019-5-12 8:00:00 -04:00
categories: javascript
tags: javascript node nodejs aws amazon ec2 linux ami
header:
  image: assets/images/finding-a-linux-ami-with-nodejs-header.jpg
---
In order to launch an Amazon EC2 instance, we need the AMI to use. This can be done in a myriad of ways, including the command line and AWS GUI Console. In this article we will leverage Node.js to get the job done!

Before choosing an AMI, there are multiple factors to consider:
- The Region
- The operating system (e.g. Ubuntu)
- The architecture: 32-bit (i386) or 64-bit (x86_64)
- The root device type: Amazon EBS or instance store
- The provider (e.g. Amazon)
- The state (e.g. is it currently available)
- Additional software (e.g. SQL server)

In working with launching EC2 instances with Node.js, I did not find a clear guide to help me obtain I needed. So, I decided to write some code, figure it out, and turn my learning into an article!

This is an example driven article with Node.js snippets of `describeImages` based on Amazon's [Finding a Linux AMI](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/finding-an-ami.html) documentation.

### Table of Contents
- Examples
  - [Find the current Amazon Linux 2 AMI](#example-find-the-current-amazon-linux-2-ami)
  - [Find the current Amazon Linux AMI](#example-find-the-current-amazon-linux-ami)
  - [Find the current Ubuntu Server 16.04 LTS AMI](#example-find-the-current-ubuntu-server-1604-lts-ami)
  - [Find the 2019 Ubuntu Bionic Servers](#example-find-the-2019-ubuntu-bionic-servers)
  - [Find the current Red Hat Enterprise Linux 7.5 AMI](#example-find-the-current-red-hat-enterprise-linux-75-ami)
- [Additional Resources](#additional-resources)

### Example: Find the current Amazon Linux 2 AMI
```javascript
const AWS = require('aws-sdk');
const fs = require("fs");

//set the region, going to perform tests in oregon
AWS.config.update({region:'us-west-2'});

//create ec2
const ec2 = new AWS.EC2({apiVersion: '2016-11-15'});

//date, which is 8 chars, e.g. 20190403
//hardware is 6? chars, can be arm64 or, x86_64
const params = {
  DryRun:false,
  Filters: [
    {
      Name: 'name',
      Values: [
        'amzn2-ami-hvm-2.0.????????-??????-??????????????'
      ]
    },
    {
      Name: 'state',
      Values: [
        'available'
      ]
    },
    /* more items */
  ],
  Owners: [
    'amazon',
    /* more items */
  ]  
 };

ec2.describeImages(params, function(err, data) {
  if (err) {
    console.log(err, err.stack); // an error occurred
  } else {
    console.log('success');
    fs.writeFile('data2.json', JSON.stringify(data, null, ' '), (err) => {
      if (err) {
        throw err;
      }
      console.log('The file has been saved');
    });
    console.log('After writing, but before callback');
    // console.log(data);           // successful response
  }  
});
```

### Example: Find the current Amazon Linux AMI
```javascript
const params = {
  DryRun:false,
  Filters: [
    {
      Name: 'name',
      Values: [        
        'amzn-ami-hvm-????.??.?.????????-x86_64-gp2'
      ]
    },
    {
      Name: 'state',
      Values: [
        'available'
      ]
    },
    /* more items */
  ],
  Owners: [
    'amazon',
    /* more items */
  ]  
 };
```

### Example: Find the current Ubuntu Server 16.04 LTS AMI
```javascript
const params = {
  DryRun:false,
  Filters: [
    {
      Name: 'name',
      Values: [
        'ubuntu/images/hvm-ssd/ubuntu-xenial-16.04-amd64-server-????????'
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
    '099720109477',
  ]  
 };
```

### Example: Find the 2019 Ubuntu Bionic Servers
```javascript
const params = {
  DryRun:false,
  Filters: [
    {
      Name: 'name',
      Values: [
        'ubuntu/images/hvm-ssd/ubuntu-bionic-18.04-amd64-server-2019????'
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
    '099720109477',
  ]  
 };
```

### Example: Find the current Red Hat Enterprise Linux 7.5 AMI
```javascript
const params = {
  DryRun:false,
  Filters: [
    {
      Name: 'name',
      Values: [
        'RHEL-7.5_HVM_GA*'
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
    '309956199498',
  ]  
 };
```

## Additional Resources
- [Finding a Linux AMI](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/finding-an-ami.html)
- [AWS EC2 API](https://docs.aws.amazon.com/AWSJavaScriptSDK/latest/AWS/EC2.html)
- [EC2 describeImages](https://docs.aws.amazon.com/AWSJavaScriptSDK/latest/AWS/EC2.html#describeImages-property)
