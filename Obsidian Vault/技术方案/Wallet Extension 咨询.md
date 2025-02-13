
### 测试流程

1、完成Wallet Extens的代码实现
2、APP打包上传到TestFlight
3、启动APP，并完成登录，将未绑定钱包的信用卡存储到扩展的共享容器中
4、通过UI调试，在扩展中，我们能够获取到信用卡信息，能够完成登录授权

打开Wallet APP，没有展示指导文档中的 "From Apps on Your iPhone" 选项，如下图：
![[截屏2025-02-11 19.15.32.png]]


### 工程配置

#### Wallet UI Extension

**info.plist 配置**
![[截屏2025-02-11 19.02.26.png]]

**Capability配置**
![[截屏2025-02-11 19.02.53.png]]
**登录页认证**
```
@interface NIBSWalletUIExtHandler : UIViewController<PKIssuerProvisioningExtensionAuthorizationProviding>

@property (nonatomic, copy, nullable) void(^completionHandler)(PKIssuerProvisioningExtensionAuthorizationResult result);

@end

// 登录完成回调
self.completionHandler(PKIssuerProvisioningExtensionAuthorizationResultAuthorized);

```

#### Wallet None Extension

**info.plist 配置**
![[截屏2025-02-11 19.06.56.png]]
**Capability配置**
![[截屏2025-02-11 19.22.26.png]]