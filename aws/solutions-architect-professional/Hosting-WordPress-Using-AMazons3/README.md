# Hosting WordPress Using Amazon S3
- 8Credits
- 1:55:00

## Configure WordPress on Amazon EC2

- PublicIP 52.26.37.226
- WordPressURL http://ec2-52-26-37-226.us-west-2.compute.amazonaws.com/wordpress
- StaticURL http://ec2-52-26-37-226.us-west-2.compute.amazonaws.com/wordpress/wordpress-static/index.html

access to WordPressURL

- Site Title: anytitle
- Username: student
- Password: student123
- Confirm Password: yes(weak)
- Your Email: student@example.com
- Serach Engine Visiblity: Do not change

log in

add new post and publish.

## Create an Amazon S3 Static Website

create bucket from console, and named such as `wordpress-xdf30`.

Properties -> Static website hosting

- index document : index.html
- Error document: error.html

## login to EC2 instance
download key(PEM or PPK)

mac 
```console
$ chmod 600 ~/Downloads/qwikLABS-L73-3221011.pem  
$ ssh -i  ~/Downloads/qwikLABS-L73-3221011.pem  -l ec2-user 52.26.37.226
```

## generate a static version of wordpress

allow the apache web server to allow permlinks override.
```console 
$ sudo sed -i.bak -e 's/AllowOverride None/AllowOverride All/g' /etc/httpd/conf/httpd.conf;
```
restart
```console 
$ sudo service httpd restart
 ```
 
 ```
$ cd /var/www/html/wordpress
$ sudo wget https://us-west-2-aws-training.s3.amazonaws.com/awsu-spl/spl-39/scripts/wpstatic.sh
$ sudo /bin/sh wpstatic.sh -a
```
