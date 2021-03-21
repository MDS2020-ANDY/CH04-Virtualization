Docker安装  

#由于Mac M1系统仅支持Parallels Desktop  
#这里选择PD安装Ubuntu20.04.2.0 LTS  
1.安装Ubuntu20.04.2.0 LTS  
-下载Ubuntu Server for ARM  
地址：https://ubuntu.com/download/server/arm  
注意：此版本需要安装好Ubuntu后，再安装图像界面  
 <img width="370" alt="image" src="https://user-images.githubusercontent.com/56303015/111911700-92ab4e00-8aa1-11eb-9f33-6780552f017a.png">

-开始安装  
 ![image](https://user-images.githubusercontent.com/56303015/111911731-b078b300-8aa1-11eb-85b2-b9624cd9ad53.jpeg)

-设置Ubuntu账户及密码  
-继续安装，耗时稍长1个小时  
 ![image](https://user-images.githubusercontent.com/56303015/111911742-bec6cf00-8aa1-11eb-82df-0d5763233fe0.jpeg)
 
-开始安装图像界面  
【登陆页面】  
Ubuntu-server-stage login:  
Password:  
【更新：apt更新与sudo apt更新】  
$sudo apt update && sudo apt upgrade -y  
【安装xfce4】  
$sudo apt-get install xfce4  
 ![image](https://user-images.githubusercontent.com/56303015/111911762-cedeae80-8aa1-11eb-8af2-77c13a3d08a6.jpeg)

-图形界面安装完成  
 <img width="417" alt="image" src="https://user-images.githubusercontent.com/56303015/111911774-d605bc80-8aa1-11eb-96aa-e30a194b3b33.png">


2.安装Docker  
-启动Docker存储库  
$sudo apt update  
$sudo apt-get install apt-transport-https ca-certificates curl gnupg  
 
-添加Docker的官方GPG密钥  
$curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
 
-设置稳定的存储库  
$echo \
  "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null


- 安装 DOCKER ENGINE  
$sudo apt-get update    
$sudo apt-get install docker-ce docker-ce-cli containerd.io    
<img width="416" alt="image" src="https://user-images.githubusercontent.com/56303015/111912125-39dcb500-8aa3-11eb-89b4-94fb8aa5fb01.png">  
 报错：存储库中没有可用的Docker Engine  
--原因：可能是上一步设置稳定存储库出错   
尝试安装其他依赖项和添加存储库   
$ sudo apt-get install gnupg-agent software-properties-common  
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add –  
$sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
$sudo apt update  
$sudo apt install docker-ce  
<img width="373" alt="image" src="https://user-images.githubusercontent.com/56303015/111912163-6264af00-8aa3-11eb-9747-5a70164dc757.png">
又报错了！！！！！但$apt list -a docker-ce有反应了！  
尝试直接通过选择版本安装docker-ce  
报错！！list有的版本，安装报错说was not found  

解决：全部重装！ 
$sudo rm -rf /var/lib/docker  
$ sudo rm -rf /var/lib/containerd  
更改阿里云镜像安装，依旧报错且$apt-cache madison docker-ce下无可用docker-ce版本，$apt list -a docker-ce有列出版本  
 <img width="387" alt="image" src="https://user-images.githubusercontent.com/56303015/111912239-bff8fb80-8aa3-11eb-8e63-48ca50bea788.png">

成功解决的办法！！！！：https://segmentfault.com/a/1190000015127278  
手动加入源：  
$ cd /etc/apt/sources.list.d  
$ sudo vi docker.list  
加上下面这一行  
<img width="416" alt="image" src="https://user-images.githubusercontent.com/56303015/111912268-d1420800-8aa3-11eb-9719-b82221eccb0f.png">

更新：  
$sudo apt update   
$sudo apt install docker-ce
<img width="416" alt="image" src="https://user-images.githubusercontent.com/56303015/111912280-db640680-8aa3-11eb-88bc-c973545f16e6.png">  

启动Docker：成功！！！！！   
$sudo systemctl status docker  
 <img width="416" alt="image" src="https://user-images.githubusercontent.com/56303015/111912297-ecad1300-8aa3-11eb-8e94-a163f1301d27.png">
  
-阻止 Docker 自动更新  
$sudo apt-mark hold docker-ce  
2-1以非 Root 用户身份执行 Docker  
$sudo usermod -aG docker hello  
<img width="416" alt="image" src="https://user-images.githubusercontent.com/56303015/111912314-00f11000-8aa4-11eb-8293-7e54dcb0b62e.png">  

解决办法：  
https://my.oschina.net/u/3585265/blog/4306023  
$ newgrp docker  
$ docker version   
$ docker run hello-world  
成功！！  
<img width="416" alt="image" src="https://user-images.githubusercontent.com/56303015/111912324-077f8780-8aa4-11eb-9acb-4d8e0d0900ea.png">


·
