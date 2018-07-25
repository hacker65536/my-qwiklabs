# Introduction to Amazon Aurora
- 1Credit
- 1:30

## Create an Amazon Aurora Instance

Launch DB instance

- DB instance class: db.t2.medium
- Multi-AZ: NO
- DB instance identifier: aurora
- Master username: master
- Master password: master123
- Confirm password: master123
- VPC: LabVPC
- Subnet group: aurora 
- VPC security groups: chooose existing VPC sg ( has rds in it's name like rds-qls-*)
- DB Cluster Identifier: aurora
- Database name: mydb
- Encryption: Disable encryption
- Monitoring: Disable enhanced monitoring
- Maintenance: Disable auto minor version upgrade

Launch DB instance

already launching from cloudformation?
## Connect to Amazon EC2 Windows instance
