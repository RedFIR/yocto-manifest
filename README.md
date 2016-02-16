Repo Manifests for the Yocto Project Build System
=================================================

Getting Started
---------------
**1.  Install Repo.**

Download the Repo script:

    $ curl http://commondatastorage.googleapis.com/git-repo-downloads/repo > repo

Make it executable:

    $ chmod a+x repo

Move it on to your system path:

    $ sudo mv repo /usr/local/bin/

If it is correctly installed, you should see a Usage message when invoked
with the help flag.

    $ repo --help

**2.  Initialize a Repo client.**

Create an empty directory to hold your working files:

    $ mkdir yocto
    $ cd yocto

Tell Repo where to find the manifest:

    $ repo init -u git://github.com/RedFIR/yocto-zynq-manifest.git 

A successful initialization will end with a message stating that Repo is
initialized in your working directory. Your directory should now
contain a .repo directory where repo control files such as the manifest are
stored but you should not need to touch this directory.

***
**Note:**
You can use the **-b** switch to specify the branch of the repository
to use.  We develop on the guaranteed-to-break **dev** branch.  Most people should use
the **master** branch, which should at least compile.

The **-m** switch selects the manifest file (default is *default.xml*).
Our default.xml on **master** is designed to be stable as it *pins*
particular commits.

To test out the bleeding edge, type:

    $ repo init -u git://github.com/RedFIR/yocto-zynq-manifest.git -b dev
    $ repo sync

To get back to the known stable version, type:

    $ repo init -u git://github.com/RedFIR/yocto-zynq-manifest.git -b master
    $ repo sync

Also you can get a specific version of Yocto Project:

For example,

    $ repo init -u git://github.com/RedFIR/yocto-zynq-manifest.git -b refs/tags/dizzy
    
To learn more about repo, look at http://source.android.com/source/version-control.html 
***

**3.  Fetch all the repositories:**

    $ repo sync

Now go turn on the coffee machine as this may take 20 minutes depending on
your connection.

**4.  Initialize the Yocto Project Build Environment.**

    $ export TEMPLATECONF=$TBD/conf 
    $ source ./poky/oe-init-build-env

This copies default configuration information into the **poky/build/conf**
directory and sets up some environment variables for the build system.  This configuration
directory is not under revision control; you may wish to edit these configuration
files for your specific setup. 

**5.  Build an image:**

This process downloads several gigabytes of source code and then proceeds to
do an awful lot of compilation so make sure you have plenty of space (25GB
minimum), and expect a day or so of build time depending on your network
connection.  Don't worry---it is just the first build that takes a while.
