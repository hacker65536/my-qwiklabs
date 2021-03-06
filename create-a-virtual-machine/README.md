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
```console
root@gcelab:~# ps auxw|grep nginx
root      2181  0.0  0.0 159504  1628 ?        Ss   15:33   0:00 nginx: master process /usr/sbin/nginx -g daemon on
; master_process on;
www-data  2182  0.0  0.0 159840  3408 ?        S    15:33   0:00 nginx: worker process
root      2211  0.0  0.0  12784   968 pts/0    S+   15:34   0:00 grep nginx
```

click ExternalIP from Google console(webUI) and check webpage

## Create new instance with gcloud

cloud shell
```console
google760785_student@cloudshell:~ (qwiklabs-gcp-c978845dd406cca9)$ gcloud compute instances create gcelab2 --zone us-central1-c
Created [https://www.googleapis.com/compute/v1/projects/qwiklabs-gcp-c978845dd406cca9/zones/us-central1-c/instances/gcelab2].
NAME     ZONE           MACHINE_TYPE   PREEMPTIBLE  INTERNAL_IP  EXTERNAL_IP   STATUS
gcelab2  us-central1-c  n1-standard-1               10.128.0.3   35.194.57.72  RUNNING
```

try following command
`gcloud compute instances create --help`  
`gcloud config set compute/zone ...`  
`gcloud config set compute/region ...`


SSH into vm using `gcloud`

Enter through the passphrase section to leave the passphrase empty.

```console
google760785_student@cloudshell:~ (qwiklabs-gcp-c978845dd406cca9)$ gcloud compute ssh gcelab2 --zone us-central1-c
WARNING: The public SSH key file for gcloud does not exist.
WARNING: The private SSH key file for gcloud does not exist.
WARNING: You do not have an SSH key for gcloud.
WARNING: SSH keygen will be executed to generate a key.
This tool needs to create the directory
[/home/google760785_student/.ssh] before being able to generate SSH
keys.
Do you want to continue (Y/n)?  Y
Generating public/private rsa key pair.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/google760785_student/.ssh/google_compute_engine.
Your public key has been saved in /home/google760785_student/.ssh/google_compute_engine.pub.
The key fingerprint is:
SHA256:+65UuIjzKVoS5hqnPnyKIxbkLX5/G9JXrDZdinji748 google760785_student@cs-6000-devshell-vm-41acdc49-f140-400a-bcc6-61427883ea7f
The key's randomart image is:
+---[RSA 2048]----+
|                 |
|                 |
|                 |
| .       ..      |
|o +     S .o .   |
| * o ....+= o    |
|+ * +..=+B o     |
|+X =.oo+*.o      |
|B+*..o+o=E+.     |
+----[SHA256]-----+
Updating project ssh metadata...⠶Updated [https://www.googleapis.com/compute/v1/projects/qwiklabs-gcp-c978845dd406cca9].
Updating project ssh metadata...done.
Waiting for SSH key to propagate.
Warning: Permanently added 'compute.4146277858329574029' (ECDSA) to the list of known hosts.
Linux gcelab2 4.9.0-7-amd64 #1 SMP Debian 4.9.110-1 (2018-07-05) x86_64
The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.
Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
google760785_student@gcelab2:~$
```

via webUI (click SSH: open in browser window)
```console
Connected, host fingerprint: ssh-rsa 2048 7C:C9:74:7B:13:7B:B0:11:FA:62:2F:47:D2:0F:72:88:11:5B:B9:BB:11:18:95:6A:F
5:E3:75:58:EE:D6:AC:41
Linux gcelab2 4.9.0-7-amd64 #1 SMP Debian 4.9.110-1 (2018-07-05) x86_64
The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.
Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
Last login: Tue Jul 31 15:52:48 2018 from 35.234.17.38
google760785_student@gcelab2:~$ w
 15:54:40 up 7 min,  2 users,  load average: 0.00, 0.00, 0.00
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
google76 pts/0    35.234.17.38     15:52   14.00s  0.00s  0.00s -bash
google76 pts/1    74.125.41.162    15:54    0.00s  0.00s  0.00s w
```
via cloud chell
```console
google760785_student@gcelab2:~$ w
 15:54:42 up 7 min,  2 users,  load average: 0.00, 0.00, 0.00
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
google76 pts/0    35.234.17.38     15:52    0.00s  0.00s  0.00s w
google76 pts/1    74.125.41.162    15:54    2.00s  0.00s  0.00s -bash
```
