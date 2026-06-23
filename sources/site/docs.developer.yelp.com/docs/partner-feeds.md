# Source: https://docs.developer.yelp.com/docs/partner-feeds

> ## 📘
> 
> This is a Yelp Partner API
> 
> Access is disabled by default. See [Yelp Partner APIs](https://docs.developer.yelp.com/docs/yelp-partner-apis) on how to get access.

# 

Summary

Yelp provides an easy way for partners to get access to current Yelp data (as files in JSON format) on a regular basis. Partners can access the feed through a secure file share where Yelp uploads up-to-date data on a daily basis.

# 

Onboarding steps

1. Yelp/Partner contract signed.
2. Partner provides GPG key so Yelp can generate and return credentials to the partner in 
 a secure way.
3. Yelp sets up an Amazon S3 location to securely share for partner (typically 
 s3://yelp-syndication/{partner}/).
4. Yelp sets up an internal pipeline to drop a full data dump of all requested data in JSON 
 format in the secure file share on a regular basis. (typical S3 filename looks like 
 s3://yelp-syndication/{partner}/YYYYMMDD\_businesses.json.gz)
5. Yelp uses the partner's provided GPG key to generate credentials for accessing the 
 secure file share on S3.
6. Yelp shares the credentials (a filename like {partner}\_s3\_credentials.asc) & access instructions with partner.

# 

Accessing the Data

### 

Example of how to access feeds using s3cmd:

Bash

`$ s3cmd ls s3://yelp-syndication/{partner}/ 2014-02-07 04:56 15176012734 s3://yelp-syndication/{partner}/20140207_businesses.json.gz  $ s3cmd get s3://yelp-syndication/{partner}/20140207_businesses.json.gz`

### 

Example of how to access feeds using boto in Python:

Python

`>>> from boto.s3.connection import S3Connection >>> conn = S3Connection(<ACCESS_KEY_ID>, <SECRET_ACCESS_KEY>) >>> bucket = conn.get_bucket('yelp-syndication', validate=False) >>> list(bucket.list('<partner>/')) <Key: yelp-syndication,<partner>/20140207_businesses.json.gz>] >>> bucket.get_key('<partner>/20140207_businesses.json.gz').get_contents_to_filename('feed.gz')`

# 

Common Issues

### 

Decrypting & viewing S3 credentials file

Yelp will provide a file with a filename like {partner}\_s3\_credentials.asc This file contains S3 access key ID and secret access key, but is encrypted.

### 

To decrypt:

JavaScript

`gpg --decrypt <partner>_s3_credentials.asc`

### 

The contents of the decrypted file should look like:

JavaScript

 `User:  <partner>  Access Key ID:  <a long, random-looking string> Secret Access Key: <a very long, random-looking string>`

This information can be used to access partner's JSON feeds on S3 using s3cmd, boto, etc. (see 'Accessing the Data' above

### 

When trying to access S3 data, an error occurs...

1. If your business already uses Amazon S3, check that you are using the S3 credentials generated & provided by Yelp, rather than your existing credentials.
 
2. Check that the S3 Access Key ID and Secret Access Key you are using are correct by re-decrypting the credentials file provided by yelp.
 
3. Check that all characters in your command are ASCII
 

### 

When a Biz ID is not return in the feed ...

There are a couple of reasons why a Biz ID is not returned in the feed

1. Biz ID is a test location (most of the case)
 
2. Biz that is inactive, restricted
 
3. Biz ID is being merged/migrated to another Biz ID and becomes inactive after the merge. You can find the new biz-id that being merged/migrated into by using our Business Detail endpoint (check out the 301 error code). 
 [https://www.yelp.com/developers/documentation/v3/business](https://www.yelp.com/developers/documentation/v3/business)
 

> ## 📘
> 
> Check out our Yelp Insights API Reference Page
> 
> ![:owlbert:](https://docs.developer.yelp.com/public/img/emojis/owlbert.png) [Endpoints](https://docs.developer.yelp.com/reference#testinput)

Updated 10 months ago

---

Did this page help you?

Yes

No

Copy Page