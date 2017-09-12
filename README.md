AWS S3 as Maven Repository
=======================

This project demonstrates how to use AWS S3 as maven repository. [AWS Maven Wagon](https://github.com/spring-projects/aws-maven) plugin is used.

create a simple-storage bucket
------------------------

```
```

## AWS Account Permissions
Proper AWS account permissions need to be granted to allow the account to write and read objects from S3.

They are required to publish artifacts to S3 or download artifacts via `s3://` schema.

You may use _AmazonS3FullAccess_ policy template for this permission.


### Configure Bucket Policy
You need to configure bucket policy so that those artifacts could be accessable. Example as below:

    {
      "Id": "Policy1397027253868",
      "Statement": [
        {
          "Sid": "Stmt1397027243665",
          "Action": [
            "s3:ListBucket"
          ],
          "Effect": "Allow",
          "Resource": "arn:aws:s3:::<BUCKET_NAME>",
          "Principal": {
            "AWS": [
              "*"
            ]
          }
        },
        {
          "Sid": "Stmt1397027177153",
          "Action": [
            "s3:GetObject"
          ],
          "Effect": "Allow",
          "Resource": "arn:aws:s3:::<BUCKET_NAME>/*",
          "Principal": {
            "AWS": [
              "*"
            ]
          }
        }
      ]
    }

Demo Projects
=============

## publish-artifact
This project is a sample maven project. It's configured to be published to s3 based repository.

It is used to demonstrate maven artifacts publish to S3 based repository.


## talk-to-s3
This project depends on **uploadme** project.

It is used to demonstrate resolving dependencies using S3 based repository with an `s3://` schema.

Configuration
=============

## Local AWS Account Settings
S3 access keys should be configured under `~/.m2/settings.xml`.

    <settings>
       <servers>
        <server>
          <id>aws-release</id>
          <username>AKIAIC5IC111111111</username>
          <password>ACF1111111111111111111111111111111</password>
        </server>
        <server>
          <id>aws-snapshot</id>
          <username>AKIAIC5IC111111111</username>
          <password>ACF1111111111111111111111111111111</password>
        </server>
      </servers>
    </settings>


