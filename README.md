<p align="center">
    <h1 align="center">scripts</h1>
</p>
<p align="center">
    一些脚本，每天定时自动签到
    <br />
    <br />
    <a href="https://github.com/sudojia/scripts/issues/new">上报Bug、  意见反馈</a>
  </p>



- [💍介绍](#介绍)
- [😍特点](#特点)
- [👗适用人群](#适用人群)
- [🔑*Env*](#Env)
- [⚠️注意事项](#%EF%B8%8F注意事项)
- [🔛使用](#使用)
- [🎯TODO](#TODO)
- [🕛历程](#历程)

## 💍介绍

基于 GitHub Actions 每天定时自动签到脚本，支持多账号，目前仅支持 `SSPANEL` 、[掘金社区](https://juejin.cn/)，[葫芦侠三楼](https://www.huluxia.com/)

多个消息平台（Telegram、Server 酱、Bark、PushPlus、钉钉等）服务推送。

## 😍特点

- ~~💰~~ 免费（项目运行在 GitHub Actions 上.）
- 🔗 多网站
- 📯 多账号

## 👗适用人群

- 老少皆宜

- 有这个需求的人

- SSPANEL 断签 7 天或者断签某天就会把你号给删的那种 ✈️

  ![images](https://cdn.jsdelivr.net/gh/sudojia/sspanel_checkin/img/fources.jpg)
  
- 掘金签到获取矿石，用于抽奖、兑换！

- 葫芦侠...貌似没什么卵用（应网友需求而写）

## 🔑*Env*

`Settings - Secrets - New repository secret`

如果你需要签到 SSPANEL 面板，就填写 `SITE_ACCOUNTS` 变量

如果你需要签到掘金，就填写 `JUEJIN_COOKIE` 变量

### SSPANEL

|      Name       |                      Value                      |                             说明                             |
| :-------------: | :---------------------------------------------: | :----------------------------------------------------------: |
| `SITE_ACCOUNTS` | 要执行签到的`网站,账号:密码`，多个请用 `&` 分割 | 单账号填写规则 e.g：`https://paolu.com,aaa@gmail.com:123456`<br/>多个填写规则：`https://aaa.com,aaa@gmail.com:aaa&https://bbb.com,bbb@gmail.com:bbb&...以此类推`<br/>中文说明：`网站,账号:密码`，多个：`网站,账号:密码&网站,账号:密码`<br/>网站与账号密码之间用`英文逗号`（`,`）分割，账号与密码之间用`英文冒号`（`:`）分割 |

### 掘金

|      Name       |    Value    |                             说明                             |
| :-------------: | :---------: | :----------------------------------------------------------: |
| `JUEJIN_COOKIE` | 掘金 Cookie | 打开[掘金社区](https://juejin.cn/) F12，选择 Application，点击 Cookies<br/>填写规则：`sessionid=xxxxxxxxx` |

### 葫芦侠

|      Name      |         Value          |                             说明                             |
| :------------: | :--------------------: | :----------------------------------------------------------: |
| `HLX_ACCOUNTS` | 账号和密码，支持多账户 | 填写规则：188888888888@`MD5加密密码`<br/>密码必须是 MD5 加密后的密码<br/>[MD5在线加密](https://md5jiami.bmcx.com/) 选择 32 位小写<br/>多个填写规则：18888888888@MD5密码&16666666666@MD5密码&...<br/>账号和密码直接用 `@` 分割，多个用 `&` |

### 消息推送变量（可选）

|       Name        |                             归属                             |  属性  |                             说明                             |
| :---------------: | :----------------------------------------------------------: | :----: | :----------------------------------------------------------: |
|    `PUSH_KEY`     |                      微信 server 酱推送                      | 非必须 | server 酱的微信通知[官方文档](http://sc.ftqq.com/3.version)，已兼容 [Server 酱·Turbo 版](https://sct.ftqq.com/) |
|    `BARK_PUSH`    | [BARK 推送](https://apps.apple.com/us/app/bark-customed-notifications/id1403753865) | 非必须 | IOS 用户下载 BARK 这个 APP，填写内容是 app 提供的`设备码`<br>例如：https://api.day.app/123 ，那么此处的设备码就是 `123` |
|   `BARK_SOUND`    | [BARK 推送](https://apps.apple.com/us/app/bark-customed-notifications/id1403753865) | 非必须 | bark 推送声音设置，例如 `choo`，具体值请在 `bark`-`推送铃声`-`查看所有铃声` |
|  `TG_BOT_TOKEN`   |                        Telegram 推送                         | 非必须 | `TG_BOT_TOKEN` 和 `TG_USER_ID` 两者必需<br>填写自己申请 [@BotFather](https://t.me/BotFather)的 Token<br>如 `10xxx4:AAFcqxxxxgER5uw` |
|   `TG_USER_ID`    |                        Telegram 推送                         | 非必须 | `TG_BOT_TOKEN` 和 `TG_USER_ID` 两者必需<br/>私聊它 [@userinfobot](https://t.me/userinfobot) 随便发点什么即可获取到自己的 ID |
|  `DD_BOT_TOKEN`   |                           钉钉推送                           | 非必须 | (`DD_BOT_TOKEN` 和 `DD_BOT_SECRET` 两者必需)[官方文档](https://developers.dingtalk.com/document/app/custom-robot-access) <br>只需 `https://oapi.dingtalk.com/robot/send?access_token=XXX` 等于 `=` 符号后面的 XXX 即可 |
|  `DD_BOT_SECRET`  |                           钉钉推送                           | 非必须 | (`DD_BOT_TOKEN` 和 `DD_BOT_SECRET` 两者必需) ，密钥，机器人安全设置页面，加签一栏下面显示的 SEC 开头的 `SECXXXXXXXXXX` 等字符，注：钉钉机器人安全设置只需勾选`加签`即可，其他选项不要勾选 |
|    `QYWX_KEY`     |                      企业微信机器人推送                      | 非必须 | 密钥，企业微信推送 webhook 后面的 key [详见官方说明文档](https://work.weixin.qq.com/api/doc/90000/90136/91770) |
|  `IGOT_PUSH_KEY`  |                          iGot 推送                           | 非必须 | iGot 聚合推送，支持多方式推送，确保消息可达。 [参考文档](https://wahao.github.io/Bark-MP-helper ) |
| `PUSH_PLUS_TOKEN` |                        pushplus 推送                         | 非必须 | 微信扫码登录后一对一推送或一对多推送下面的 token(您的 Token)<br>[官方网站](http://www.pushplus.plus/) |
| `PUSH_PLUS_USER`  |                        pushplus 推送                         | 非必须 | 一对多推送的 “群组编码”（一对多推送下面 -> 您的群组(如无则新建)->群组编码）<br>注：(1、需订阅者扫描二维码  2、如果您是创建群组所属人，也需点击“查看二维码”扫描绑定，否则不能接受群组消息推送)<br>只填 `PUSH_PLUS_TOKEN` 默认为一对一推送 |

## ⚠️注意事项

SSPANEL 签到暂不支持密码带  `,`  与  `:`  的字符！

SSPANEL 签到同一个网站，多个账号，导致第一个能成功，第二个总是失败 - **待解决**

**SSPANEL 签到暂不支持带有图形验证码的机场网站！**

## 🔛使用

1. 右上角 Fork 该项目

2. 在仓库的  `Settings - Secrets - New repository secret`  添加变量，变量说明请看  [🔑Env](#env)

3. 点击仓库中的 Actions，点击图中所示

   ![image](https://cdn.jsdelivr.net/gh/sudojia/sspanel_checkin/img/20210927171440.jpg)

   看图

   ![image](https://cdn.jsdelivr.net/gh/sudojia/sspanel_checkin/img/20210927171527.jpg)

   继续看图

   ![image](https://cdn.jsdelivr.net/gh/sudojia/sspanel_checkin/img/20210927171547.jpg)

   执行成功，如图，如果报错，不妨提个 [issues](https://github.com/sudojia/sspanel_checkin/issues/new)

   ![image](https://cdn.jsdelivr.net/gh/sudojia/sspanel_checkin/img/20210927171605.jpg)


## 🎯TODO

- [x] 多账号
- [x] 多网站
- [x] 消息推送
- [ ] 掘金社区一键 soha
- [ ] ...

## 🕛历程

- 2022-01-20 10:18 - 添加掘金社区签到、抽奖，应网友要求，添加葫芦侠签到（一开始还以为看剧的葫芦...）

- 2021-09-27 15:22 - 更改写法，采用一个变量，单个规则为：`网站,账号:密码`  多个：`网站,账号:密码&网站,账号:密码`

- 2021-09-26 11:18 - 添加多个消息推送（Telegram、server 酱、Bark、PushPlus、钉钉等）

- 2021-09-26 0:04 - 支持多账号、多网站！
- 2021-09-25 22:39 - 第一版推出，仅支持单网站、单账号签到
