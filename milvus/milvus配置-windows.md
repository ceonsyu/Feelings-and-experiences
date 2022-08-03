最后修改2022.7.14
## 准备工作
- linux虚拟机
  - 虚拟机工具采用virtualBox，系统采用Ubuntu，虚拟硬盘空间预留至少15G，以免后续空间不足。
- shell工具
  - 因为虚拟机运行ubuntu系统太过卡顿，采用shell工具mobaxterm来控制虚拟机
## 配置
- 虚拟机工具配置
  - 将虚拟机网络设置为NAT模式，**并添加端口转发规则**，将虚拟机端口映射到主机上
- 虚拟机配置
  - 安装ssh,为shell工具连接虚拟机做准备
  - 启动ssh
```
#安装ssh
sudo apt-get install openssh-server
#启动ssh
sudo service sshd start
```
## 连接虚拟机
使用shell工具建立连接，远端host使用localhost即可
## 安装docker
根据docker官网的[文档](https://docs.docker.com/engine/install/ubuntu/#set-up-the-repository)，ubuntu系统安装docker的步骤如下：
1. 设置docker仓库
   - 更新软件包索引并安装软件包 
   ```
    sudo apt-get update
    sudo apt-get install \
        ca-certificates \
        curl \
        gnupg \
        lsb-release
    ```
    - 添加docker官方GPGkey
    ```
    sudo mkdir -p /etc/apt/keyrings
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
    ```
    - 设置仓库
    ```
     echo \
    "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
    $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    ```
2. 安装docker引擎
    - 更新软件包索引，并安装最新版本的 Docker 引擎、容器和 Docker Compose
    ```
    sudo apt-get update
    sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
    ```
    - 验证是否安装成功
    ```
    sudo docker run hello-world
    ```
## 安装milvus(来自milvus[官方文档](https://milvus.io/docs/v2.0.x/install_standalone-docker.md))
1. 安装docker-compose  
这是docker的多服务管理工具，通过Compose，可以使用YML文件来配置应用程序需要的所有服务。
```
sudo apt  install docker-compose
```

2. 下载安装milvus的yml文件
```
wget https://github.com/milvus-io/milvus/releases/download/v2.0.2/milvus-standalone-docker-compose.yml -O docker-compose.yml
```
3. 安装milvus  
此过程可能较慢或卡死不动，可以ctrl+c中止后重来。
```
sudo docker-compose up -d
```
4. 检查容器状态
```
sudo docker-compose ps
```
## 安装pythonSDK
- python版本要在3.8以上（适配milvus2.0.2）。如果没有pip，要先安装pip。
- SDK安装语句如下
```
python3 -m pip install pymilvus==2.0.2
```
安装完毕后执行下面的语句，如果安装成功，则没有任何报错。
```
python3 -c "from pymilvus import Collection"
```
## [测试milvus](https://milvus.io/docs/v2.0.x/example_code.md)
- 下载测试代码

```
wget https://raw.githubusercontent.com/milvus-io/pymilvus/v2.0.2/examples/hello_milvus.py
```
- 运行测试代码
```
python3 hello_milvus.py
```
## 注意
每次重启虚拟机后需要重新执行以下语句，否则milvus无法连接服务器
```
sudo docker-compose up -d
```

