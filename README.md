# easy-docker-install / docker-ce傻瓜式安装


1. docker-ce傻瓜式安装
=====================


- 如果是国外的vps，用docker官方提供的安装脚本：
  ```
  # curl -sSL https://get.docker.com | sh
  ```

- 国内的主机：
  ```
   # curl -sSL https://get.daocloud.io/docker -o get-docker.sh
   # sh get-docker.sh --mirror Aliyun
  ```
  > 等脚本运行完成，docker就装好了

- 重启Docker
  ```
  # systemctl restart docker
  ```

- 设置Docker开机自启
  ```
  # systemctl enable docker
  ```
- 添加用
  ```
  #  sudo usermod -aG docker your-user
  ```

2. 用apt安装docker-ce
=================
- 为了确认所下载软件包的合法性，需要添加软件源的 GPG 密钥。
  ```
  curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
  ```
- 添加国内apt源
  ```
  add-apt-repository "deb [arch=amd64] https://mirrors.aliyun.com/docker-ce/linux/ubuntu $(lsb_release -cs) stable"
  add-apt-repository "deb [arch=amd64] https://mirrors.ustc.edu.cn/docker-ce/linux/ubuntu $(lsb_release -cs) stable"
  add-apt-repository "deb [arch=amd64] https://mirrors.tuna.tsinghua.edu.cn/docker-ce/linux/ubuntu $(lsb_release -cs) stable"
  ```
- 开始安装
  ```
  apt install docker-ce
  ```
