## Preamble

The following is a synopsis of Jeff Becker's video instuctions (30 Dec 2018) provided on how to clone, build and install Lokinet client. It follows up with installation of WeeChat and connecting to Lokinet chat room to test out the installation over the network.

Hope to see you there. :)

The example given here was tested on Ubuntu 18.10. 18.04 as used in the video should be the same.

These instruction anticipate that you have familiarity with Linux commands although most of the commands are a matter of copy/pasting into the cli or editing configuration files with nano (specific instructions provided).

Jeff's video is posted here https://youtu.be/pmssO185jKw and these steps follow the same sequence less verifying data in a couple instances using the "less" instruction which have been removed here for brevity.

## Build and Install:

From your users home directory extract and install the dependencies to compile loki-network with the command:

     sudo apt install build-essential cmake git libcap-dev wget rapidjson-dev

Clone the loki-network repository

    git clone https://github.com/loki-project/loki-network

Change to loki-network directory

    cd loki-network

Compile (example -j6 for core cpu used for this operation for 6 jobs, you are able to specify the number of jobs based on the cores you have for this task i.e. -j2 or -j4 etc.). Tests will execute at the end of compilation.

    make -j6
    
Install the binary:

    sudo make install

### Install resolvconf and modify the default resolvers on system

    sudo apt install resolvconf

Elevate user to root

    sudo -i

Edit the head file of resolvconf

    nano /etc/resolvconf/resolv.conf.d/head
    
Add the following below the existing text of the file

    nameserver 127.3.2.1
    
Overwrite the file and exit

    Ctrl O
    y
    Ctrl X
exit out of root console

    exit
    
Genrate config file

    lokinet -g
    
Grab the node info for bootstrap

    lokinet-bootstrap
    
Elevate to root

    sudo -i
    
Update resolvconf configuration

    resolvconf -u
    
Exit root user

    exit
    
### Run a client node.

    lokinet
    
## Connecting IRC client WeeChat via Lokinet
Log in to a new server screen.

### Install WeeChat (if not previously installed)

    sudo apt install weechat
    
execute WeeChat

     weechat
     
### Add Lokinet server in WeeChat and connect

    /server add lokinet 7okic5x5do3uh3usttnqz9ek3uuoemdrwzto1hciwim9f947or6y.loki/6667
    or
    /server add lokinet mguttytrxawnsby144oaabsc4h45e393ykiyttyxwu6u6p156tny.loki/6667
    
    /connect lokinet
    
### Join the channel

    /j #lokinet
    
Specify a nickname

    /nick [nickname]
    
### Say hello.












