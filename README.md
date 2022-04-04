# Build-Linux-Rt-Kernel
This tutorial is shows how to build a Preempt_RT Linux Kernel

<h2> 1. Get Dependencies! </h2>
sudo apt-get build-dep linux (you should enable dependency repositories) <br>
sudo apt-get install libncurses-dev flex bison openssl libssl-dev dkms libelf-dev libudev-dev libpci-dev libiberty-dev autoconf fakeroot
<h2> 2. Download Rt Patch and Kernel </h2>
<p>
  <font color="red"><b>IMPORTANT NOTE!</b></font><br>
<b>The Rt Patch and Kernel must be same version!<br>
Also (for this tutorial) you must download higher version kernel than yours. So check it by write on terminal : </b><br>
<code>$ uname -a</code></p><br>
For Rt Patch :<br>
http://cdn.kernel.org/pub/linux/kernel/projects/rt/<br>
For Kernel :<br>
http://cdn.kernel.org/pub/linux/kernel/<br>
For this tutorial version;<br>
File type must be "tar.xz" for both of them.<br>
##3. Preparing for build<br>
After download you have 2 tar.xz files like this:<br>
Uppercase X's are must be numbers.<br>
[1]) linux-X.X.X.tar.xz<br>
[2]) patch-X.X.X-rtX.patch.xz or patch-X.X.X-rtX-rcX.patch.xz.<br>
- Take this files into same folder.<br>
- You must be sure that you have enough space on disk(around 35-40gb but may change between versions).<br>
- Open terminal inside this folder.<br>
- Extract kernel : <br>
`$ tar -xf [kernel package filename]`<br>
- Go to extracted kernel folder : <br>
`$ cd [kernel package foldername]`<br>
- Extract RT patch and patch to kernel : <br>
`$ xzcat ../[rt patch filename] | patch -p1`<br>
- Copy your systems config to extracted kernel folder : <br>
`$ cp /boot/config[kernel name] .config` <br>
(<font color="red">Important note: You must copy config that lower version than downloaded new kernel!</font>)<br>
- Prepare config for new kernel :<br>
`make oldconfig`<br>
After writing this you should see question with choices and choose Fully Preemptible Kernel(Should be 4th option but not sure.)<br>
Then press enter for all or if you know anything about asking thing you can answer it but i'm not responsible for that.<br>
##4. Build<br>
- Disable old config keys for new build :<br>
`scripts/config --disable SYSTEM_REVOCATION_KEYS`<br>
`scripts/config --disable SYSTEM_TRUSTED_KEYS`<br>
`scripts/config --disable CONFIG_DEBUG_INFO_BTF`<br>
- Finally build it!<br>
`make -j[core count] deb-pkg` (You should write your cpu's core count after -j option ex;  make -j8 deb-pkg).<br>
<br>
<font color="red">Note:</font> Build process taking so much time. Please be patient. <br>
You should know that, if you do it on your first try you're so lucky person!<br>


