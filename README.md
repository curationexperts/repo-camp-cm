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
1.  `git clone --recurse https://github.com/bess/ohsu-cm.git`
1.  `cd ohsu-cm`
1. Put your new server's IP in the ansible `hosts` file in this repo. Create a new section for it, if appropriate. E.g., you might want to record separately which are your production servers vs your QA or staging servers. Each system will need a `hostname` and `domain` variable. 
1. Run the build: `ansible-playbook build_ohsu_demo_server.yml`
