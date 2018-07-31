# Creating a Virtual Machine
- 1credis
- 00:30:00

## setup

copy id and password for google ccount and paste it to log in to google cloud console

accept agreement

start cloud shell


```console
Welcome to Cloud Shell! Type "help" to get started.
Your Cloud Platform project in this session is set to qwiklabs-gcp-95a24cb4ec107945.
Use “gcloud config set project [PROJECT_ID]” to change to a different project.
google760663_student@qwiklabs-gcp-95a24cb4ec107945:~$ gcloud auth list
          Credentialed Accounts
ACTIVE  ACCOUNT
*       google760663_student@qwiklabs.net
To set the active account, run:
    $ gcloud config set account `ACCOUNT`
google760663_student@qwiklabs-gcp-95a24cb4ec107945:~$
```

```console
google760663_student@qwiklabs-gcp-95a24cb4ec107945:~$ gcloud config list project
[core]
project = qwiklabs-gcp-95a24cb4ec107945
Your active configuration is: [cloudshell-17670]
```

## Create a new instance from the cloud console

menu -> Compute Engine -> VM instances

create an instance
- name: gcelab
- region: us-central1(lowa)
- zone: us-central1-c
- Machine type: 1vCPU (3.75GB memory)
- Boot disk: New 10GB 
  - Image Debian GNU/Linux9(stretch)
- Firewall
 - [x] Allow HTTP trafic
 
 click create
 
 when finished, click _SSH_ to into the VM
 
 ```console
 Connected, host fingerprint: ssh-rsa 2048 41:69:FB:F5:AD:86:6C:9B:1B:33:B6:A5:BE:97:DC:B6:E5:6E:3F:03:FD:B2:ED:C1:1
C:78:E8:DE:61:69:A1:23
Linux gcelab 4.9.0-7-amd64 #1 SMP Debian 4.9.110-1 (2018-07-05) x86_64
The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.
Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
google760663_student@gcelab:~$ 
```
```console
oogle760663_student@gcelab:~$ sudo su -
root@gcelab:~# apt-get update
---snip---
Fetched 1,304 kB in 2s (584 kB/s)
Reading package lists... Done
```


```console
root@gcelab:~# apt-get install nginx -y
Reading package lists... Done
Building dependency tree       
---snip----
Setting up nginx (1.10.3-1+deb9u1) ...
Processing triggers for libc-bin (2.24-11+deb9u3) ...
Processing triggers for sgml-base (1.29) ...
```
