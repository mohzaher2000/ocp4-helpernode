# Helper Node Quickstart Install

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
1. HA Proxy for future use, if required
2. NFS configuration for NFS persistent volume for the registry, if required
3. Resources for internal registry creation

