# V2Ray云彩姬

**科学上网 从娃娃抓起** **||** **运行脚本 开箱即用**

## :carousel_horse: 项目简介

> 1. 本项目架构去层级，用户可直接通过视图交互访问数据库；
> 2. 本项目通用版本使用集群定时采集方案；
> 3. 本项目软件及源码禁止在国内大陆网络环境大范围传播，项目转载请注明出处；
> 4. 本项目开源免费，请不要滥用接口；
> 5. 禁止任何人使用本项目及其分支提供任何形式的收费服务；

针对全球范围内基于`STAFF原生架构`产出的机场进行垂直挖掘；从youtube油管等平台获取机场链接及打击目标；采集免费优质的订阅链接，综合会员时长、可用流量、节点质量等管理条件进行优先排序；

## :loudspeaker: 更新日志

- **2020.10.20**

  > > 重要更新！

  1. 支持Troajn、V2ray、SSR订阅链接多线程联合采集；
  2. 文档树调整，旧版本软件无法正常运行，请将客户端更新至最新版本;
  3. 支持软件自动更新。

  > > 功能迭代！

  1. 使用Redis接管存取业务，提高分发效率；
  2. 开放get接口，快速获取订阅链接；
  3. 自闭时间提升至30s/次；
  4. 添加一键部署脚本，用户可在CentOS7环境下快速建立采集环境（可改动源码以适配不同环境的需求）；

## :eagle: 快速上手

- **软件获取**

  - 【方案一】：[下载安装向导 (约17MB)](https://t.qinse.top/subscribe/installer.exe)；

  - 【方案二】：Clone项目；

  ![Snipaste_2020-10-22_13-53-00](https://i.loli.net/2020/10/22/s9vC6RI7FtVJahe.png)

- **软件使用**

  - 运行`V2Ray云彩姬.exe` 即可启动**v2ray云彩姬**获取订阅连接。
  - [云彩姬使用说明](https://github.com/QIN2DIM/V2RayCloudSpider/blob/master/V2Ray云彩姬使用说明.md)


## :video_game: 进阶玩法

> 该脚本未在macOS测试运行，可能存在非常多的bug，欢迎感兴趣的小伙伴来跑一下程序- -

- `/V2RaySpider0925`中存放该项目通用版本的源代码

- 运行`main.py`启动程序

- 安装依赖`当前目录：/V2RaycSpider0925`

  ```
  pip install -r requirements.txt -i https://pypi.tuna.tsinghua.edu.cn/simple/
  ```

- 修改配置` config.py`

### :balance_scale: 参数设置

- 请在此正确填写你的服务器信息，并将整个项目文件`V2RaycSpider0925`上传至linux服务器的`/qinse`文件夹

- 服务器首次运行请确保已安装`redis`并正确配置（开放）访问权限，且安装项目Python第三方库

- 运行`./funcBase/deploy_engine.py`则可部署脚本。

- **一定确保宁的环境部署在非大陆VPS上否则大概率翻车**

  ```powershell
  # 预览运行效果;如下为默认路径
  python3 /qinse/V2RaycSpider0925/funcBase/deploy_engine.py
  ```
  
  ```python
  # 部署
  nohup python3 /qinse/V2RaycSpider0925/funcBase/deploy_engine.py &
  ```
  
  ```python
  # /V2RaycSpider0925/config.py
  # SYS_PATH = f'/qinse/V2RaycSpider{verNum}'
  
  # ---------------------------------------
  # Cloud server configuration(SSH)
  # ---------------------------------------
  ECS_HOSTNAME: str = 'your ip'
  ECS_PORT: int = 29710
  ECS_USERNAME: str = ''
  ECS_PASSWORD: str = ''
      
  # ---------------------------------------
  # Redis server configuration(SSH)
  # ---------------------------------------
  
  REDIS_HOST: str = 'your ip'
  REDIS_PORT: int = 6379
  REDIS_PASSWORD: str = ''
  ```

- **设置驱动执行权限**

  给`chromedriver`设置可执行权限，如果用`Finalshell`l或`Xshell`的同学，直接右键目标文件即可设置文件权限；项目预装的驱动是最新版本的[2020.10]所以`Linux`中要下载`v85.0.4183.102`或更新版本的Chrome

  ```python
  CHROMEDRIVER_PATH = os.path.dirname(__file__) + '/MiddleKey/chromedriver'
  ```

- 安装`gcc`

  ```
  yum install gcc-c++
  ```

- `Linux`**安装Chrome**

  - 指定yum源

  ```powershell
  wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
  ```

  - 安装

  ```powershell
  curl https://intoli.com/install-google-chrome.sh | bash
  ```

  - 安装后执行

  ```powershell
  google-chrome-stable --no-sandbox --headless --disable-gpu --screenshot https://www.baidu.com/
  ```

- [安装](https://shimo.im/docs/5bqnroJYDbU4rGqy/)`redis`

### :zap: 其他设置

- 快速获取

  - 使用requests的get请求，分别访问以下链接，使用text抽取订阅链接

    ```python
    # Python3.8
    # quick——get Subscribe API
    import requests
    
    subs_target = 'https://t.qinse.top/subscribe/{}.txt'
    
    subs_ssr = requests.get(subs_target.format('ssr')).text
    subs_trojan = requests.get(subs_target.format('trojan')).text
    subs_v2ray = requests.get(subs_target.format('v2ray')).text
    
    print("subs_ssr: {}\nsubs_: {}\nsubs_v2ray: {}\n".format(subs_ssr,subs_trojan,subs_v2ray))
    
    ```

    ![image-20201020112752998](https://i.loli.net/2020/10/20/XaJc4qA1ehPUM5V.png)

##  :small_red_triangle: 注意事项

- **防火墙警告**

  - 首次运行可能会弹出提示

    ![3](https://i.loli.net/2020/10/06/MhwiZfOz3VdDPU5.png)

    ![3](https://i.loli.net/2020/10/06/gmLksO3HCtyWu9r.png)

## :world_map: 开源计划

- [x] 支持Trojan-go、Trojan-gfw机场的采集
- [ ] 融合网络代理核心，形成自洽的科学上网模块
- [x] 合并订阅链接消息队列，PC端可查看目前在库最多25条Subscribe订阅链接，并择一获取
  - [x] 合并队列
  - [x] 查看链接
  - [x] 择一获取
- [ ] 逐渐停用easyGUI前端模块，兼容跨平台访问(手机，电脑，嵌入式系统)



## :email: 联系我们

> 本项目由海南大学机器人与人工智能协会提供维护

- [**Email**](mailto:RmAlkaid@outlook.com?subject=CampusDailyAutoSign-ISSUE) **||** [**Home**](https://a-rai.github.io/)

###  