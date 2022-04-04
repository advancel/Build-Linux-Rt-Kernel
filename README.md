# Build-Linux-Rt-Kernel
This tutorial is shows how to build a Preempt_RT Linux Kernel

<h2> 1. Get Dependencies! </h2>
sudo apt-get build-dep linux (you should enable dependency repositories) <br>
sudo apt-get install libncurses-dev flex bison openssl libssl-dev dkms libelf-dev libudev-dev libpci-dev libiberty-dev autoconf fakeroot
<h2> 2. Download Rt Patch and Kernel </h2>
<p>
  <font color="red"><b>IMPORTANT NOTE!</b></font>
**The Rt Patch and Kernel must be same version!
Also (for this tutorial) you must download higher version kernel than yours. So check it by write on terminal : **
`$ uname -a`</p>
For Rt Patch :
http://cdn.kernel.org/pub/linux/kernel/projects/rt/
For Kernel :
http://cdn.kernel.org/pub/linux/kernel/
For this tutorial version;
File type must be "tar.xz" for both of them.
##3. Preparing for build
After download you have 2 tar.xz files like this:
Uppercase X's are must be numbers.
[1]) linux-X.X.X.tar.xz
[2]) patch-X.X.X-rtX.patch.xz or patch-X.X.X-rtX-rcX.patch.xz.
- Take this files into same folder.
- You must be sure that you have enough space on disk(around 35-40gb but may change between versions).
- Open terminal inside this folder.
- Extract kernel : 
`$ tar -xf [kernel package filename]`
- Go to extracted kernel folder : 
`$ cd [kernel package foldername]`
- Extract RT patch and patch to kernel : 
`$ xzcat ../[rt patch filename] | patch -p1`
- Copy your systems config to extracted kernel folder : 
`$ cp /boot/config[kernel name] .config` 
(<font color="red">Important note: You must copy config that lower version than downloaded new kernel!</font>)
- Prepare config for new kernel :
`make oldconfig`
After writing this you should see question with choices and choose Fully Preemptible Kernel(Should be 4th option but not sure.)
Then press enter for all or if you know anything about asking thing you can answer it but i'm not responsible for that.
##4. Build
- Disable old config keys for new build :
`scripts/config --disable SYSTEM_REVOCATION_KEYS`
`scripts/config --disable SYSTEM_TRUSTED_KEYS`
`scripts/config --disable CONFIG_DEBUG_INFO_BTF`
- Finally build it!
`make -j[core count] deb-pkg` (You should write your cpu's core count after -j option ex;  make -j8 deb-pkg).

<font color="red">Note:</font> Build process taking so much time. Please be patient. 
You should know that, if you do it on your first try you're so lucky person!


