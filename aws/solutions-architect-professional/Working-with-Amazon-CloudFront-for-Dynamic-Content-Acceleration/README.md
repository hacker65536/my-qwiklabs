# Working with Amazon CloudFront for Dynamic Content Acceleration

https://qwiklabs.com/focuses/330?parent=catalog


- 10credits
- 1:57:00

## Create an Amazon cloudFront Web Distribution

Create Distribution

- [x] web
- [ ] RTMP(Real Time Messaging Protocol)

Get Started

origin settings
 - Origin Domain Name (ForumURL / ec2 public DNS)
Default Cache Behavior Settings
 - View Protocol Policy: HTTP and HTTPS
 - Allowed HTTP Methods: GET,HEAD,OPTIONS,PUT,POST,PATCH,DELETE
 - Object Caching: Customize
  - Minimun TTL: 0
 - Forward Cookies: All
 - Query String Forwarding and Caching: Foward all, cache based on all
Distribution Settings
 - Price Class: Use All Edge Locations(Best Performance)
 - Alternate Domain Names(CNAMEs): Leave empty
 - SSL Certificate: Default CloudFront Certificate(*.cloudfront.net)
 - Default Root Object: Leave this as blank
 - Logging: Leave this Off
 - Distribution State: Enabled

Create Distribution ( will take approximately 15 mins )
*70+ global endpoint locations


## Create a Custom Error Page

`Custom404ErrorPage.html`
```html
<html><body>
<h2>This is not the page you are looking for!</h2>
</body></html>
```
upload to S3 bucket whose name starts with : _qls_

make it public


## Customize your Amazon CloudFront Web Distribution

Select the distribution and Click Distribution Settings.

Behaviors tab -> Create Behavior
- Path Pattern : `*.gif`
- Object Caching : Customize
 - Minimum TTL: 86400

Create

Origins tab -> Create Origin
- Origin Domain Name: select S3 bucket that starts with qls
- Restrict Bucket Access: yes
- Your Identities: access idenitity ...? (access-idenitity-)

Create

Behaviors tab -> Create Behavior
- Path Pattern: `/Custom*ErrorPage.html`
- Origin: select S3-*qls*

Create

Error Pages -> Create Custom Error Response
- HTTP Error Code: 404: Not Found
- Customize Error Response: Yes
- Response Page Path: `/Custom404ErrorPage.html`
- HTTP Response Code: 404: Not Found

Create

## Configure the PHP Forum Website

`http://ForumURL/phpbb`

login `user:bitnami`

go to ACP -> Server settings -> Server URL settings -> Force server URL settings to Yes

copy cloudfront Domain Name and paste to phpbb Domain name field. submit.

## access from cloudfront
when cloudfront be deployed

d11h3sk6eqqw2j.cloudfront.net/phpbb


## ??
cant access to ACP

