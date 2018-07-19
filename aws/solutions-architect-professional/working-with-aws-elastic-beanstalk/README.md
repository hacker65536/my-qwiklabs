# Working with AWS Elastic Beanstalk
https://qwiklabs.com/focuses/1217?parent=catalog
- 8Credits
- times 1hour



## create New Application

- Application Name: `DeployRubyApp`
- Description: `My Ruby Application`

### All Application -> DeployRubyApp   
click the `Create one now` link link

### Select environment tier
select `web server environment`

- [x] Web server environment
- [ ] Worker environment

### Create a web server environment

Environment information

- Description `My Ruby Application`

Base configuration

- platform: Preconfigured platfrom `Ruby`
- Application code: Upload youor code `Public S3 URL`
  - http://us-west-2-aws-training.s3.amazonaws.com/awsu-spl/spl-42/scripts/eb_sample_app.zip
  
__configure more option__

### Configure Deployrubyapp-env

click `Change platform configuration` link then configure

- select `Passenger with Ruby 1.9.3 running on 64bit Amazon Linux/2.8.1`

### Modify instances

click __modify__ in the __Instances__ box

- Instance Type: `t2.micro`

### Modify capacity

- [x] Single instance
- [ ] Load balanced

### Modify security

select below
- Service role
- EC2 key pair
- IAM instance profile

### Modify database

- Engine: mysql
- Instance class: db.t2.micro
- Storage: 5GB
- Username: sampleRubyRoot
- Password: myRubyPassword123

### Create environament

click `Create environment`


### resources

- arn:aws:iam::690384115853:role/aws-elastic-beanstalk-ec2-role
  - arn:aws:iam::690384115853:instance-profile/qls-3192456-eca541ef7ccf3f1a-AWSBeanstalkEc2Role-1RSFC0ACBWHU9
  - AWSElasticBeanstalkWebTier
  - AWSElasticBeanstalkMulticontainerDocker
  - AWSElasticBeanstalkWorkerTier
  
### access application

http://deployrubyapp-env.fmmahh6d4h.us-west-2.elasticbeanstalk.com/

input email and show user list

http://deployrubyapp-env.fmmahh6d4h.us-west-2.elasticbeanstalk.com/users


### Modify capacity (for scale)

All applications -> configuration  
Configuration overview -> capacity box

- [ ] Single instance
- [x] Load balanced
  - Instances Min: 2
  
  apply -> confirm

### EVENTS

| 2018-07-20 01:05:03 UTC+0900 | INFO | Environment health has transitioned from Info to Ok.                                                                                                                                                                                                                                                       |
|------------------------------|------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 2018-07-20 01:04:26 UTC+0900 | INFO | Environment update completed successfully.                                                                                                                                                                                                                                                                 |
| 2018-07-20 01:04:26 UTC+0900 | INFO | Successfully deployed new configuration to environment.                                                                                                                                                                                                                                                    |
| 2018-07-20 01:04:24 UTC+0900 | INFO | Deleted EIP: 52.32.168.228                                                                                                                                                                                                                                                                                 |
| 2018-07-20 01:04:03 UTC+0900 | INFO | Environment health has transitioned from Ok to Info. Command is executing on 1 out of 2 instances.                                                                                                                                                                                                         |
| 2018-07-20 01:04:03 UTC+0900 | INFO | Added instance [i-0c1ca78e86ab24452] to your environment.                                                                                                                                                                                                                                                  |
| 2018-07-20 01:03:51 UTC+0900 | INFO | Updated Deployrubyapp-env.c3tiqqda3p.us-west-2.elasticbeanstalk.com to point to awseb-e-j-AWSEBLoa-1JSYUKA9VLEVM-1442706645.us-west-2.elb.amazonaws.com. Your application might be unavailable for a few minutes while the changes propagate.                                                              |
| 2018-07-20 01:03:47 UTC+0900 | INFO | Created CloudWatch alarm named: awseb-e-ja5xfeyjzm-stack-AWSEBCloudwatchAlarmHigh-1ANVPVAK5KP6R                                                                                                                                                                                                            |
| 2018-07-20 01:03:47 UTC+0900 | INFO | Created CloudWatch alarm named: awseb-e-ja5xfeyjzm-stack-AWSEBCloudwatchAlarmLow-ADTDTV62PLFT                                                                                                                                                                                                              |
| 2018-07-20 01:03:47 UTC+0900 | INFO | Created Auto Scaling group policy named: arn:aws:autoscaling:us-west-2:398383393881:scalingPolicy:961e0e61-38cd-4575-acd0-da8738f9e2a8:autoScalingGroupName/awseb-e-ja5xfeyjzm-stack-AWSEBAutoScalingGroup-1MKGKY1L4TFRB:policyName/awseb-e-ja5xfeyjzm-stack-AWSEBAutoScalingScaleUpPolicy-1W0QUTPNYQ6BF   |
| 2018-07-20 01:03:47 UTC+0900 | INFO | Created Auto Scaling group policy named: arn:aws:autoscaling:us-west-2:398383393881:scalingPolicy:21b47850-c88a-4aea-93ce-62b013837757:autoScalingGroupName/awseb-e-ja5xfeyjzm-stack-AWSEBAutoScalingGroup-1MKGKY1L4TFRB:policyName/awseb-e-ja5xfeyjzm-stack-AWSEBAutoScalingScaleDownPolicy-1XFU9XGFSDB6P |
| 2018-07-20 01:00:58 UTC+0900 | INFO | Created load balancer named: awseb-e-j-AWSEBLoa-1JSYUKA9VLEVM                                                                                                                                                                                                                                              |
| 2018-07-20 01:00:58 UTC+0900 | INFO | Created security group named: sg-dd0666ad                                                                                                                                                                                                                                                                  |
| 2018-07-20 01:00:42 UTC+0900 | INFO | Updating environment Deployrubyapp-env's configuration settings.                                                                                                                                                                                                                                           |
| 2018-07-20 01:00:34 UTC+0900 | INFO | Environment update is starting.                                                                                                                                                                                                                                                                            |
| 2018-07-20 00:52:58 UTC+0900 | INFO | Successfully launched environment: Deployrubyapp-env                                                                                                                                                                                                                                                       |
| 2018-07-20 00:52:04 UTC+0900 | INFO | Environment health has transitioned from Pending to Ok. Initialization completed 1 second ago and took 12 minutes.                                                                                                                                                                                         |
| 2018-07-20 00:51:19 UTC+0900 | INFO | Waiting for EC2 instances to launch. This may take a few minutes.                                                                                                                                                                                                                                          |
| 2018-07-20 00:51:04 UTC+0900 | INFO | Added instance [i-0be9dc6592c5d3b51] to your environment.                                                                                                                                                                                                                                                  |
| 2018-07-20 00:49:42 UTC+0900 | INFO | Created RDS database named: aaonilgo1343gd                                                                                                                                                                                                                                                                 |
| 2018-07-20 00:40:26 UTC+0900 | INFO | Created EIP: 52.32.168.228                                                                                                                                                                                                                                                                                 |
| 2018-07-20 00:40:11 UTC+0900 | INFO | Creating RDS database named: aaonilgo1343gd. This may take a few minutes.                                                                                                                                                                                                                                  |
| 2018-07-20 00:40:11 UTC+0900 | INFO | Created security group named: awseb-e-ja5xfeyjzm-stack-AWSEBSecurityGroup-ZA3RYT7KZTYA                                                                                                                                                                                                                     |
| 2018-07-20 00:40:05 UTC+0900 | INFO | Environment health has transitioned to Pending. Initialization in progress (running for 2 seconds). There are no instances.                                                                                                                                                                                |
| 2018-07-20 00:39:44 UTC+0900 | INFO | Using elasticbeanstalk-us-west-2-398383393881 as Amazon S3 storage bucket for environment data.                                                                                                                                                                                                            |
| 2018-07-20 00:39:42 UTC+0900 | INFO | createEnvironment is starting.                                                                                                                                                                                                                                                                             |
