############
Installation
############

There are three component included in the Chef setup.

1. Chef server - it works as a central repository for cookbooks.  

2. Chef workstations - it is used to create cookbooks. 

3. Chef client - it is installed on the switch. 

Chef server and workstation can be installed on a standalone server that has connectivity to all the Dell EMC Networking devices that need to be managed under Chef (see https://www.chef.io).

Setup verification 
******************

Fetch configuration.

    knife ssl fetch

Test the configuration.

    knife client list

Bootstrap a new node with the knife command
*******************************************

    knife bootstrap node_domain_or_IP -N testing -x demo -P password --sudo --use-sudo-password

For example, ``knife bootstrap 10.16.204.64 -N testing64 -x linuxadmin -P linuxadmin --sudo --use-sudo-password``

Devops Ruby utils Debian package installation
#############################################

The ``os10_devops_infra_install.sh`` script installs the dependency for the Chef client. The prerequisite for this installation is that the user ``os10devops`` should have been created with role as sysadmin (for example, use the username command in CONF mode in the OS10 CLI).
  
.. code-block:: bash
  
      OS10(config)#username os10devops password <password_str> role sysadmin

Download the ``os10_devops_infra_install.sh`` script in the switch from https://raw.githubusercontent.com/Dell-Networking/dellos10-ruby-utils/master/os10_devops_infra_install.sh. User can use ''wget'' or a curl utility.
After downloading the script, change the permission using the ``chmod +x os10_devops_infra_install.sh`` command. Execute the ``os10_devops_infra_install.sh`` script to install devops Ruby utilities Debian package.
    
Usage
-----
.. code-block:: bash

    $ os10_devops_infra_install.sh chef_ruby_utils active_partition local/remote <os10_devops_ruby_utils_url>

Options
~~~~~~~

- chef_ruby_utils: first option should be always the ''chef_ruby_utils'' string; Chef client should be already installed in the switch before installing devops ruby utils debian package for chef_ruby_utils option
- active_partition: denotes the installation will happen in an active partition
- local: denotes the relative path in the switch
  - remote: denotes the relative path in the remote machine using protocols like HTTPS, FTP, and so on
- <os10_devops_ruby_utils_url>: devops Ruby utilites URL link from GitHub if the previous option is remote (for example, https://raw.githubusercontent.com/Dell-Networking/dellos10-ruby-utils/master/os10-devops-ruby-utils-1.0.0.deb)
  - <os10_devops_ruby_utils_url>: download the os10-devops-ruby-utils-1.0.0.deb package in the local path of the switch if previous option is local (for example, /home/admin/)

Sample usage
------------

    ./os10_devops_infra_install.sh chef_ruby_utils active_partition remote https://raw.githubusercontent.com/Dell-Networking/dellos10-ruby-utils/master/os10-devops-ruby-utils-1.0.0.deb
  
OR
  
    ./os10_devops_infra_install.sh chef_ruby_utils active_partition remote "-u ftp:ftp  ftp://<remote_ip>://<path>/os10-devops-ruby-utils-1.0.0.deb"
  
OR
  
    ./os10_devops_infra_install.sh chef_ruby_utils active_partition local /home/admin/

Chef client installation after an image upgrade
###############################################
When an OS10 image is upgraded manually or through Chef recipe, the Chef client will not be automatically installed in the upgraded partition. The prerequisite for this installation is the Chef should have been configured in the loaded partition (for example, the node should have been bootstrapped and the devops Ruby utilites Debian package should have been installed).

Download the ``os10_devops_infra_install.sh`` script in the switch from https://raw.githubusercontent.com/Dell-Networking/dellos10-ruby-utils/master/os10_devops_infra_install.sh. After downloading the script, change the permission using the ``chmod +x os10_devops_infra_install.sh`` command. Execute the ``os10_devops_infra_install.sh`` script to install Chef and the devops Ruby utilities Debian package in the upgraded partition.

Usage
-----

.. code-block:: bash

    $ os10_devops_infra_install.sh chef standby_partition local/remote <chef_client_url> local/remote <os10_devops_ruby_utils_url>

Options
~~~~~~~

- chef: first option should be always the string 'chef'
- standby_partition: denotes the installation will happen in standby partition
- local: denotes the relative path in the switch
  - remote: denotes the relative path in the remote machine using protocols like HTTPS, FTP, and so on
- <chef_client_url>: Chef url should be an HTTPS/FTP path if previous option is remote (for example, https://packages.chef.io/files/stable/chef/13.8.5/debian/8/chef_13.8.5-1_amd64.deb)
  - <chef_client_url>: download the ``chef_13.8.5-1_amd64.deb`` package in the local path of the switch if previous option is local (for example, /home/admin/)
- <os10_devops_ruby_utils_url>: devops ruby utils URL link from GitHub if the previous option is remote (for example, https://raw.githubusercontent.com/Dell-Networking/dellos10-ruby-utils/master/os10-devops-ruby-utils-1.0.0.deb)
  - <os10_devops_ruby_utils_url>: download the ``os10-devops-ruby-utils-1.0.0.deb`` package in the local path of the switch if previous option is local (for example, /home/admin/)
  
Sample usage
------------

    ./os10_devops_infra_install.sh chef standby_partition remote https://packages.chef.io/files/stable/chef/13.8.5/debian/8/chef_13.8.5-1_amd64.deb remote https://raw.githubusercontent.com/Dell-Networking/dellos10-ruby-utils/master/os10-devops-ruby-utils-1.0.0.deb
  
OR
  
    ./os10_devops_infra_install.sh chef standby_partition remote "-u ftp:ftp  ftp://<remote_ip>://<path>/chef_13.8.5-1_amd64.deb" remote "-u ftp:ftp  ftp://<remote_ip>://<path>/os10-devops-ruby-utils-1.0.0.deb"
  
OR
  
    ./os10_devops_infra_install.sh chef standby_partition local /home/admin local /home/admin
  
> **NOTE**: After the image upgrade and reload, execute any Chef resource. If the Chef client gives the LoadError "cannot load such file -- xml/libxml", execute the ``/opt/chef/embedded/bin/gem install libxml-ruby`` below command in root/sudo mode.      
