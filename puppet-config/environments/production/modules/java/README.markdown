java
====


Overview
--------

The Java module installs the JDK and JRE. 

Module Description
-------------------

The Java module allows Puppet to install the JDK/JRE and update the bashrc file to include java in the path. 

Setup
-----

**What java affects:**

* installation directory for java
* bashrc file of the user or /etc/bashrc if parameter pathfile is not set 
	
### Beginning with Java

To deploy JDK-6u35-x64 to /home/example.com/apps/jdk-6u35 and append JAVA_HOME to $PATH

    java::setup { "example.com-jdk_6u35":
      ensure        => 'present',
      source        => 'jdk-6u35-linux-x64.tar.gz',
      deploymentdir => '/home/example.com/apps/jdk-6u35',
      user          => 'example.com',
      pathfile      => '/home/example.com/.bashrc'
    }

### Example usage on OpenSuSE

To install globally in /usr/lib64/jvm/oracle-jdk7 with environment configured via /etc/profile.local:

    java::setup {'jdk-7u21-linux-x64':
      source => 'jdk-7u21-linux-x64.tar.gz',
      deploymentdir => '/usr/lib64/jvm/oracle-jdk7',
      user => 'root',
      pathfile => '/etc/profile.local',
      cachedir => "/tmp/java-setup-${name}"
    }

Usage
------

The `java::setup` resource definition has several parameters to assist installation of java.

**Parameters within `java`**

####`ensure`

This parameter specifies whether java should be deployed to the deployment directory and bashrc file is updated or not.
Valid arguments are "present" or "absent". Default 


####`source`

This parameter specifies the source for the java archive. 
This file must be in the files directory in the caller module.
Value should be the exact name of the downloaded JDK or JRE archive file put in the files directory

**Only .tar.gz, .gz or .bin format as provided on Oracle's download website are supported.**

####`deploymentdir`

This parameter specifies the directory where java will be installed.

Note: If deploymentdir is set to /usr/local/, and you want to remove this installation in the future, setting ensure => 'absent' will cause the entire directory, i. e. /usr/local/ to be deleted permanently.

####`user`

This parameter is used to set the permissions for the installation directory of java.

####`pathfile`

This parameter is used to find and update the bashrc file to include java in the environment path.


Limitations
------------

This module has been built and tested using Puppet 2.6.x, 2.7, and 3.x.

The module has been tested on:

* CentOS 5.9
* CentOS 6.4
* Debian 6.0 
* Ubuntu 12.04
* OpenSuSE 12.1 (x64)

Testing on other platforms has been light and cannot be guaranteed. 

Development
------------

Bug Reports
-----------

Release Notes
--------------
**0.0.8**
\#10 - prepend JAVA_HOME to PATH instead of appending it
\#9 - improved module stability when default $cache_dir does not exist

**0.0.7**
\#7 - license added according to module specs

**0.0.6**
\#7 - added module license

**0.0.5**
\#6 - native support from .bin format of JDK / JRE as provided in Oracle's download section

**0.0.4**
\#5 - search term 'java' on forge.puppetlabs.com friendly

**0.0.3**
\#2 - added support for $::osfamily = Suse

**0.0.2**
\#1 - fixed validation error

**0.0.1**

First initial release.
