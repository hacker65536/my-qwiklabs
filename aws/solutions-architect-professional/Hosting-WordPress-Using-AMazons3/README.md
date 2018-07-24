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

```
Don't forget to change the theme files to limit comment, RSS, meta, and login links, and search fields.
--2018-07-24 14:18:54--  http://ec2-52-26-37-226.us-west-2.compute.amazonaws.com/wordpress/
Resolving ec2-52-26-37-226.us-west-2.compute.amazonaws.com (ec2-52-26-37-226.us-west-2.compute.amazonaws.com)... 172.31.40.236
Connecting to ec2-52-26-37-226.us-west-2.compute.amazonaws.com (ec2-52-26-37-226.us-west-2.compute.amazonaws.com)|172.31.40.236|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: unspecified [text/html]
Saving to: 'wordpress-static/index.html'

index.html              [ <=>                ]  54.19K  --.-KB/s    in 0.02s

Last-modified header missing -- time-stamps turned off.
2018-07-24 14:18:55 (2.62 MB/s) - 'wordpress-static/index.html' saved [55487]

Loading robots.txt; please ignore errors.
------snip--------
Downloaded: 38 files, 1.1M in 0.2s (5.40 MB/s)
Converting links in wordpress-static/index.html?p=1.html... 36-2
Converting links in wordpress-static/index.php/2018/07/24/hello-world/index.html?replytocom=1.html... 37-2
Converting links in wordpress-static/wp-login.php.html... 4-1
Converting links in wordpress-static/index.php/2018/07/index.html... 27-2
Converting links in wordpress-static/index.html?p=6.html... 34-2
Converting links in wordpress-static/index.html... 28-2
Converting links in wordpress-static/index.php/2018/07/24/my-title/index.html... 34-2
Converting links in wordpress-static/wp-login.php?action=lostpassword.html... 4-1
Converting links in wordpress-static/index.php/2018/07/24/hello-world/index.html... 36-2
Converting links in wordpress-static/index.php/author/student/index.html... 28-2
Converting links in wordpress-static/wp-admin/load-styles.php?c=1&dir=ltr&load%5B%5D=dashicons,buttons,forms,l10n,login&ver=4.9.7.css... 7-0
Converting links in wordpress-static/wp-content/themes/twentyseventeen/style.css?ver=4.9.7.css... nothing to do.
Converted links in 12 files in 0.009 seconds.
```

```
sudo chown -R apache:apache /var/www/html/wordpress
```
```
# Determine Region
AZ=`curl --silent http://169.254.169.254/latest/meta-data/placement/availability-zone/`
REGION=${AZ::-1}

# Retrieve Amazon S3 bucket name starting with wordpress-*
BUCKET=`aws s3api list-buckets --query "Buckets[?starts_with(Name, 'wordpress-')].Name | [0]" --output text`
```
```
$ echo $AZ
us-west-2a
$ echo $BUCKET
wordpress-bj92
```
