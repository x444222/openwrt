# openwrt

本教程基于lean源码  https://github.com/coolsnowwolf/lede
P3TERX云编译模板   https://github.com/P3TERX/Actions-OpenWrt



教程开始  请全局科学上网


第一步：无脑虚拟机安装Ubuntu，自行百度教程

第二步：ubuntu配置源码

参考教程https://github.com/coolsnowwolf/lede    


ctrl+alt+t打开命令行


命令行输入
sudo apt-get update 
输入密码

然后输入
sudo apt-get -y install build-essential asciidoc binutils bzip2 gawk gettext git libncurses5-dev libz-dev patch python3 python2.7 unzip zlib1g-dev lib32gcc1 libc6-dev-i386 subversion flex uglifyjs git-core gcc-multilib p7zip p7zip-full msmtp libssl-dev texinfo libglib2.0-dev xmlto qemu-utils upx libelf-dev autoconf automake libtool autopoint device-tree-compiler g++-multilib antlr3 gperf wget curl swig rsync

因为我安装过了，所以很快

使用 git clone https://github.com/coolsnowwolf/lede 命令下载好源代码

下载源码，请科学上网，不然很慢



然后 cd lede 进入目录

./scripts/feeds update -a
在这一步之前需要酸酸乳等插件需要修改lede 目录下的feeds.conf.default


./scripts/feeds install -a


make menuconfig     过程参考如下教程https://www.right.com.cn/forum/thread-1237348-1-1.html

target images 教程中此步骤为修改固件大小 一般不要修改

luci >applications  此步骤为选择app插件
  
luci >themes  此步骤选主题

kwrnel modules > network devices  此步骤为选择有线网卡，我的只需要8168网卡驱动，所以取消了其他,强迫症，不要的都取消了

kwrnel modules > wirelcss drivers  此步骤为选无线网卡，一般不选，如果需要无线功能要选很多插件，小白先略过此步


一般选择
kwrnel modules > network devices  选择有线网卡驱动

luci >applications 选择插件

既然咱们是小白，其他就不用管他，默认即可

lean的源码默认选好了完整固件需要的组件
所以我们只需要修改网卡驱动和luci插件

记得最后save保存配置

以上步骤参考教程https://www.right.com.cn/forum/thread-1237348-1-1.html



第三步：配置好make menuconfig 导出lede目录下的 .config 和feeds.conf.default 文件备用  看不到文件按ctrl+h  还看不到就是你没有save保存配置

接着打开 https://github.com/P3TERX/Actions-OpenWrt 项目

此步参考教程 https://p3terx.com/archives/build-openwrt-with-github-actions.html

Fork项目到自己的仓库或 use this template 复制模板到自己仓库

在复制过来的模板上传feeds.conf.default文件  新建一个 .config《无法直接上传我们备份出来的》把备份出来的 .config内容复制进去保存

点击项目页actions  点击 Build OpenWrt 点击run workflow 即可开始编译

已经开始编译，等待2-4个小时即可，在等待时间了可以来十几盘鸡

这是我编译好的
