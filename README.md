## 实验目的
1. 初步了解虚拟化技术，理解云计算的相关概念
2. 理解系统工程师面临的困境
3. 理解自动化安装、管理（DevOps）在云应用中的重要性

## 实验环境与要求
1. **实验需要硬件虚拟化（AMD-V 或 Intel-VT）支持，部分旧笔记本不支持。**
2.  用户通过互联网，使用微软远程桌面，远程访问你在PC机上创建的虚拟机
3. 虚拟机操作系统 Centos，Ubuntu，或 你喜欢的 Linux 发行版，能使用 NAT 访问外网。

## 实验内容
### 1.安装VirtualBox
* **安装 Git 客户端（git bash）**
  由于我的电脑之前已经安装了Git客户端，所以这里不做过程的说明。
* **安装 Oracle VirtualBox 5.X**
  由于我的电脑之前已经安装了VirtualBox，所以这里不做过程的说明。
* **配置 VirtualBox 虚拟机存储位置**
   为了避免找不到虚拟机存储位置，特别是消耗启动盘的宝贵空间，所以我们要找一个剩余空间多的磁盘建立一个文件夹，作为虚拟机存储位置。
   
   **①** 在VirtualBox菜单中找到“**管理**”这个选项，然后选择“**全局设定**”选项；
   
   **②** 在全局设定页面中点击“**常规**”选项，选择自己建立的文件夹作为默认虚拟电脑位置。
   
    ![](https://img-blog.csdnimg.cn/20190828164009769.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1YW5fdGluZw==,size_16,color_FFFFFF,t_70)

* **创建虚拟机内部虚拟网络**
    我们要使 VirtualBox 内部虚拟机可以通过内部虚拟网络，实现虚拟机之间、虚拟机与主机的通讯。
    
    **配置过程：**
     
     （1） 在VirtualBox菜单中点击“**管理** ”，选择“**主机网络管理器**“”，点击左上角的“**创建**”选项；
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190828165152172.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1YW5fdGluZw==,size_16,color_FFFFFF,t_70)
 
    （2）在新建的虚拟网卡中填写好IPv4地址和网络掩码，勾选“**启用**”，并点击“**应用**”选项。
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190828165947648.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1YW5fdGluZw==,size_16,color_FFFFFF,t_70)
    **验证**：在主机 windows 命令行窗口输入 ipconfig 就可以看到刚刚创建的虚拟网卡VirtualBox Host-Only Network #3的信息，和设置的一样。
    
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190828170424461.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1YW5fdGluZw==,size_16,color_FFFFFF,t_70)

### 2.创建Linux虚拟机（选择了CentOS ）
* **下载 Linux 发行版镜像**
  选择了CentoOS，所以在官网下载了Minimal ISO镜像文件。
* **用VBox创建虚拟机**

   (1)新建一个虚拟机，以“centos”开头命名，选择好储存位置，要注意是64bit；
   ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190828171452582.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1YW5fdGluZw==,size_16,color_FFFFFF,t_70)
  
  (2)设置内存大小；
   ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190828172004958.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1YW5fdGluZw==,size_16,color_FFFFFF,t_70)
   
   (3)选择“创建虚拟硬盘”，并选择类型为VDI文件；
   ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190828172405980.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1YW5fdGluZw==,size_16,color_FFFFFF,t_70)
   
   (4)选择动态分配存储空间；
   ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190828172521444.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1YW5fdGluZw==,size_16,color_FFFFFF,t_70)
  
  (5)设置存储空间大小不低于30G。避免以后扩展难。
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190828172636834.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1YW5fdGluZw==,size_16,color_FFFFFF,t_70)
   
   (6)配置虚拟机网卡
   第一块网卡必须是 NAT；第二块网卡连接方式： Host-Only，接口就是前面创建的虚拟网卡。右键点击centos-hby虚拟机，然后选择“设置”选项，查看“网络”界面。
   **①**网卡1的连接方式为NAT；
   ![在这里插入图片描述](https://img-blog.csdnimg.cn/2019082819150894.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1YW5fdGluZw==,size_16,color_FFFFFF,t_70)
   
   **②**网卡2的连接方式为Host-only，而且选择界面为之前新建的网卡VirtualBox Host-Only Ethernet Adapter #3。
   ![](https://img-blog.csdnimg.cn/20190828191606374.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1YW5fdGluZw==,size_16,color_FFFFFF,t_70)
* **安装Base虚拟机**
此处若有鼠标不显现的情况，解决方法见此[链接](https://www.jianshu.com/p/f9ffa8369673)。
   (1)右键点击centos-hby虚拟机，然后选择“启动”选项，选择下载好的CentOS镜像文件作为启动盘；
   ![在这里插入图片描述](https://img-blog.csdnimg.cn/2019082819194215.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1YW5fdGluZw==,size_16,color_FFFFFF,t_70)
   
   (2)按照提示选择语言，并且点击“安装位置”选项，选择“完成”；
   ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190828193731185.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1YW5fdGluZw==,size_16,color_FFFFFF,t_70)
  
   (3)点击“网络和主机名”，分别打开enp0s3和enp0s8,并修改左下角主机名为hby；
   ![](https://img-blog.csdnimg.cn/20190828193901312.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1YW5fdGluZw==,size_16,color_FFFFFF,t_70)
   ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190828194204612.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1YW5fdGluZw==,size_16,color_FFFFFF,t_70)
  
   (4)点击“开始安装”，设置好ROOT密码，并填写用户名且设置为管理员；
   ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190828194653649.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1YW5fdGluZw==,size_16,color_FFFFFF,t_70)
   (5)升级OS内核
   重启安装成功后，输入用户名和密码进入系统，然后输入```yum update```命令升级OS内核。
   ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190828202711469.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1YW5fdGluZw==,size_16,color_FFFFFF,t_70)
   (6)检查网卡设置
    **①**输入命令```nmtui```，选择“Edit a connection”，配置好第二块网卡enp0s8的IP和DNS等，然后选择保存并返回；
       ![在这里插入图片描述](https://img-blog.csdnimg.cn/2019082819560272.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1YW5fdGluZw==,size_16,color_FFFFFF,t_70)
       ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190829154908168.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1YW5fdGluZw==,size_16,color_FFFFFF,t_70)
    选择“Activate a connection”，把enp0s8的状态点击“Activate“”;![在这里插入图片描述](https://img-blog.csdnimg.cn/2019082819572276.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1YW5fdGluZw==,size_16,color_FFFFFF,t_70)
       **②**ping主机的IP，可以发现能ping通。
       ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190828200845706.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1YW5fdGluZw==,size_16,color_FFFFFF,t_70)
       
* **安装虚拟机**
    (1)点击 centos-hby选择复制，输入新虚拟机的名，必须选择重新初始化所有网卡的 MAC 地址，然后选择“**链接复制**”；
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190828210349817.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1YW5fdGluZw==,size_16,color_FFFFFF,t_70)
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190828210451629.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1YW5fdGluZw==,size_16,color_FFFFFF,t_70)
    (2)使用```nmtui```命令第二块网卡地址为192.168.99.101；
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190828211015272.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1YW5fdGluZw==,size_16,color_FFFFFF,t_70)
    (3)主虚拟机hby去ping第二个虚拟机hbyA，就是ping 192.168.99.101，成功ping通；通过ssh也能访问到该虚拟机，输入```logout```则可以断开连接。**注意要在两台虚拟机的第二块网卡都是Active的状态下，并且windows要开启git bash。**
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190828213310447.png)
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190828213336450.png)
 * **安装CentOS桌面(以虚拟机hbyA为例)**
    (1)使用命令```yum groupinstall "GNOME Desktop"```安装桌面，注意要在特权模式下，即先输入sudo，输入管理员命令；
    (2)使用命令```ln -sf /lib/systemd/system/runlevel5.target  /etc/systemd/system/default.target```，设置启动目标为桌面；
    (3)使用命令```reboot```重启；
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190828230316452.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1YW5fdGluZw==,size_16,color_FFFFFF,t_70)
    (4)安装VirtualBox增强功能；
    ①首先使用命令```sudo yum install -y kernel devel gcc```安装kernel和gcc；
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190829090356583.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1YW5fdGluZw==,size_16,color_FFFFFF,t_70)
    ②然后点击窗口工具栏中的“**设备**”，选择“**安装增强功能**”，最后运行。右键查看桌面VBOXADDITIONS 的属性，看其存放路径,然后进入该存放路径进行安装，例如：
cd /run/media/rootname/VBOXADDITIONS_4.xxx_59338 
sh ./VBoxLinuxAdditions.run 
    成功后可以看到鼠标不再受Right Ctrl的控制，屏幕也可以扩大了。![在这里插入图片描述](https://img-blog.csdnimg.cn/20190829090646165.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1YW5fdGluZw==,size_16,color_FFFFFF,t_70)
    (5)安装Chrome浏览器。
    ①下载rpm包，搜索 “Google Chrome for Linux 下载” 得到；
    ②使用命令```yum localinstall google-chrome-stable_current_x86_64.rpm```，yum会自动分析依赖，完成安装。
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190829152102938.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1YW5fdGluZw==,size_16,color_FFFFFF,t_70)
### **3.配置用远程桌面访问虚拟机**
   (1)从VirtualBox官网上下载与VirtualBox对应版本的Oracle VM VirtualBox Extension Pack。我的VirtualBox是6.0.4。
   ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190829210434536.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1YW5fdGluZw==,size_16,color_FFFFFF,t_70)
   (2)关闭所有虚拟机，点击工具栏中的“管理”，选择“全局设定”，点击“扩展”，添加刚刚下载的扩展包。
   ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190829210851444.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1YW5fdGluZw==,size_16,color_FFFFFF,t_70)
   (3)为每台虚拟机配置不同的端口，以centos-hbyA为例，右击虚拟机，选择**“设置**”，点击“**显示**”，选择“**远程桌面**”，勾选“**启用服务器**”，填写端口号。
   ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190829211639808.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1YW5fdGluZw==,size_16,color_FFFFFF,t_70)
   (4)打开windows远程桌面连接，填写IP和端口号，点击连接，可以登录虚拟机。
   ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190829212258310.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1YW5fdGluZw==,size_16,color_FFFFFF,t_70)
   ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190829212908658.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1YW5fdGluZw==,size_16,color_FFFFFF,t_70)
## 实验心得
总算是配置好这个私有云了！经过两天晚上的努力，加上查询各种网上资料，踏踏实实地做好每一步，把配置的过程详细地写了出来，我的内心充满了成就感。曾经觉得配置环境是一件令人头疼的事，因为所遇到的困难都是未知的，但是经过这次实验，我对自己多了一点信心，也明白耐心是十分重要的！
   
   
