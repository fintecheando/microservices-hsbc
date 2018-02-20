# 1. Install OpenShift on CentOS 7

Reference from this page https://www.server-world.info/en/note?os=CentOS_7&p=openshift


Install OpenShift Origin which is the Open Source version of Red Hat OpenShift.
This example is based on the environment like follows.
           +-------------------------------------+---------------------------------+
           |192.168.188.133                      |192.168.188.131                  |192.168.188.130
+----------+-------------------+      +----------+---------------+      +----------+---------------+
|  [kmaster.mx.fintecheando ]  |      | [ kn01.mx.fintecheando ] |      | [ kn01.mx.fintecheando ] |
|     (Master Node)            |      |    (Compute Node)        |      |    (Compute Node)        |
|     (Compute Node)           |      |                          |      |                          |
+------------------------------+      +--------------------------+      +--------------------------+

 	
There are some System requirements to configure cluster.
  * Master node has up to 16G memory.
  * On all nodes, free space on physical volume is required to create a new volume group for Docker Direct LVM.

# [1]	On All Nodes, Create a user for installation to be used in Ansible and also grant root privileges to him.
  
```bash
[root@kmaster ~]# useradd origin 
[root@kmaster ~]# passwd origin 
[root@kmaster ~]# echo -e 'Defaults:origin !requiretty\norigin ALL = (root) NOPASSWD:ALL' | tee /etc/sudoers.d/openshift 
[root@kmaster ~]# chmod 440 /etc/sudoers.d/openshift 
# if Firewalld is running, allow SSH
[root@kmaster ~]# firewall-cmd --add-service=ssh --permanent 
[root@kmaster ~]# firewall-cmd --reload 

```

[2]	On All Nodes, install OpenShift Origin 3.6 repository and Docker.
Next, create a volume group for Docker Direct LVM to setup LVM Thinpool like follows.
Reference from this page https://docs.docker.com/storage/storagedriver/device-mapper-driver/#configure-direct-lvm-mode-for-production
Reference from this page https://docs.docker.com/install/linux/linux-postinstall/#manage-docker-as-a-non-root-user
```bash
[root@dlp ~]# yum -y install centos-release-openshift-origin36 docker
[root@dlp ~]# vgcreate centos /dev/sda2
Volume group "centos" successfully created
[root@dlp ~]# echo VG=centos >> /etc/sysconfig/docker-storage-setup 
[root@dlp ~]# systemctl start docker 
[root@dlp ~]# systemctl enable docker 
```


[3]	On Master Node, login with a user created above and set SSH keypair with no pass-phrase
```bash
[origin@kmaster ~]$ ssh-keygen -q -N "" 
Enter file in which to save the key (/home/origin/.ssh/id_rsa):
[origin@kmaster ~]$ vi ~/.ssh/config
# create new ( define nodes )
Host kmaster
    Hostname kmaster.mx.fintecheando
    User origin
Host kn01
    Hostname kn01.mx.fintecheando
    User origin
Host kn02
    Hostname kn02.mx.fintecheando
    User origin

[origin@kmaster ~]$ chmod 600 ~/.ssh/config
# transfer public-key to another node
[origin@kmaster ~]$ ssh-copy-id kn01 
origin@kn01.mx.fintecheando's password: 

Number of key(s) added: 1

Now try logging into the machine, with:   "ssh 'kn01'"
and check to make sure that only the key(s) you wanted were added.

[origin@kmaster ~]$ ssh-copy-id kn02 
```

[4]	On Master Node, login with a user created above and run Ansible Playbook for setting up OpenShift Cluster.
I had to do some trikcs editing the minimum requirements Reference from this file https://github.com/openshift/openshift-ansible/blob/master/roles/openshift_health_checker/openshift_checks/memory_availability.py 
```bash
[origin@kmaster ~]$ sudo vi /etc/ansible/hosts
# add follows to the end
[OSEv3:children]
masters
nodes

[OSEv3:vars]
# admin user created in previous section
ansible_ssh_user=origin
ansible_become=true
openshift_deployment_type=origin

# use HTPasswd for authentication
openshift_master_identity_providers=[{'name': 'htpasswd_auth', 'login': 'true', 'challenge': 'true', 'kind': 'HTPasswdPasswordIdentityProvider', 'filename': '/etc/origin/master/.htpasswd'}]
openshift_master_default_subdomain=apps.mx.fintecheando

# allow unencrypted connection within cluster
openshift_docker_insecure_registries=172.30.0.0/16

[masters]
kmaster.mx.fintecheando openshift_schedulable=true containerized=false

[etcd]
kmaster.mx.fintecheando

[nodes]
# set labels [region: ***, zone: ***] (any name you like)
kmaster.mx.fintecheando openshift_node_labels="{'region': 'infra', 'zone': 'default'}"
kn01.mx.fintecheando openshift_node_labels="{'region': 'primary', 'zone': 'chapultepec'}" openshift_schedulable=true
kn02.mx.fintecheando openshift_node_labels="{'region': 'primary', 'zone': 'toluca'}" openshift_schedulable=true    

[origin@kmaster ~]$ ansible-playbook /usr/share/ansible/openshift-ansible/playbooks/byo/config.yml 
2017-11-23 19:17:14,120 p=1889 u=root |  PLAY [Create initial host groups for localhost] 
2017-11-23 19:17:14,127 p=1889 u=root |  TASK [include_vars] ****************************

................
................

PLAY RECAP ****************************************************************
kmaster.mx.fintecheando    : ok=643  changed=172  unreachable=0    failed=0   
kn01.mx.fintecheando       : ok=248  changed=52   unreachable=0    failed=0   
kn02.mx.fintecheando       : ok=248  changed=51   unreachable=0    failed=0   
localhost                  : ok=12   changed=0    unreachable=0    failed=0  

# show state
[origin@kmaster ~]$ oc get nodes
NAME                      STATUS    AGE       VERSION
kmaster.mx.fintecheando   Ready     1h        v1.6.1+5115d708d7
kn01.mx.fintecheando      Ready     1h        v1.6.1+5115d708d7
kn02.mx.fintecheando      Ready     1h        v1.6.1+5115d708d7

# show state with labels
[origin@kmaster ~]$ oc get nodes --show-labels=true
NAME                      STATUS    AGE       VERSION             LABELS
kmaster.mx.fintecheando   Ready     1h        v1.6.1+5115d708d7   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/hostname=kmaster.mx.fintecheando,region=infra,zone=default
kn01.mx.fintecheando      Ready     1h        v1.6.1+5115d708d7   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/hostname=kn01.mx.fintecheando,region=primary,zone=chapultepec
kn02.mx.fintecheando      Ready     1h        v1.6.1+5115d708d7   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/hostname=kn02.mx.fintecheando,region=primary,zone=toluca
```

[NOTES]	FYI

```bash
[origin@kmaster ~]$ sudo docker info
Containers: 4
 Running: 4
 Paused: 0
 Stopped: 0
Images: 4
Server Version: 1.12.6
Storage Driver: devicemapper
 Pool Name: centos-docker--pool
 Pool Blocksize: 524.3 kB
 Base Device Size: 10.74 GB
 Backing Filesystem: xfs
 Data file: 
 Metadata file: 
 Data Space Used: 2.155 GB
 Data Space Total: 3.095 GB
 Data Space Available: 940.6 MB
 Metadata Space Used: 430.1 kB
 Metadata Space Total: 16.78 MB
 Metadata Space Available: 16.35 MB
 Thin Pool Minimum Free Space: 309.3 MB
 Udev Sync Supported: true
 Deferred Removal Enabled: true
 Deferred Deletion Enabled: true
 Deferred Deleted Device Count: 0
 Library Version: 1.02.140-RHEL7 (2017-05-03)
Logging Driver: journald
Cgroup Driver: systemd
Plugins:
 Volume: local
 Network: overlay null host bridge
Swarm: inactive
Runtimes: docker-runc runc
Default Runtime: docker-runc
Security Options: seccomp selinux
Kernel Version: 3.10.0-693.17.1.el7.x86_64
Operating System: CentOS Linux 7 (Core)
OSType: linux
Architecture: x86_64
Number of Docker Hooks: 3
CPUs: 2
Total Memory: 2.73 GiB
Name: kmaster.mx.fintecheando
ID: SQAA:XZRA:HFLK:B7AI:TWN4:WKLK:YZ3T:CYX7:BOMN:SNVE:JQZL:DCBT
Docker Root Dir: /var/lib/docker
Debug Mode (client): false
Debug Mode (server): false
Registry: https://index.docker.io/v1/
WARNING: bridge-nf-call-iptables is disabled
WARNING: bridge-nf-call-ip6tables is disabled
Insecure Registries:
 172.30.0.0/16
 127.0.0.0/8
Registries: docker.io (secure)
```
