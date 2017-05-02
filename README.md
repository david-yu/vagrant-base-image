Vagrant Virtualbox setup for Docker EE Engine on CentOS 7.3
========================

An exercise on installing Docker EE Engine and properly configuring Device Mapper on CentOS, which may be helpful for walking through the install and configuration of Docker EE Engine before actually doing so in production environments. This vagrant file is provided strictly for educational purposes.

## Download vagrant from Vagrant website

```
https://www.vagrantup.com/downloads.html
```

## Install Virtual Box

```
https://www.virtualbox.org/wiki/Downloads
```

## Download CentOS 7 box
```
vagrant init centos/7
```

## Create files in project to store environment variables with custom values for use by Vagrant
```
ee_url
```

## Bring up nodes

```
vagrant up centos-node
```

### Validate Docker Device Mapper Config

After properly configuring Docker with Device Mapper:

```
[vagrant@centos-node ~]$ docker info
Containers: 0
 Running: 0
 Paused: 0
 Stopped: 0
Images: 0
Server Version: 1.13.1-cs2
Storage Driver: devicemapper
 Pool Name: docker-thinpool
 Pool Blocksize: 524.3 kB
 Base Device Size: 10.74 GB
 Backing Filesystem: xfs
 Data file:
 Metadata file:
 Data Space Used: 19.92 MB
 Data Space Total: 3.997 GB
 Data Space Available: 3.977 GB
 Metadata Space Used: 40.96 kB
 Metadata Space Total: 41.94 MB
 Metadata Space Available: 41.9 MB
 Thin Pool Minimum Free Space: 399.5 MB
 Udev Sync Supported: true
 Deferred Removal Enabled: true
 Deferred Deletion Enabled: true
 Deferred Deleted Device Count: 0
 Library Version: 1.02.135-RHEL7 (2016-09-28)
Logging Driver: json-file
Cgroup Driver: cgroupfs
...
```

## Stop nodes

```
vagrant halt centos-node
```

## Destroy nodes

```
vagrant destroy centos-node
```
