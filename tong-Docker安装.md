基于Ubuntu的Docker安装指南

1	安装环境  

Vmware12.1  
Ubuntu20.04

2	安装步骤
$sudo apt update (并输入密码)

  ![image](https://user-images.githubusercontent.com/79824627/112018445-84286980-8b69-11eb-96e1-edb83ba58c66.png)  

$sudo apt install apt-transport-https ca-certificates curl punpg-agent software-properties-common  

![image](https://user-images.githubusercontent.com/79824627/112018582-a8844600-8b69-11eb-9fc3-e964faae657c.png)  

 
$curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

![image](https://user-images.githubusercontent.com/79824627/112018610-b0dc8100-8b69-11eb-8a1f-5db607a99d16.png)  

 
$sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs)
stable"

![image](https://user-images.githubusercontent.com/79824627/112018730-cd78b900-8b69-11eb-91ad-ba41a799ce1b.png)  

 
下面开始安装Docker的最新版本：

$sudo apt update

![image](https://user-images.githubusercontent.com/79824627/112018767-d4073080-8b69-11eb-9e3e-7c5561142e07.png)  

 
$sudo apt install docker-ce docker-ce-cli containerd.io  

![image](https://user-images.githubusercontent.com/79824627/112018805-dcf80200-8b69-11eb-802b-da7a70ffc25f.png)  

 
错误解决方法：  
若出现“无法获得锁、无法获得管理目录，是否有其它进程在占用它”  
解决方案：  
sudo rm /var/cache/apt/archives/lock   
sudo rm /var/lib/dpkg/lock  
强行释放锁，然后重启终端，再继续操作就可以了。  

安装完成，Docker启动，并验证

![image](https://user-images.githubusercontent.com/79824627/112018892-eb461e00-8b69-11eb-839c-c802a249379f.png)  

 
$sudo apt-mark hold docker-ce （阻止Docker自动更新）

![image](https://user-images.githubusercontent.com/79824627/112018936-f305c280-8b69-11eb-870d-5642d3bae535.png)  

 
设置以非ROOT用户登录Docker  
$sudo usermod -aG docker ubuntu  
![image](https://user-images.githubusercontent.com/79824627/112018978-fb5dfd80-8b69-11eb-96cb-f754eb6dc73b.png)  

 
注销本机 并重新登录  
$newgrp docker  
$docker version  

![image](https://user-images.githubusercontent.com/79824627/112019011-03b63880-8b6a-11eb-9439-5d6f622443e2.png)  

 
验证安装  
$docker container run hello-world  

![image](https://user-images.githubusercontent.com/79824627/112019061-0ca70a00-8b6a-11eb-82e9-f34b416b320d.png)  

 
自此安装完成！
