
### 环境配置

**WiFi：**
dtoap   chbuat2022
dtoap5G   chbuat2022 (代码获取需链接5g网络)

**源码管理**
创兴源码地址
http://192.168.1.146:8080/ynet_team/chb_mobile_hk_ios
ssh://git@192.168.1.146:10222/ynet_team/chb_mobile_hk_ios.git
SDK源码地址
http://192.168.1.146:8080/root/chb_ynetflame_ios.git

**电脑设备账号：**
MLYnet07
1q2w3e4r!

### 1、**项目整体架构和模块划分** 
猎豹架构，了解项目基座搭建方式即可
https://www.yuque.com/liebaodoc/pf9y7h/zd10dn

### 2、**项目介绍**

**代码环境配置**

(1) 全局配置：CHMobileBank_Header
(2) 猎豹接口配置：meta.config
(3) Target代码变量区分 CHMobileBank_UAT/PRE/PRDPRE
```
#ifdef CHMobileBank_DEV
// 测试
#elif defined CHMobileBank_SIT
// web
#elif defined CHMobileBank_UAT
// 测试常用环境

#elif defined CHMobileBank_PRE
// 预发环境

#elif defined CHMobileBank_PRDPRE
// 生产环境
#else
    chHost = CHBank_Prd;
#endif
```

### 3、**基础模块**

1、js&OC互调使用方案，使用范式、注意事项，新增方式
[https://www.yuque.com/liebaodoc/pf9y7h/owyiyk](https://www.yuque.com/liebaodoc/pf9y7h/owyiyk) 
==使用js类名隐射调用==
映射文件：Poseidon-Extra-Config.plist 
类文件夹：ChBank_JsApiExtension

2、Cheetah_FloorTemplate 楼层配置说明，使用场景和范式？


3、CHBank_tradeLink模块说明，使用场景和范式？

4、Cheetah_MyRpc模块说明，使用场景和范式？

5、路由模块使用范式？Cheetah_JumpMoudle

6、网络模块使用范式？ YNETRpcService

7、楼层模版使用？

### 4、**业务模块**

**启动**

1、initCacheFloorData楼层数据初始化，使用场景, APP展示的样式，增删楼层模版范式？

2、initRPC初始化拦截器，使用场景，原理，注意事项？

3、[[MediatorService sharedInstance] startServices] 启动服务的作用？

4、楼层数据样式如何切换更新的？

5、初始化菜单黑名单管理器 [[MenuAuthorityManager instance]initData]： 黑名单是什么？

6、YNETTabBarViewController、YNETHomeViewController、DFNavigationController 主页面

**登录**

ChBankLoginViewController

登录业务流程，输入账号登录成功：

登录业务校验

    LoginConfigStep_start = 0,

    LoginConfigStep_1,//校验是否签协议   原生  push

    LoginConfigStep_2,//强制修改密码提示   原生    push  ，需要重新登录

    LoginConfigStep_3,//修改密码警告提示,只要登录就提示   alert push ，

    LoginConfigStep_4,//T24手机号码处理 alert

    LoginConfigStep_5,//设备兼容性警告提示  alert

LoginConfigStep_6,//老softtoken 验证处理提醒 登录后验证 alert push

AfterLoginConfigStep_start = 0,

AfterLoginConfigStep_1,//新用户开流保提示 新用户开通softtoken提示框    

AfterLoginConfigStep_2,//ApplePay 广告页弹窗  

AfterLoginConfigStep_3,//ApplePay 挂卡提示

AfterLoginConfigStep_4,//保险模块，白名单用户判断

 登录认证 YESSafeTokenManager， 开启认证

**首页/****转账/投资/我的**

1、 界面初始化，楼层模版关联，字段说明文档，新增流程，编码范式？

楼层组件清单： https://www.yuque.com/liebaodoc/pf9y7h/wyqm9cnvzabro4up

2、 楼层组件界面事件响应 floorTemplateJumpEvent

3、 时尚版、简洁版切换，UI布局

**支付**

**搜索**

**推送**

**路由**

**埋点**

**离线**

1、离线服务使用场景，加载时机，数据存储方式，注意事项？

2、Cheetah_Flame_Offline.bundle 压缩内容？

### **5****、微应用和微服务**

### **6****、测试**

（1）APP的测试，测试账号，测试环境

（2）微应用测试及调试方式

### **7****、sdk模块**

Softtoken-isprint？

Softtoken-tradeLink

极光推送

密码安全控件

加固

EKYC 人脸

ApplePay

埋点

### **8****、项目开发流程：****业务需求、****评审、****素材、开发、****测试、****打包发布****等？**

**需求路径**

1、 电脑共享磁盘  此电脑>share>科技开发文档交互>02项目资料>…