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
