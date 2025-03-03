![](https://applepaydemo.apple.com/static/img/walletextensions/wallet-extensions-flow.4416c1ca0ec5b83c4843da6e9d96993b.png)
1. **The user initiates provisioning from Apple Wallet:**
2. **Apple Wallet to the issuer app
3. **The issuer app to Apple Wallet
4. **The user selects the issuer app in Apple Wallet:** The user can proceed with the issuer app’s extension by tapping the listed issuer under the "From Apps on Your iPhone" section of Apple Wallet.
5. **Apple Wallet to the issuer app:** Apple Wallet uses [`PKIssuerProvisioningExtensionAuthorizationResult`](https://developer.apple.com/documentation/passkit_apple_pay_and_wallet/pkissuerprovisioningextensionauthorizationresult) to interrogate the issuer app for determining the user’s authorization status. The authorization _UI extension_ extends a [`UIViewController`](https://developer.apple.com/documentation/uikit/uiviewcontroller/) from the issuer app to perform authentication. The _UI extension_ needs to be a subclass of [`PKIssuerProvisioningExtensionAuthorizationProviding`](https://developer.apple.com/documentation/passkit_apple_pay_and_wallet/pkissuerprovisioningextensionauthorizationproviding).

我们在执行到第五步时，点击“创兴银行”入口，提示“Cannot Add Card“，我们按要求实现了登录页，但没有被触发：
```
@interface NIBSWalletUIExtHandler : UIViewController<PKIssuerProvisioningExtensionAuthorizationProviding>
@property (nonatomic, copy, nullable) void(^completionHandler)(PKIssuerProvisioningExtensionAuthorizationResult result);
@end
```

我们检测到statusWithCompletion方法有执行，并正确回调了参数：
`- (void)statusWithCompletion:(void (^)(PKIssuerProvisioningExtensionStatus *))completion`
```
回调的参数
   status.passEntriesAvailable = YES;
   status.remotePassEntriesAvailable = NO
   status.requiresAuthentication = YES;
```
![[IMG_2572.png|200]]![[WechatIMG322.jpg|200]]


下面是我们扩展的配置信息：

UI extension的配置信息
![[截屏2025-02-24 18.22.09.png|600]]
![[截屏2025-02-24 18.27.28.png|600]]

non-UI extension的配置信息
![[截屏2025-02-24 18.22.55.png]]![[截屏2025-02-24 18.27.02.png|600]]、