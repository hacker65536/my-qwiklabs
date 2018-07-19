# Working with AWS Elastic Beanstalk

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
