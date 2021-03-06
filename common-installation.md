<p align="center"><img src="https://github.com/sonata-nfv/tng-api-gtw/wiki/images/sonata-5gtango-logo-500px.png" /></p>

# 5GTANGO Service Platform installation guide

The 5GTANGO system consists of the Service Platform for deploying and orchestrating services and the Service Development Kit to create deployable service packages. Between the service development and Production, we have a tool for Validate and Verify the Network Service. This tool is called VnV and helps develpers to create a set of test to run it in an automatically way against network services. 

## Prerequisites

* [Linux ubuntu = 16.04](http://releases.ubuntu.com/16.04/)
* [ansible > 2.4](https://docs.ansible.com/ansible/2.4/intro_installation.html#latest-releases-via-apt-ubuntu)
* [docker > 17.12.0-ce](https://docs.docker.com/install/linux/docker-ce/ubuntu/#install-docker-ce)
* [docker-py = 1.9.0](https://pypi.org/project/docker/)
* [Git](https://git-scm.com/download/linux)

### Recommended server specs to run SONATA Service Platform

* **Cpu:** 4 cores
* **Ram:** 8 GB
* **Hdd:** 80 GB

### Ansible installation

```bash
sudo apt-get update
sudo apt-get install software-properties-common
sudo apt-add-repository ppa:ansible/ansible
sudo apt-get update
sudo apt-get install ansible
```

### Docker installation

```bash
sudo apt-get update
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
sudo apt-get update
sudo apt-get install docker-ce
```

### Python-docker installation

```bash
sudo apt-get install python3 python3-pip pip
pip install docker
```

[In case of this error](https://stackoverflow.com/questions/14547631/python-locale-error-unsupported-locale-setting)

```bash
"Traceback (most recent call last):
  File "/usr/bin/pip3", line 11, in <module>
    sys.exit(main())
  File "/usr/lib/python3/dist-packages/pip/__init__.py", line 215, in main
    locale.setlocale(locale.LC_ALL, '')
  File "/usr/lib/python3.5/locale.py", line 594, in setlocale
    return _setlocale(category, locale)
locale.Error: unsupported locale setting
"
```

It can be fixed with:

```bash
export LC_ALL="en_US.UTF-8"
export LC_CTYPE="en_US.UTF-8"
sudo dpkg-reconfigure locales
```

### Git installation

```bash
sudo apt-get install git
```

### Cloning the tng-devops repository

```bash
git clone https://github.com/sonata-nfv/tng-devops.git
cd tng-devops/
```

## SONATA Installation

To use the last stable version of SONATA you need to change the branch to v4.0. That can be performed being inside `tng-devops` folder, with the command:
`git checkout v4.0`

### Creating docker network to allocate the containers

```bash
sudo docker network create tango
```