# OCP4 Helper Node

The main target of this playbook is to prepare the helper node to install OCP4 using Installer Provisioned Installation (IPI). This is achieved by doining the folloing, respectively:

1. Generate the SSH keys
2. Install the necessary packages
3. Configure DHCP
4. Configure DNS (forward zones, backword zones)
5. Configure the firewall
6. Install the Openshift CLI **(oc)** client
7. Install the Openshift Installer **(openshift-install)**
8. Download the vCenter certificates and install them in the trust store
9. Create and installation directory
10. Create the **install-config**

Optionally, it also creates:
1. HA Proxy for future use, i frequired
2. NFS configuration for NFS persistent volume for the registry
3. Registry resources



Below is a highlevel diagram how the ocp4-helpernode fits into your network.

![ocp4-helpernode](docs/images/hn.png)


# Using this playbook

The following are highlevel steps on how to use this playbook. There are more detailed instructions in the ["quickstarts"](#quickstarts) section.

## Prereqs

Install a RHEL server with this recommended setup:

* 4 vCPUs
* 4 GB of RAM
* 30GB HD
* Static IP


Once the base OS is installed, install `ansible` and `git`, then clone this repo and check out to your branch `KIO-networks`.

```
yum -y install ansible git
git clone https://github.com/mohzaher2000/ocp4-helpernode.git
git checkout KIO-networks
cd ocp4-helpernode
```
Alternatively you can install [EPEL](https://fedoraproject.org/wiki/EPEL) if you don't want to connect to the Red Hat Subscription Manager, for now. Next install `ansible` and `git`, then clone this repo.


```
yum -y install https://dl.fedoraproject.org/pub/epel/epel-release-latest-$(rpm -E %rhel).noarch.rpm
yum -y install ansible git
git clone https://github.com/mohzaher2000/ocp4-helpernode.git
git checkout KIO-networks
cd ocp4-helpernode
```

## Setup your Environment Vars

In the project there is a [vars-ipi.yaml](docs/examples/vars-ipi.yaml) file under `docs/examples/var.yaml` ... **__modify it__** to match your network and the environment. 

> :warning: **NOTE**, currently this playbook assumes/is limited to a `/24` network

See the `vars.yaml` [documentation page](docs/vars-doc.md) for more info about what you can define. There are different options, depending on what you're doing. For example, if you're doing a static ip install vs a dhcp install.


## Run the playbook

Once you edited your `vars.yaml` file; run the playbook

```
ansible-playbook -e @vars.yaml tasks/main.yml
```

## Helper Script

You can run this script and it's options to display helpful information about the install and other post-install goodies.

```
/usr/local/bin/helpernodecheck
```

## Install OpenShift 4 UPI

Now you're ready to follow the [OCP4 UPI install doc](https://docs.openshift.com/container-platform/latest/installing/installing_bare_metal/installing-bare-metal.html#ssh-agent-using_installing-bare-metal)


# Quickstarts

The following are quickstarts. These are written using libvirt, but are generic enough to be used in BareMetal or other Virtualized Environments.


* Bare Metal DHCP install [quickstart](docs/bmquickstart.md)
* Bare Metal Static IPs install [quickstart](docs/bmquickstart-static.md)
* Libvirt DHCP install [quickstart](docs/quickstart.md)
* Libvirt Static IPs install [quickstart](docs/quickstart-static.md)
* DHCP install on KVM/Power [quickstart](docs/quickstart-ppc64le.md)
* DHCP install on PowerVM [quickstart](docs/quickstart-powervm.md)
* OCP4 on VMware vSphere UPI Automation [quickstart](https://github.com/RedHatOfficial/ocp4-vsphere-upi-automation)
* A Video "how-to" done on a [Twitch Stream](docs/yt-twitch.md)

# Contributing

Please see the [contributing doc](docs/contribute.md) for more details.
