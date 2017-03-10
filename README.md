
---

# AWS S3

---

###### Table of Contents

* [Introduction](#introduction)
* [What is S3](#s3)
* [S3 buckets](/chapter1.md)
  * [Create](#create-an-s3-bucket) / Delete / List 
* [S3 objects](/s3-objects.md)
* [ACL and Policies](#acls--policies)
* [S3 Security](/s3-and-security.md)



You can checkout all the examples in this book at https://github.com/nagwww/101-AWS-S3-Hacks 

# 

# Introduction..

---

Digital information is driving exponential growth in data. Data in the form of genes, biometrics, logs, events, photos, videos, comments, etc play a key role in the current digital generation.

If you are student, teacher, doctor, engineer no matter the profession it is likely that you are playing with data in every walk of life.

Here are some basics of data

* Each of the 0's and 1's is called a bit - Binary digit
* Eight bits form a Byte

##### Running code and examples \[ test \]

Option 1 :

Option 2 :

Contributors

# What is S3 {#s3}

---

S3 stands for **S**imple **S**torage **S**ervice. An Amazon service which was released on

The one word answer for it's widely used popularity is the ease of use at any scale ranging from 1 byte to peta bytes.

S3 is used to store your data on internet. In layman terms

* Imagine like a Folder in your C drive. Just that the Folder is present on internet.
* Imagine like a Directory on your UNIX/UBUNTU server, just that the directory is on internet.

  ?![](/assets/s31.jpg)

* You can store your personal files \( Photos, videos, documents \). Why buy an external hard drive you can as well use S3

* Database administrators can use it to store the RMAN Backups

* Do you have a website, then you can store your static pages like Images, Java Script, HTML,CSS.

# S3 buckets {#buckets}

---

Amazon Bucket is a container of data. In technical terms “A bucket is a Container with objects Inside”.

A few things to keep in mind when working with AWS S3 buckets,

* Buckets names are unique
* Buckets are regional
* By default you can create 101 buckets in an AWS account, you can always work with AWS support and increase the limit.

#### Create an S3 bucket

Come up with a bucket naming convention, for me I would like append the AWS region for all the buckets.

By default when you create an S3 bucket if you do not specify a region they are created in "us-east-1" region

Using AWS CLI :

```py
"""
- Hack    : Create an Bucket in S3
- AWS CLI : aws s3api create-bucket  --bucket us-east-1.nag
"""

import boto3

if __name__ == "__main__":
    client = boto3.client('s3')
    bucketname = "us-east-1.nag"
    print client.create_bucket(Bucket=bucketname)

```

To create an S3 bucket in a different AWS region

```py
"""
- Hack    : Create an Bucket in S3
- AWS CLI : aws s3api create-bucket  --bucket us-west-1.nag --region us-west-1 --create-bucket-configuration LocationConstraint=us-west-1

"""

import boto3

if __name__ == "__main__":
    client = boto3.client('s3')
    bucketname = "us-west-1.nag"
    print client.create_bucket(Bucket=bucketname, CreateBucketConfiguration={'LocationConstraint': 'us-west-1'})
```

#### Delete an S3 Bucket {#bucket}

To delete a S3 bucket

```py
import boto3

if __name__ == "__main__":
   client = boto3.client('s3')
   bucket_name = "101-s3-aws-1"
   print client.delete_bucket(Bucket=bucket_name)
```

To delete a S3 bucket in a different region

```py

"""
- Hack   : Delete an Bucket in S3
- AWS CLI: aws s3api delete-bucket --bucket us-west-1.nag ( You do not have to specify the region when deleting the bucket )
"""

import boto3

if __name__ == "__main__":
    client = boto3.client('s3', region_name="us-west-1")
    bucket_name = "us-west-1.nag"
    print client.delete_bucket(Bucket=bucket_name)
```

#### Find out all the S3 buckets in  your AWS Account.

By default you can only create 101 S3 buckets in an AWS account. If needed you can work with AWS to increase the limit,

Here is a quick script to list all the S3 buckets in your account

```py
import boto3

if __name__ == "__main__":
   client = boto3.client('s3')
   all_buckets =  client.list_buckets()["Buckets"]
   for bucket in all_buckets:
       print bucket["Name"], "Created on ", bucket["CreationDate"]
```

# 

# S3 Objects

---

You can think of objects as a file. An object has,

* Data
* MetaData





# ACL's & Policies

---

ACL's and policies are the gate keepers for your data in S3.

##### ACL - Access Control List

This is how an ACL looks like if you are curious.

* Every Bucket and object has an ACL
* Every

![](/assets/s3_acl.jpg)

# Archiving & Backup

---

Archiving

* Archiving is for space management and long term retention.

Backup

* Backup is for recovery from hardware of data corruption. This is the the data that is needed for near term business continuity 

Here are few way you can use to



|  |
| :--- |
| LifeCycle |
| Glacier |
| Google Cloud Platform |
| Microsoft - Azure |

#### LifeCycle

#### Glacier

Google Cloud Platform

# S3 and Security

---

There are primarily two layers of security you can use to secure you S3 data

* Resource level security
  * S3 ACLS.
  * S3 Policies at bucket level
  * S3 permissions at object level
* User level security
  * AWS IAM Policy

Things to note :

AWS account which create the object is the owner of the object. Here are few example,

Tools I use to monitor my S3.

Security Monkey

