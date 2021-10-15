# Hosting a Static-website-using-S3-bucket



[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

## Description.
Here, we are creating a simple html website. However, it's files are loading from s3 bucket.An Amazon S3 bucket is a public cloud storage resource available in Amazon Web Services' (AWS) Simple Storage Service (S3), an object storage offering. Amazone s3 is imilar to file folders, store objects, which consist of data and its descriptive metadata.
### Resources
- Creation of s3 bucket
- Uploading files to s3 bucket
- Creation of bucket policy to make bucket objects public

### Prerequisites for this project

- Need an IAM user
- bucket policy

### IAM User Configuration via aws cli

Here Iam configuring an IAM user with S3 full access
```sh
[root@ip-172-31-6-205 html]# aws configure
AWS Access Key ID [None]: ************
AWS Secret Access Key [None]: ********************
Default region name [None]: ap-south-1
Default output format [None]: json
```
## Bucket policy creation for providing priveillages for IAM user to access the bucket.
Here we are creating a bucket policy under the bucket "ddr3.website" for providing priveillage for IAM user to access the bucket.

The following bucket policy is added under the bucket permmision section.
```sh
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::*****************:user/test"
            },
            "Action": "s3:*",
            "Resource": [
                "arn:aws:s3:::***************",
                "arn:aws:s3:::************/*"
            ]
        }
    ]
}
```


## Uploading files to the s3 bucket using sync command:
The following command sync local image folder with s3 bucket. You can directly drag images to the bucket using upload command in aws console.


```sh
root@pc1:# aws s3 sync . s3://ddr3.website

upload: css/bootstrap.min.css to s3://ddr3.website/css/bootstrap.min.css
upload: fontawesome/LICENSE.txt to s3://ddr3.website/fontawesome/LICENSE.txt
upload: css/slick.css to s3://ddr3.website/css/slick.css          
upload: css/tooplate-simply-amazed.css to s3://ddr3.website/css/tooplate-simply-amazed.css
upload: fontawesome/webfonts/fa-regular-400.eot to s3://ddr3.website/fontawesome/webfonts/fa-regular-400.eot
upload: fontawesome/webfonts/fa-brands-400.woff2 to s3://ddr3.website/fontawesome/webfonts/fa-brands-400.woff2
upload: fontawesome/css/all.min.css to s3://ddr3.website/fontawesome/css/all.min.css
upload: fontawesome/webfonts/fa-brands-400.woff to s3://ddr3.website/fontawesome/webfonts/fa-brands-400.woff
upload: fontawesome/webfonts/fa-brands-400.ttf to s3://ddr3.website/fontawesome/webfonts/fa-brands-400.ttf
upload: fontawesome/webfonts/fa-regular-400.woff to s3://ddr3.website/fontawesome/webfonts/fa-regular-400.woff
upload: fontawesome/webfonts/fa-regular-400.ttf to s3://ddr3.website/fontawesome/webfonts/fa-regular-400.ttf
upload: fontawesome/webfonts/fa-regular-400.woff2 to s3://ddr3.website/fontawesome/webfonts/fa-regular-400.woff2
upload: fontawesome/webfonts/fa-brands-400.svg to s3://ddr3.website/fontawesome/webfonts/fa-brands-400.svg
upload: fontawesome/webfonts/fa-regular-400.svg to s3://ddr3.website/fontawesome/webfonts/fa-regular-400.svg
upload: img/gallery-img-01.jpg to s3://ddr3.website/img/gallery-img-01.jpg
upload: fontawesome/webfonts/fa-solid-900.woff to s3://ddr3.website/fontawesome/webfonts/fa-solid-900.woff
upload: fontawesome/webfonts/fa-solid-900.ttf to s3://ddr3.website/fontawesome/webfonts/fa-solid-900.ttf
upload: img/gallery-img-02.jpg to s3://ddr3.website/img/gallery-img-02.jpg
upload: fontawesome/webfonts/fa-solid-900.eot to s3://ddr3.website/fontawesome/webfonts/fa-solid-900.eot
upload: fontawesome/webfonts/fa-solid-900.woff2 to s3://ddr3.website/fontawesome/webfonts/fa-solid-900.woff2
upload: img/gallery-img-03.jpg to s3://ddr3.website/img/gallery-img-03.jpg
upload: img/gallery-img-06.jpg to s3://ddr3.website/img/gallery-img-06.jpg
upload: img/gallery-img-05.jpg to s3://ddr3.website/img/gallery-img-05.jpg
upload: img/gallery-img-04.jpg to s3://ddr3.website/img/gallery-img-04.jpg
upload: fontawesome/webfonts/fa-solid-900.svg to s3://ddr3.website/fontawesome/webfonts/fa-solid-900.svg
upload: img/gallery-img-07.jpg to s3://ddr3.website/img/gallery-img-07.jpg
upload: img/gallery-img-08.jpg to s3://ddr3.website/img/gallery-img-08.jpg
upload: img/gallery-img-09.jpg to s3://ddr3.website/img/gallery-img-09.jpg

```

### Now we are creating a bucket policy to make the objects in s3 bucket as public
Before that we have to edit the status of Block public access (bucket settings) to off from on status.

![alt text](https://github.com/rony-james/Static-website-using-S3-bucket/blob/main/ddr1.png?raw=true)



```sh
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": [
                "s3:GetObject"
            ],
            "Resource": [
                "arn:aws:s3:::ddr3.website/*"
            ]
        }
    ]
}
```
![alt text](https://github.com/rony-james/Static-website-using-S3-bucket/blob/main/ddr2.png?raw=true)

The above code will provide all the object in that bucket to public access.
Now go to the "static website hosting" option under the properties section of the bucket.

![alt text](https://github.com/rony-james/Static-website-using-S3-bucket/blob/main/ddr4.png?raw=true)

Now our images are loading from s3 bucket, we can identify the same by browsing website's image on a browser tab and see the image url will be pointed to your S3 bucket like "http://ddr3.website.s3-website.us-east-2.amazonaws.com"

Please check the following screen shots :
![alt text](https://github.com/rony-james/Static-website-using-S3-bucket/blob/main/ddr3.png?raw=true)


