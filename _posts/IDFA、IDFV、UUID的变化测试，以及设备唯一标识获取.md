---
title: IDFA、IDFV、UUID的变化测试，以及设备唯一标识获取
date: 2017-10-18
tags: [iOS,设备唯一标识]
categories: iOS
---

# 获取

## UUID
```
+ (NSString *)createUUID
{
    // Create universally unique identifier (object)
    CFUUIDRef uuidObject = CFUUIDCreate(kCFAllocatorDefault);
    
    // Get the string representation of CFUUID object.
    NSString *uuidStr = (NSString *)CFBridgingRelease(CFUUIDCreateString(kCFAllocatorDefault, uuidObject));
    
    // If needed, here is how to get a representation in bytes, returned as a structure
    // typedef struct {
    //   UInt8 byte0;
    //   UInt8 byte1;
    //   ...
    //   UInt8 byte15;
    // } CFUUIDBytes;
    //CFUUIDBytes bytes = CFUUIDGetUUIDBytes(uuidObject);
    
    CFRelease(uuidObject);
    
    return uuidStr;
}
```
## IDFA
```
+ (NSString *)getIDFAString
{
    NSString *adId = [[[ASIdentifierManager sharedManager] advertisingIdentifier] UUIDString];
    return adId;
}
```
## IDFV
```
+ (NSString *)getIDFVString
{
    NSString *idfv = [[[UIDevice currentDevice] identifierForVendor] UUIDString];
    return idfv;
}
```
# 测试

## iPhone 6s plus iOS9.0(模拟器)

第一次
```
idfa--------FA5A184C-933E-4E83-B5A2-55841F2011ED
idfv--------74594A83-1E41-4531-9A80-48BA72FB562F
uuid--------E91AEF82-5E5C-40F8-90D6-63B9ACB66CF7
keychains---E607AD64-4F21-4E0F-8D46-55E3CEDE91AA
```
第二次
```
idfa--------FA5A184C-933E-4E83-B5A2-55841F2011ED
idfv--------74594A83-1E41-4531-9A80-48BA72FB562F
uuid--------3AAC0C7F-5616-4063-A8AC-D65A5B9A1056
keychains---E607AD64-4F21-4E0F-8D46-55E3CEDE91AA
```

卸载重装
```
idfa--------FA5A184C-933E-4E83-B5A2-55841F2011ED
idfv--------7AB3F4C8-3973-4DA1-93F0-DE88FD7F235A
uuid--------24F753C2-0205-45CC-B416-BA679909C1E9
keychains---E607AD64-4F21-4E0F-8D46-55E3CEDE91AA
```


# ipad,iOS 10.2.1 （真机）


第一次
```
idfa--------FBF3BF74-1C10-4AC9-9AD8-F9D0FF0753CF
idfv--------64B1DFCF-951D-49F4-B4F4-CC5095316B5C
uuid--------F609B6A4-C1D1-4301-89E6-0E16B94EF170
keychains---1E0D87A5-0A1F-484E-9C98-8920B2E16F27
```
第二次
```
idfa--------FBF3BF74-1C10-4AC9-9AD8-F9D0FF0753CF
idfv--------64B1DFCF-951D-49F4-B4F4-CC5095316B5C
uuid--------BBAC0119-C11A-4C45-AA9F-799570DD028A
keychains---1E0D87A5-0A1F-484E-9C98-8920B2E16F27
```

卸载重装：
```
idfa--------FBF3BF74-1C10-4AC9-9AD8-F9D0FF0753CF
idfv--------64B1DFCF-951D-49F4-B4F4-CC5095316B5C
uuid--------E73401B0-CA3D-4969-96A0-9C435ED2BED5
keychains---1E0D87A5-0A1F-484E-9C98-8920B2E16F27
```


# iPhone 8 plus, iOS 11 (模拟器)

第一次
```
idfa--------0BA97921-8F58-41C9-BFD0-E920BD9F8B59
idfv--------7F7EE423-0BB3-4ABD-8304-F051B3B387BA
uuid--------D12DE2E5-3A54-4AF2-A809-77C46E73169E
keychains---ECD6366D-09F5-4349-A781-D67F4F3B6F35
```

第二次
```
idfa--------0BA97921-8F58-41C9-BFD0-E920BD9F8B59
idfv--------7F7EE423-0BB3-4ABD-8304-F051B3B387BA
uuid--------D3A6EC1F-D46B-4A37-AECB-6B59A6BA1B1D
keychains---ECD6366D-09F5-4349-A781-D67F4F3B6F35
```

卸载重装：
```
idfa--------0BA97921-8F58-41C9-BFD0-E920BD9F8B59
idfv--------DC04933D-65C1-4020-8583-18040F338F6F
uuid--------133D20C7-ED69-4ED9-BCBC-D0B38EF214DD
keychains---ECD6366D-09F5-4349-A781-D67F4F3B6F35
```


# iPad iOS11.0.3 （真机）

第一次
```
idfa--------DB08FC60-1CE6-4EC5-A20A-D8B909F62642
idfv--------B5F266E9-2BCA-46A2-B304-A2BB6C57EF55
uuid--------65C3AD4A-F9D5-40D4-BCE4-4E6184D68BC4
keychains---644B1FE5-A454-4ACE-AB82-E5B5C1F9127D
```


第二次
```
idfa--------DB08FC60-1CE6-4EC5-A20A-D8B909F62642
idfv--------B5F266E9-2BCA-46A2-B304-A2BB6C57EF55
uuid--------5149E9A5-1D65-4989-A6E8-149479F4225D
keychains---644B1FE5-A454-4ACE-AB82-E5B5C1F9127D
```

卸载重装
```
idfa--------DB08FC60-1CE6-4EC5-A20A-D8B909F62642
idfv--------FF76D818-6839-40EC-9C88-58D1CE2A8DC1
uuid--------8D892E51-07A1-4F8A-9076-C01A21B1800B
keychains---644B1FE5-A454-4ACE-AB82-E5B5C1F9127D
```


# 测试结果：

1，iOS10.2.1 系统下
`idfa、idfv、keychains在杀进程运行和卸载重装均不会改变；`

2，iOS9.0 、iOS11.0 系统下
`idfa、keychains在杀进程运行和卸载重装均不会改变,
idfv 卸载重装会改变；`

# 结论：

为了获取设备唯一ID

## 方案1:

可以先获取idfa，如果获取不到，就获取idfv。第一次获取到的值保存到钥匙串(keychains)

上代码
```
// 获取唯一标识
+(NSString *)getDeviceId{
    NSString * deviceId = [SFHFKeychainMTSDKTool getPasswordForUsername:DEVICEID andServiceName:DEVICEID error:nil];
    if(!deviceId){
        deviceId = [MTSDKTool getIDFAString];
        if (!deviceId) {
            deviceId = [MTSDKTool getIDFVString];
        }
        if([SFHFKeychainMTSDKTool storeUsername:DEVICEID andPassword:deviceId forServiceName:DEVICEID updateExisting:YES error:nil]){
            return deviceId;
        } else {
            return nil;
        }
    }
    return deviceId;
}
```

方案2:

获取uuid，第一次获取到的值保存到钥匙串(keychains)

```
+(NSString *)getDeviceId{
    NSString * deviceId = [SFHFKeychainMTSDKTool getPasswordForUsername:DEVICEID andServiceName:DEVICEID error:nil];
    if(!deviceId){
        deviceId = [MTSDKTool createUUID];
        if([SFHFKeychainMTSDKTool storeUsername:DEVICEID andPassword:deviceId forServiceName:DEVICEID updateExisting:YES error:nil]){
            return deviceId;
        } else {
            return nil;
        }
    }
    return deviceId;
}
```

# 定义 (延伸)

## UDID (Unique Device Identifier)

苹果IOS设备的唯一识别码，它由40个字符的字母和数字组成。在很多需要限制一台设备一个账号的应用中经常会用到。在iOS5中可以获取到设备的UDID。

**⚠️后来被苹果禁止了。**

## UUID（Universally Unique Identifier）

中文意思是通用唯一识别码。它是让分布式系统中的所有元素，都能有唯一的辨识资讯，而不需要透过中央控制端来做辨识资讯的指定。这样，每个人都可以建立不与其它人冲突的 UUID。在此情况下，就不需考虑数据库建立时的名称重复问题。苹果公司建议使用UUID为应用生成唯一标识字符串。

开发者可以在应用第一次启动时调用一 次，然后将该串存储起来，替代UDID来使用。

但是，如果用户删除该应用再次安装时，又会生成新的字符串，所以不能保证唯一识别该设备。使用UUID，就要考虑应用被删除后再重新安装时的处理。

一个解决的办法是：UUID一般只生成一次，保存在iOS系统里面，如果应用删除了，重装应用之后它的UUID还是一样的，除非系统重置 。但是不能保证在以后的系统升级后还能用（如果系统保存了该信息就能用）。

## MAC Address

用来表示互联网上每一个站点的标识符，采用十六进制数表示，共六个字节（48位）。其中，前三个字节是由IEEE的注册管理机构

 RA负责给不同厂家分配的代码(高位24位)，也称为“编制上唯一的标识符” （Organizationally Unique Identifier)，后三个字节(低位24位)由各厂家自行指派给生产的适配器接口，称为扩展标识符（唯一性）。

MAC地址在网络上用来区分设备的唯一性，接入网络的设备都有一个MAC地址，他们肯定都是不同的，是唯一的。一部iPhone上可能有多个MAC地址，包括WIFI的、SIM的等，但是iTouch和iPad上就有一个WIFI的，因此只需获取WIFI的MAC地址就好了，也就是en0的地址。

MAC地址就如同我们身份证上的身份证号码，具有全球唯一性。这样就可以非常好的标识设备唯一性，类似与苹果设备的UDID号，通常的用途有：1）用于一些统计与分析目的，利用用户的操作习惯和数据更好的规划产品；2）作为用户ID来唯一识别用户，可以用游客身份使用app又能在服务器端保存相应的信息，省去用户名、密码等注册过程。

使用Mac地址生成设备的唯一标识主要分三种：

1、直接使用“MAC Address” 

2、使用“MD5(MAC Address)”

3、使用“MD5(Mac Address+bundle_id)”获得“机器＋应用”的唯一标识（bundle_id 是应用的唯一标识）

在iOS7之后，如果请求Mac地址都会返回一个固定值。

## IDFA（identifierForIdentifier）

广告标示符，适用于对外：例如广告推广，换量等跨应用的用户追踪等。

是iOS 6中另外一个新的方法，提供了一个方法advertisingIdentifier，通过调用该方法会返回一个NSUUID实例，最后可以获得一个UUID，由系统存储着的。不过即使这是由系统存储的，但是有几种情况下，会重新生成广告标示符。如果用户完全重置系统（(设置程序 -> 通用 -> 还原 -> 还原位置与隐私) ，这个广告标示符会重新生成。另外如果用户明确的还原广告(设置程序-> 通用 -> 关于本机 -> 广告 -> 还原广告标示符) ，那么广告标示符也会重新生成。关于广告标示符的还原，有一点需要注意：如果程序在后台运行，此时用户“还原广告标示符”，然后再回到程序中，此时获取广 告标示符并不会立即获得还原后的标示符。必须要终止程序，然后再重新启动程序，才能获得还原后的广告标示符。

在同一个设备上的所有App都会取到相同的值，是苹果专门给各广告提供商用来追踪用户而设的，用户可以在 设置|隐私|广告追踪 里重置此id的值，或限制此id的使用，故此id有可能会取不到值，但好在Apple默认是允许追踪的，而且一般用户都不知道有这么个设置，所以基本上用来监测推广效果，是戳戳有余了。

注意⚠️：由于idfa会出现取不到的情况，故绝不可以作为业务分析的主id，来识别用户。
 
## IDFV（identifierForVendor）

Vindor标示符，适用于对内：例如分析用户在应用内的行为等。

是给Vendor标识用户用的，每个设备在所属同一个Vender的应用里，都有相同的值。其中的Vender是指应用提供商，但准确点说，是通过BundleID的DNS反转的前两部分进行匹配，如果相同就是同一个Vender，例如对于com.somecompany.appone,com.somecompany.apptwo

 这两个BundleID来说，就属于同一个Vender，共享同一个idfv的值。和idfa不同的是，idfv的值是一定能取到的，所以非常适合于作为内部用户行为分析的主id，来标识用户，替代OpenUDID。

注意⚠️：如果用户将属于此Vender的所有App卸载，则idfv的值会被重置，即再重装此Vender的App，idfv的值和之前不同。

# 参考：

[iOS获取设备唯一标识的各种方法？IDFA、IDFV、UDID分别是什么含义？](http://www.cnblogs.com/zxykit/p/5320259.html)