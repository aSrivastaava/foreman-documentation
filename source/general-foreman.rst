General Foreman
================

Provisioning
------------

This chapter details the configuration of the required UI components necessary to provision an OS onto a host.

Operating Systems
^^^^^^^^^^^^^^^^^

The Operating Systems page (Hosts -> Operating Systems) details the OSs known to Foreman, and is the central point that the other required components tie into.


**Creating an Operating System**

Simply click New Operating system on the main page. You will be taken to a screen where you can create the bare essentials of a new OS. Not everything required for a successful provision is on this page (yet) - the remaining components will appear for selection as we create them.

You will need to fill in the first few parts of the form (Name, Major, Minor, Family, and possibly some family-dependant information). In the case of OSs like Fedora, it is fine to leave Minor blank.

If the default Partition Tables & Installation media are suitable, then you can assign them now. If not, return here after each step in this chapter to assign the newly created objects to your Operating System

**Auto-created Operating Systems**

Foreman does not come with any Operating Systems by default. However, Foreman will detect the Operating System of any host which reports in via Puppet - if the OS of that Host is supported, it will be created (with very basic settings) and assigned to the Host. Thus you may find some OSs already created for you.

Installation Media
^^^^^^^^^^^^^^^^^^
The Installation Media represents the web URL from where the installation packages can be retrieved (i.e the OS mirror). Some OS Media is pre-created for you when Foreman is first installed. However, it is best to edit the media you are going to use and ensure the Family is set.

**New Installation Media**

If your OS of choice does not have a mirror pre-created for you, click the New Medium button to create one. There are a few variables which can be used to pad out the URL. For example:

*http://mirror.averse.net/centos/$major.$minor/os/$arch*

Be sure to set the Family for the Media

**Assign to Operating System**

If you have not already done so, return to the Operating System page for your OS and assign the Media to it now.

Provisioning Templates
^^^^^^^^^^^^^^^^^^^^^^
The Provision Templates is the core of Foreman’s flexibility to deploy the right OS with the right options. There are several types of template, along with a flexible matching system to deliver different templates to different Hosts.

Foreman comes with pre-created templates for the more common OSs, but you will need to review these. All these templates are locked by default, hence they can not be modified. Most of them are customizable through parameters, but if you need some custom functionality, the recommended workflow is to clone the template and edit the clone. You can unlock the pre-created template and edit it directly, but note that any custom change will be overridden on any Foreman update. If you believe your change is worth of including in next Foreman release, please consider sending a patch to community-templates repository which we regularly synchronize with our codebase.

**Template kind**

There are several template kinds:
 * PXELinux, PXEGrub, PXEGrub2 - Deployed to the TFTP server to ensure the Host boots the correct installer with the correct kernel options (also referred to as PXE templates)
 * Provision - The main unattended installation file; e.g. Kickstart or Preseed
 * Finish - A post-install script used to take custom actions after the main provisioning is complete
 * User_data - Similar to a Finish script, this can be assigned to hosts built on user_data-capable images (e.g. Openstack, EC2, etc)
 * Script - An arbitrary script, not used by default, useful for certain custom tasks
 * iPXE - Used in {g,i}PXE environments in place of PXELinux (do not confuse with PXE templates above)

