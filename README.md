# aligenie

home assistant custom component for tmall genie

basicly it's a gate and wrapper of Yonsm's gate in https://github.com/Yonsm/HAExtra/tree/master/hagenie



### 配置

* 将aligenie文件夹拷贝到home assistant的custom_components目录下
* 在配置文件configuration.yaml中添加：

``` yaml
aligenie:  
  expire_hours: 9999999
```

* 在个性化配置文件customize.yaml中为需要暴露给天猫精灵的设备添加设置项：

``` yaml
switch.printer:
  friendly_name: 打印机
  hagenie_deviceName: 机顶盒
  hagenie_deviceType: STB
  hagenie_zone: 书房
```

其中：

* hagenie_deviceName：设备名称，可以自由输入
* hagenie_deviceType：设备类型，取值范围参考https://open.bot.tmall.com/oauth/api/aliaslist中的所有value字段；
* hagenie_zone：设备区域，取值范围参考https://open.bot.tmall.com/oauth/api/placelist中的内容；

也可以借助HassAPP对每个实体进行配置。

### 天猫精灵开发平台

首先确保你的home assistant能在公网访问，并且配置有https域名（证书必须可以验证，端口可以不使用443端口），证书的问题可以参考：http://www.yunsean.com/tong-guo-tian-mao-jing-ling-kong-zhi-home/

1. 访问天猫精灵开放平台：https://iap.aligenie.com/console/skill/list
2. 创建一个“内容&IOT技能”，进入技能
3. 在“服务设置”中配置：

- 账户授权链接：https://yourdomain:port/auth/authorize
- Client ID：https://open.bot.tmall.com
- Client Secret：不填都可以，或者随便写，不写就弄一个home assistant的长效令牌给他
- 跳转 URL：https://open.bot.tmall.com/oauth/callback
- Access Token URL：https://yourdomain:port/auth/token
- 开发者网关地址：https://yourdomain:port/ali_genie_gate

其他项目留白，保存。

4. 进入“测试验证”，点击账户配置，应该就看到你家home assistant中的登录页面了。
5. 然后就可以打开天猫精灵APP看到你暴露的设备进行修改。