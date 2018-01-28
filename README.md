# ohsu-cm
OHSU configuration management

=====================================================
### About ###
This is an ansible build script optimized for Ubuntu Linux 16.04 LTS (long term support). It will install:
* Hyrax pre-requisites
* solr on port 8983
* fedora on port 8080
* ffmpeg for video transcoding of video derivatives
* imagemagick, ghostscript, and other image libraries for creating image derivatives
* the `mahonia` software, a version of Hyrax customized for OHSU, from http://github.com/curationexperts/mahonia


### How to Build a Single Box Server ###
Clone this repo to your local system to build OHSU servers on AWS.  

1. Ensure you have ansible >= 2.3 installed
1. Ensure you have [boto](https://boto3.readthedocs.io/en/latest/) >= 3 installed
1. Use the AWS web client to create an Ubuntu 16.04 server. Record the IP it was assigned. Ensure you have the ssh key required to access it.
1.  `git clone --recurse https://github.com/curationexperts/ohsu-cm.git`
1.  `cd ohsu-cm`
1. Put your new server's IP in the ansible `hosts` file in this repo. Create a new section for it, if appropriate. E.g., you might want to record separately which are your production servers vs your QA or staging servers. Each system will need a `hostname` and `domain` variable. 
1. Run the build: `ansible-playbook mahonia.yml`

**Things have run successfully if:**
1. Mahonia is deployed at https://{{ hostname }}.{{ domain }}
1. http should redirect to https
1. Visiting https://{{ hostname }}.{{ domain }}/Shibboleth.sso/Login takes you to a Shibboleth login screen

### To change the shibboleth server
To change the shibboleth server that the `shibboleth-sp` task is configured against, update
the `{{ shibboleth_host }}` variable in the `hosts` file of this repository and re-run 
the `shibboleth-sp` task. Note that the hostname variable should only be the 
hostname + domain name, not including any `https://` prefix, e.g., "bet.curationexperts.com".

You might also need to update the configuration files in this task, according to how your
local shibboleth-idp system is configured. The current task assumes that the idp metadata
is available from `https://{{ shibboleth_host }}/shibboleth`, which you might need to customize.

If you need to provide your shibboleth-sp metadata to the OHSU shibboleth-idp server, you can 
get it from `https://{{ hostname }}.{{ domain }}/Shibboleth.sso/Metadata`
