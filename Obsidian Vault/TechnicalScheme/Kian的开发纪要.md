------------------
工号： 111321 

邮箱：
https://mail.belink.com/
gongyq1@belink.com
gyq123456

内网邮箱密码：CHbank12

结构图绘制工具：https://app.diagrams.net/

------------------
vpn
账号权限和VPN说明
https://www.yuque.com/liebaodoc/pf9y7h/qflgfk?singleDoc# 《账号权限和VPN说明》 密码：wwd6

------------------
组织知识库
https://alidocs.dingtalk.com/i/spaces/oJRz0dnMa403wzLZ/overview

------------------
Windows: https://atrustcdn.sangfor.com/standard/windows/2.3.10.65/aTrustInstaller.exe
Mac: https://atrustcdn.sangfor.com/standard/mac/2.3.10.65/aTrustInstaller.pkg
下载完成以后，接入地址修改为：https://111.204.125.248:3441

------------------
gitlab:
http://git.ynet.io

------------------

WiFi：
dtoap   chbuat2022
dtoap5G   chbuat2022

源码管理
创兴源码地址
http://192.168.1.146:8080/ynet_team/chb_mobile_hk_ios
ssh://git@192.168.1.146:10222/ynet_team/chb_mobile_hk_ios.git
SDK源码地址
http://192.168.1.146:8080/root/chb_ynetflame_ios.git

gongyouqiang
chbank12

UAT验证码查询地址：OTP查询 客户编号
http://10.98.33.100:10008/#/

-------------------
创兴通账号：
youqianggong    
123456

电脑设备账号：
MLYnet07
1q2w3e4r!

邮箱密码：CHbank12

nucky139 GZX9@lxx
1774466001 Uat000000@

-------------------
/usr/local/bin/pod install
git branch <本地分支名> <远程仓库名>/<远程分支名>


香港测试苹果账号：

账号
charlescoffey2436@gmail.com
密码
Tt557755
密保
朋友q333----工作w222---父母e111----1990-01-


*******
#转换crt证书到PEM再到cer，不可直接转否则会有格式问题

#openssl x509 -in www_ibanking_chbank_com.2024.crt   -out prdcer20251218.pem -outform PEM

#openssl x509 -inform pem -in  prdcer20251218.pem    -outform der -out prdcer20251218.cer


AI
https://chatgpt.com/c/67bbd9bf-3778-8010-b232-0d702592f376
https://chat.deepseek.com/

document文档新增测试日志

```
+ (void)logWalletExtensionMsg:(NSString *)msg {

#ifdef DEBUG

    // 生产环境日志功能禁用

    dispatch_async(dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_BACKGROUND, 0), ^{

        NSURL *containerURL = [YNETAppGroupManager appGroupManager].appGroupSharedContainerDirectory;

        // 设备当前时间

        NSString *localTimeString = [NSDateFormatter localizedStringFromDate:[NSDate date] dateStyle:NSDateFormatterMediumStyle timeStyle:NSDateFormatterMediumStyle];

        NSURL *logFileURL = [containerURL URLByAppendingPathComponent:@"logs.txt"];

        NSString *logEntry = [NSString stringWithFormat:@"\nWallet Extension Logs %@-----------:\n%@\n\n", localTimeString, msg];

        // 如果文件不存在，则创建文件

        if (![NSFileManager.defaultManager fileExistsAtPath:logFileURL.path]) {

            NSError *error = nil;

            NSString *initialContent = @""; // 可以设置初始内容

            [initialContent writeToURL:logFileURL atomically:YES encoding:NSUTF8StringEncoding error:&error];

            if (error) {

                NSLog(@"Error creating log file: %@", error.localizedDescription);

            } else {

                NSLog(@"Log file created successfully.");

            }

        }

        NSFileHandle *fileHandle = [NSFileHandle fileHandleForWritingAtPath:logFileURL.path];

        if (fileHandle) {

            [fileHandle seekToEndOfFile];

            [fileHandle writeData:[logEntry dataUsingEncoding:NSUTF8StringEncoding]];

            [fileHandle closeFile];

        }

    });

#endif

}



// 捞取 Wallet Extension

+ (void)checkAndUploadLogs {

    // 异步读取日志文件

    dispatch_async(dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_BACKGROUND, 0), ^{

        // 获取主应用的 Documents 目录路径

        NSString *localTimeString = [NSDateFormatter localizedStringFromDate:[NSDate date] dateStyle:NSDateFormatterMediumStyle timeStyle:NSDateFormatterMediumStyle];

  

        NSArray *paths = NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, YES);

        NSString *documentsDirectory = [paths firstObject];

        NSURL *documentsLogFileURL = [NSURL fileURLWithPath:[documentsDirectory stringByAppendingPathComponent:[NSString stringWithFormat:@"%@_logs.txt", localTimeString]]];

        // 获取共享容器的路径

        NSFileManager *fileManager = [NSFileManager defaultManager];

        NSURL *containerURL = [fileManager containerURLForSecurityApplicationGroupIdentifier:appGroupID];

        NSURL *logFileURL = [containerURL URLByAppendingPathComponent:@"logs.txt"];

        if ([[NSFileManager defaultManager] fileExistsAtPath:logFileURL.path]) {

            NSData *logData = [NSData dataWithContentsOfURL:logFileURL];

            if (logData.length > 0) {

                // 上传日志数据

                NSString *logString = [[NSString alloc] initWithData:logData encoding:NSUTF8StringEncoding];

                if (logString) {

                    NSLog(@"Log Data: \n %@", logString);

                    /*

                     id<ChBank_TrackEventProtocol> trackService = [YNETContextGet() findServiceByName:@"ChBank_TrackEventProtocol"];

                     [trackService trackEvent:@"Wallet_Extension" parameters:@{@"logs":logString}];

                     */

                } else {

                    NSLog(@"Failed to convert data to string.");

                }

                // 上传后清空日志文件

                // [YNETDataHandleHelper clearLogFileAtURL:logFileURL];

                NSError *error = nil;

                // 将数据写入到 Documents 文件夹中的 logs.txt 文件

                BOOL success = [logData writeToURL:documentsLogFileURL options:NSDataWritingAtomic error:&error];

                if (success) {

                    NSLog(@"Log file successfully written to Documents folder.");

                    // 上传后清空日志文件

                    [AppWallet clearLogFileAtURL:logFileURL];

                } else {

                    NSLog(@"Failed to write log file to Documents folder: %@", error.localizedDescription);

                }

            }

        }

    });

}

  

// 删除日志文件

+ (void)clearLogFileAtURL:(NSURL *)logFileURL {

    [[NSFileManager defaultManager] removeItemAtURL:logFileURL error:nil];

}


// plist新增key
Supports opening documents in place

Application supports iTunes file sharing

```







