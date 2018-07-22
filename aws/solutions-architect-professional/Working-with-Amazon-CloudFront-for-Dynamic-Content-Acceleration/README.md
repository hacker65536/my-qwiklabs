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
