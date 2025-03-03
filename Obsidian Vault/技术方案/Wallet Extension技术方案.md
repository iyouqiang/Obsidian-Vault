
#### Apple 指导文档

https://applepaydemo.apple.com/wallet-extensions
https://developer.apple.com/documentation/passkit/implementing-wallet-extensions

#### 项目要求

iOS 运行 14 或更高版本的iOS设备
Xcode 15或更高版本
测试设备： SEID需要注册到visa

https://developer.apple.com/forums/thread/767458

#### Apple Pay配置方式

**1、应用内配置：**

Implementing In-App Provisioning is a prerequisite for the configuration of Wallet Extensions
实施应用内配置是配置钱包扩展的先决条件，应用内配置至少需要 iOS 10.3 或您所在国家/地区应用内配置启动时通知的版本（以版本较高者为准）。

**2、Wallet Extension:**

The Wallet Extensions feature relies on two extensions：

a _UI extension_ and a _non-UI extension_. The issuer app needs a _non-UI extension_ to report on the status of the extension（如果不是库）, passes the app has available to add, and to perform the card data lookup—just like when adding payment passes to Apple Wallet from within the issuer app.

As for the _UI extension_, the issuer app needs a _UI extension_ to perform authentication of the user if the _non-UI extension_ reports that authentication is required. The _UI extension_ isn’t a redirect to the issuer app, but a separate screen that uses the same issuer app login credentials.


⚠️注意
==1、The Wallet Extensions experience starts in Apple Wallet. **Note: A user has to open and log in to the issuer app at least once for Apple Wallet to detect the extensions.**== 
==注意：用户必须打开并登录发行方应用至少一次，Apple Wallet 才能检测到扩展。==
==2、The implementation of In-App Provisioning is a prerequisite to the configuration of Wallet Extensions.== 


**Wallet Extension挂卡步骤**：

1、First, a user taps the add button (+) in the top right corner of Apple Wallet. 

2、The next screen Wallet displays to the user includes a "From Apps on Your iPhone" section. 

3、Issuer apps that have implemented Wallet Extensions will appear in a list under the "From Apps on Your iPhone" section if the issuer app has at least one available payment pass that is not currently in Wallet.

4、A user can, then, tap on a listed issuer to begin the provisioning experience using the issuer’s Wallet Extension. 

5、The extension will return user to Wallet automatically once the provisioning is complete.
  ![[wallet-extensions-experience.12e2361972fd43d1c27e9d04e612e7e2.png]]  
**Wallet Extension flow**

![[wallet-extensions-flow.4416c1ca0ec5b83c4843da6e9d96993b.png|500]]

**1、The user initiates provisioning from Apple Wallet:** The user initiates adding a payment pass in Apple Wallet by tapping the add button (+) in the top right of Apple Wallet. The user must open and log in to the issuer app at least once for Apple Wallet to detect the extensions.
  
2、**Apple Wallet to the issuer app:** The principal class of the _non-UI extension_ needs to be a subclass of [PKIssuerProvisioningExtensionHandler](https://developer.apple.com/documentation/passkit_apple_pay_and_wallet/pkissuerprovisioningextensionhandler). Apple Wallet uses [PKIssuerProvisioningExtensionStatus](https://developer.apple.com/documentation/passkit_apple_pay_and_wallet/pkissuerprovisioningextensionstatus), which is passed to the extension handler, to interrogate the issuer app. The interrogation determines the availability of the extension, whether any payment passes are available to add, and whether adding a payment pass requires authentication.

**3、The issuer app to Apple Wallet:** The [status(completion:)](https://developer.apple.com/documentation/passkit_apple_pay_and_wallet/pkissuerprovisioningextensionhandler/3571367-status) method within [PKIssuerProvisioningExtensionHandler](https://developer.apple.com/documentation/passkit_apple_pay_and_wallet/pkissuerprovisioningextensionhandler) indicates whether a payment pass is available to add to Apple Pay and whether adding the pass requires authentication. The issuer app icon displays in Apple Wallet under "From Apps on Your iPhone" if the user logged in the issuer app at least once and there is at least one payment pass available to add to Apple Pay.

- [passEntriesAvailable](https://developer.apple.com/documentation/passkit_apple_pay_and_wallet/pkissuerprovisioningextensionstatus/3571376-passentriesavailable): The issuer app declares whether a payment pass is available to add to an iPhone.
- [remotePassEntriesAvailable](https://developer.apple.com/documentation/passkit_apple_pay_and_wallet/pkissuerprovisioningextensionstatus/3606587-remotepassentriesavailable): The issuer app declares whether a payment pass is available to add to an Apple Watch.
- [requiresAuthentication](https://developer.apple.com/documentation/passkit_apple_pay_and_wallet/pkissuerprovisioningextensionstatus/3571377-requiresauthentication): The issuer app declares whether adding a payment pass requires the user to authenticate in the authorization _UI extension_ that the issuer app provides

- **Important**
- ==The system needs to invoke the handler within 100 ms, or the extension does not display to the user in Apple Wallet.== 100ms处理完，否则不会展示UI扩展

4、**The user selects the issuer app in Apple Wallet:** The user can proceed with the issuer app’s extension by tapping the listed issuer under the "From Apps on Your iPhone" section of Apple Wallet.

5、**Apple Wallet to the issuer app:** Apple Wallet uses [PKIssuerProvisioningExtensionAuthorizationResult](https://developer.apple.com/documentation/passkit_apple_pay_and_wallet/pkissuerprovisioningextensionauthorizationresult) to interrogate the issuer app for determining the user’s authorization status. The authorization _UI extension_ extends a [UIViewController](https://developer.apple.com/documentation/uikit/uiviewcontroller/) from the issuer app to perform authentication. The _UI extension_ needs to be a subclass of [PKIssuerProvisioningExtensionAuthorizationProviding](https://developer.apple.com/documentation/passkit_apple_pay_and_wallet/pkissuerprovisioningextensionauthorizationproviding).

**6、The issuer app to the user:** The issuer app performs authentication of the user as part of their existing security framework, such as Face ID, Touch ID, or another authentication method subject to issuer requirements. Many issuer apps rely on biometric authentication like Face ID and Touch ID to provide the most seamless experience for the user.

7、**The issuer app to Apple Wallet:** The result of the [completionHandler](https://developer.apple.com/documentation/passkit_apple_pay_and_wallet/pkissuerprovisioningextensionauthorizationproviding/3571360-completionhandler), an instance property of [PKIssuerProvisioningExtensionAuthorizationProviding](https://developer.apple.com/documentation/passkit_apple_pay_and_wallet/pkissuerprovisioningextensionauthorizationproviding), indicates whether the user has authorization to add a payment pass.

- [authorized](https://developer.apple.com/documentation/passkit_apple_pay_and_wallet/pkissuerprovisioningextensionauthorizationresult/authorized): The issuer declares that the user successfully authorized adding a payment pass.
- [canceled](https://developer.apple.com/documentation/passkit_apple_pay_and_wallet/pkissuerprovisioningextensionauthorizationresult/canceled): The issuer declares that the user canceled authorization or doesn’t have authorization to add the payment pass.

8、**Apple Wallet to the issuer app:** After authorization, Apple Wallet uses [PKIssuerProvisioningExtensionPaymentPassEntry](https://developer.apple.com/documentation/passkit_apple_pay_and_wallet/pkissuerprovisioningextensionpaymentpassentry) to interrogate the issuer app for determining the list of payment passes available to add to the user’s iPhone and Apple Watch.


>With successful authorization, the _non-UI_ extension is capable of fetching all data necessary to create and provision payment passes for a reasonable period of time.

>For Apple Wallet to correctly show the issuer app icon, the app needs to exclude any passes the user has already added to their device from the list of available passes. Passes need to include the extension’s bundle identifier in associatedApplicationIdentifiers to ensure accurate status of existing passes in Apple Wallet. To learn more about this identifier key, see [PNO Pass Metadata Configuration](https://applepaydemo.apple.com/wallet-extensions#pnoPassMetadata).

>Issuer can use [PKPassLibrary().canAddSecureElementPass(primaryAccountIdentifier:)](https://developer.apple.com/documentation/passkit_apple_pay_and_wallet/pkpasslibrary/3543354-canaddsecureelementpass) to determine if a pass has already been provisioned.

  
9、**The issuer app to Apple Wallet:** The completion handlers return an array of payment passes that are available to add to the user’s iPhone ( [passEntries(completion:)](https://developer.apple.com/documentation/passkit_apple_pay_and_wallet/pkissuerprovisioningextensionhandler/3571366-passentries) ) and Apple Watch ( [remotePassEntries(completion:)](https://developer.apple.com/documentation/passkit_apple_pay_and_wallet/pkissuerprovisioningextensionhandler/3606586-remotepassentries) ). This list of eligible payment passes displays to the user.

- [art](https://developer.apple.com/documentation/passkit_apple_pay_and_wallet/pkissuerprovisioningextensionpassentry/3571370-art): The image representing the card that displays to the user. The image needs to have square corners and can’t include personally identifiable information like user’s name or account number. See the card art requirements available in the Functional Requirements for Apple Pay and Direct NFC Access. Please contact your Apple project contact, PNO, or service provider relationship manager for documentation on Functional Requirements for Apple Pay and Direct NFC Access.
- [title](https://developer.apple.com/documentation/passkit_apple_pay_and_wallet/pkissuerprovisioningextensionpassentry/3571373-title): The name of the payment pass that displays to the user.
- [identifier](https://developer.apple.com/documentation/passkit_apple_pay_and_wallet/pkissuerprovisioningextensionpassentry/3571371-identifier): An internal value the issuer uses to identify the card. This identifier needs to be unique.
- [PKAddPaymentPassRequestConfiguration](https://developer.apple.com/documentation/passkit_apple_pay_and_wallet/pkaddpaymentpassrequestconfiguration): The configuration data for setting up and displaying a view controller that lets the user add a payment pass.

>Don’t return payment passes that are already present in the user’s pass library. The system needs to invoke the handler within 20 seconds, or it treats the call as a failure and the attempt stops.

**10、The user selects the passes to add:** The user selects one or more cards to provision.

11、**Apple Wallet to the issuer app:** Apple Wallet uses the completion handler [generateAddPaymentPassRequestForPassEntryWithIdentifier](https://developer.apple.com/documentation/passkit_apple_pay_and_wallet/pkissuerprovisioningextensionhandler/3571365-generateaddpaymentpassrequestfor?language=objc) to interrogate the issuer app for the [PKAddPaymentPassRequest](https://developer.apple.com/documentation/passkit_apple_pay_and_wallet/pkaddpaymentpassrequest) and supplies the identifier, configuration data, certificates, nonce, and nonce signatures for the selected payment passes.

>==The system needs to invoke the handler within 20 seconds, or it treats the call as a failure and the attempt stops.==  此处接口需要在20s内处理完成


12、**The issuer app to Apple Wallet:** The completion handler, then, returns a [PKAddPaymentPassRequest](https://developer.apple.com/documentation/passkit_apple_pay_and_wallet/pkaddpaymentpassrequest), which Apple Wallet uses to provision the pass.


--------

### 技术实现与测试

##### iOS端实现

**1、如何登录授权？**

If you already have a ==shared framework== responsible for the user authentication, you can call it directly from the UI Extension. ==If not, you can copy and reuse the containing issuer app’s login logic into the extension to perform the user authentication==. If a subclass of [UIViewController](https://developer.apple.com/documentation/uikit/uiviewcontroller/) is used for the containing issuer app’s login view, reuse the containing app’s login code by copying the code logic over into the UI extension’s principal class (WUIExtHandler). Then, refactor the code to include and invoke the [completionHandler](https://developer.apple.com/documentation/passkit_apple_pay_and_wallet/pkissuerprovisioningextensionauthorizationproviding/3571360-completionhandler) based on the status of the user’s authorization.

**2、图片配置**

- **What are the size and resolution requirements for the card images?**  
    The card image should follow the same requirements as in the Functional Requirements for Apple Pay and Direct NFC Access. ==(1536 x 969 resolution, <4 MB,== squared corners, no chip contacts, and so forth). Please contact your Apple project contact, PNO, or service provider relationship manager for more information on Functional Requirements for Apple Pay and Direct NFC Access.

**3、The extensions’ bundle IDs need to be added to the associatedApplicationIdentifier at the PNO. iOS now supports wildcard bundle identifiers. Issuers also need to update all the existing passes in Apple Wallet, using the PNO APIs.

- 在 `associatedApplicationIdentifier` 中添加扩展的 Bundle ID。这是通过 Apple Pay and Wallet 中的 PNO（Pass Network Operations）API 完成的。
- iOS 现在支持通配符（wildcard）Bundle ID，例如：`com.company.*`。这意味着您可以一次性支持多个扩展的 Bundle ID。
- 
- 登录 **Apple Developer Account**，并进入 Apple Wallet 配置。
- 找到 **Pass Type ID** 或 **Merchant Identifier** 的配置页面。
- 编辑 `associatedApplicationIdentifier`，将需要的扩展的 Bundle ID 添加到列表中（支持通配符）。![[截屏2025-02-13 09.23.44.png]]

**Extension使用注意**

 **1、iOS Extension是否可以发起网络请求**

在 iOS Extension（如 Today Widget、Share Extension、Notification Service Extension 等）中，可以发起网络请求，但需要注意以下几点：

**支持的网络请求方式**

- 可以使用 `NSURLSession`、`URLRequest` 等 API 发起 HTTP 请求。
- 可以集成第三方网络库（如 `Alamofire` 或 `AFNetworking`），但需要保证其符合 Extension 的限制。

 **注意事项**

- **时间限制**  
    Extension 的生命周期有限（如 Notification Service Extension 最多 30 秒），需要确保网络请求能在规定时间内完成。
    
- **后台运行**  
    Extension 不支持后台运行，即使网络请求未完成，系统可能会终止 Extension。
    
- **数据共享**  
    如果需要在主应用和 Extension 间共享网络请求结果，可以使用 `App Groups` 或 `NSUserDefaults`（通过 App Group 配置）来共享数据。
    

**2、iOS Extension包体大小限制**

Apple 对 Extension 的大小并没有直接规定硬性限制，但以下是相关限制：

**App 总体大小**

- 应用的总大小（包括主应用和所有 Extensions）受到 Apple 的限制。上传到 App Store 的 `.ipa` 文件解压后不能超过 4GB。

 **Extension 的大小优化建议**

- **移除不必要的资源**  
    确保 Extension 仅包含运行所需的资源和代码，避免嵌入主应用中不必要的资源文件。
    
- **动态加载资源**  
    尽量避免在 Extension 中打包大型资源，可以通过网络请求动态加载资源。
    
- **减少依赖库**  
    使用更轻量化的第三方库，避免将过多依赖库打包到 Extension 中。
    
- **Bitcode 和架构优化**  
    如果不需要支持所有架构，可以移除不必要的架构（如通过 `lipo` 工具）。

******
##### 服务端接口

**1、获取App信用卡条目**

请求接口：**creditBind/queryMountedCardListByWallet**
返回数据：
```
     cardList =     (
                 {
             cardBinImage = 1;
             cardBinType = 8;
             cardCategory = VISA;
             cardStatus = 0;
             cardType = VISA;
             creditNo = 4423828220468024;
             expiryDate = 2804;
             phone = 99995583;
             cardholderNamee = Ng Po Lam;
             primaryAccountSuffix = 8024;
         }
     );
```

**2、加密信用卡数据**

接口：**creditBind/encrytedPassData**
回传数据封装为PKAddPaymentPassRequest类型回传给 Apple

**3、数据流转流程**
* 启动APP
* 登录
* 请求服务器接口，获取未绑定的Apple Wallet的信用卡新
* 存储信用卡信息到手机指定路径
* 打开Wallet唤起Extension应用
* Extension获取本地存储的信用卡信息传给Apple
* 选择需要绑定的信用卡片
* 完成绑卡


*****

##### 测试流程<!-- uat&prd -->

>==用户至少登录过一次 iOS 发卡机构应用，并且至少有一个付款凭证可以添加到 Apple Pay，则发卡机构应用图标会显示在 Apple Wallet 中的“来自 iPhone 上的应用”下。==

**UAT环境测试**

在uat环境，暂不支持 Wallet Extension 完整流程测试，需要上传到生产环境包到TestFlight进行测试; 暂时只支持uat环境获取信用卡信息测试，Extension登录页测试

==测试方式==

**1、工程配置修改，打包时开发手动修改**

将 NSExtensionPointIdentifier 更改为 com.apple.ui-services
```
<key>NSExtensionPointIdentifier</key>
<string>com.apple.PassKit.issuer-provisioning.authorization</string>

<key>NSExtensionPointIdentifier</key>
<string>com.apple.ui-services</string>
```

修改前：![[截屏2025-02-13 10.05.52.png]]
修改后：![[截屏2025-02-13 10.05.21.png]]

**2、安装APP进行登录**
启动APP，进行登录，登录成功自动请求信用卡数据并存储到本地

**3、打开Extension的进行登录测试**
* 打开备忘录，编辑随意内容
* 点击分享,如下图：
![[IMG_2557.png|180]]

* 上滑系统弹出的分享页，找到uat扩展
* 点击该选项弹出登录页
![[IMG_2556.png|180]]

* ==登录界面展示时会弹出获取的信息卡信息，仅uat环境调试使用，正式环境不会展示==
* 如果主APP开启了人脸验证，登录页会显示对应的人脸验证按钮
* 登录操作完成，弹窗提示，登录页自动关闭
![[IMG_2559.png|180]]

****

**生产环境测试**

**同上述：Wallet Extension挂卡步骤**：

在TestFlight下载APP，启动APP并成功登录，然后打开苹果 Wallet 应用，按下述流程操作：

1. 点击 Apple Wallet 右上角的添加按钮 (+)。

2. 接下来，Wallet 会显示一个界面，其中包括一个 "来自您 iPhone 上的应用" 选项。

3. 如果APP已实现 Wallet 扩展，并且该应用至少有一个未在 Wallet 中的有效支付凭证，那么APP将出现在 "来自您 iPhone 上的应用" 部分的列表中。

4. 用户可以点击列表中发行方的APP，开始使用该发行方APP的 Wallet 扩展进行配置。

5. 配置完成后，扩展会自动将用户返回到 Wallet
  ![[wallet-extensions-experience.12e2361972fd43d1c27e9d04e612e7e2.png]]
### 新增绑卡提示语

