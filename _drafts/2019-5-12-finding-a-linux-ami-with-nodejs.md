---
layout: single
title:  "Finding a Linux AMI with Node.js"
date:   2019-5-12 8:00:00 -04:00
categories: javascript
tags: javascript node nodejs aws amazon ec2 linux ami
header:
  image: assets/images/finding-a-linux-ami-with-nodejs-header.jpg
---

# Describe Amazon Machine Images
Node.js examples of `describeImages` based off Amazon's [Finding a Linux AMI](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/finding-an-ami.html) documentation.

## Example: Find the current Amazon Linux 2 AMI
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

## Example: Find the current Amazon Linux AMI
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

## Example: Find the current Ubuntu Server 16.04 LTS AMI
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

## Example: Find the 2019 Ubuntu Bionic Servers
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

## Example: Find the current Red Hat Enterprise Linux 7.5 AMI
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
