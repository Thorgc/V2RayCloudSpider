# V2Ray云彩姬

**科学上网 从娃娃抓起** **||** **运行脚本 开箱即用**

## :carousel_horse: 项目简介

> 1. 本项目软件及源码禁止在国内网络环境大范围传播；
>
> 2. 本项目开源免费，请不要滥用接口；
>
> 3. 禁止任何人使用本项目及其分支提供任何形式的收费服务。

- 针对全球范围内基于[STAFF原生架构](https://github.com/Anankke/SSPanel-Uim)产出的机场进行垂直挖掘；
- 从`Youtube`、`SONA-TechnologyForum` 等平台获取`RegisteUrl & HitTarget`；
- 综合`LifeCycle`、`RemainingFlow `、`NodeQuality`等参数进行联合采集；
- 虽然软件名叫`V2Ray云彩姬`但理论上支持所有形式订阅链接的采集；
- 更多项目细节请访问[李芬特小窝Blog](https://www.qinse.top/v2raycs/) :smirk:

## :loudspeaker: 更新日志

- #### 2020.11.24 v_1.0.2.11162350.11.beta

  > **Major Update**

  1. Further optimize the project engineering structure.
  2. Further optimize the program logic to reduce the difficulty of project deployment.
  3. Modify user permissions.

  > **Function Iteration**

  1. Overload the `TrojanCollectionModule(TCM)`.
  2. Expand the work queue to `150pieces/day`.
  3. Program the `ACM-CentralEngine` to counter the anti-crawler mechanism.

  > **Performance Tuning**

  1. Introduce the  `Type-SuperClass Elastic Scaling Solution(T-SC ESS)`.
  2. Introduce the `Goroutine-APSchedule Mode(G-APSM)`.

- #### **2020.10.20 v_4.5.2** 

  > **Major Update**

  1. These types of subscription links（ `Trojan`、`v2ray`、`ssr` ）are supported by multi-threaded federated collections.
  2. The document tree has been rewritten, and the old version of the software cannot run normally.
     -  :old_key: Update the `v2raycs Client` to the latest version.
  3. Add auto update function.

  > **Function Iteration** 

  1. Using `Redis` to take over the access business to improve distribution efficiency.
  2. Open get interface. Please refer to the manual for usage.
  3. `ConfinementTime` increased to `30s/e`.

## :eagle: 快速上手

- **软件获取**

  - 【方案一】：[**Windows10 64x <约17Mb>**](https://t.qinse.top/subscribe/v2ray云彩姬.zip) **||** [备用下载地址](https://yao.qinse.top/subscribe/v2ray云彩姬.zip)

  - 【方案二】：Clone项目

  ![Snipaste_2020-10-22_13-53-00](https://i.loli.net/2020/10/22/s9vC6RI7FtVJahe.png)

- **软件使用**

  运行`V2Ray云彩姬.exe` 即可启动[**v2ray云彩姬**](https://github.com/QIN2DIM/V2RayCloudSpider/blob/master/V2Ray云彩姬使用说明.md)获取订阅连接。


## :video_game: 进阶玩法

> `Tos`：该项目基于`Windows10`环境开发，Mac用户~~可能~~无法正常使用

- `/V2RaySpider1025`中存放该项目通用版本的源代码

- 运行`main.py`启动程序

- 安装依赖`当前目录：/V2RaycSpider1025`

  ```
  pip install -r requirements.txt -i https://pypi.tuna.tsinghua.edu.cn/simple/
  ```

- 修改配置` config.py`

### :balance_scale: 参数设置

- 请在`config.py`根据提示正确填写配置信息，并将整个项目文件`V2RaycSpider版本号`上传至服务器的`/qinse`文件夹

- 请确保服务器本项目前已安装`redis`并配置`Python3`开发环境

- 请确保服务器安装`google-chrome`，并配置了对应版本的`ChromeDriver`

    - 设置驱动执行权限

        给`chromedriver`设置可执行权限，如果您正在使用`Finalshell`l或`Xshell`等远程桌面登录方案，直接<kbd>右键</kbd>目标文件 -> `文件权限`即可给予文件**执行权限**；项目预装的`ChromeDriver`对应的`Chrome`版本为`v85.0.4183.102`若版本不同，请根据`config.py`中的提示替换目录中的对应文件，并根据上文所示操作基于驱动执行权限。

        ```python
        #Windows运行环境的驱动文件路径
        if 'win' in platform:
            CHROMEDRIVER_PATH = dirname(__file__) + '/BusinessCentralLayer/chromedriver.exe'
        #其他（Linux）运行环境的驱动文件路径
        else:
            CHROMEDRIVER_PATH = dirname(__file__) + '/BusinessCentralLayer/chromedriver'
        ```

- 运行`./main.py`即可跑动项目，详细操作流程请看`main.py`源码

    ```shell
    # 部署
    nohup python3 /qinse/V2RaycSpider1125/main.py deploy &
    ```

- 以上设置均在`main.py`以及`config.py`文件中有详细的设定说明，若有疑惑及报错请自行检索 或查看[v2ray云彩姬依赖拉取文档](https://shimo.im/docs/5bqnroJYDbU4rGqy/)（撰写中...）也可在issue中留言或者私信作者都可~方法总比困难多。

### :zap: 其他设置

- 使用`GET`请求，访问以下接口，既可获取`CrawlerSeq subscribe_link`（该资源来自`Redis`数据交换的分发缓存接口，作者会在未来版本将此类玩法拓展为基于垂直网络的数据挖掘模块并暴露更多的`API`）。
- 注：使用该方法获取的链接并不一定可用

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

  ​	首次运行可能会弹出提示

  ![3](https://i.loli.net/2020/10/06/MhwiZfOz3VdDPU5.png)

  ![3](https://i.loli.net/2020/10/06/gmLksO3HCtyWu9r.png)

## :world_map: 开源计划

- [x] 支持`Trojan-go`、`Trojan-gfw`机场的采集
- [x] 合并订阅链接消息队列，PC端可查看目前在库的`Subscribe Link`并择一获取
  - [x] 合并队列
  - [x] 查看链接
  - [x] 择一获取
- [ ] 逐渐停用`easygui`前端模块，开发跨平台视图交互模块
- [ ] 引入`呼吸节拍`中间件，让任务行为拟人化
- [ ] 兼容所有类型链接的贯通采集
- [ ] 前后端分离，拓展Flask包装中间件

## :email: 联系我们

> 本项目由海南大学机器人与人工智能协会提供维护

- [**Email**](mailto:RmAlkaid@outlook.com?subject=CampusDailyAutoSign-ISSUE) **||** [**Home**](https://a-rai.github.io/)

###  
