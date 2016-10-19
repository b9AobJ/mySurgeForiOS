# mySurgeForiOS
from other people has 3900 rules fail wall

# Untitled Note

目 录<!--more-->

[1简介和直播云............................................................................................................ 3](#_Toc24034)

[1.1概述...................................................................................................................... 3](#_Toc10601)

[1.2阅读对象............................................................................................................... 3](#_Toc7750)

[2 SDK说明.................................................................................................................... 4](#_Toc4360)

[2.1系统功能............................................................................................................... 4](#_Toc32165)

[2.2推流介绍............................................................................................................... 4](#_Toc32337)

[3 使用方法................................................................................................................... 5](#_Toc10541)

[3.1 下载SDK............................................................................................................... 5](#_Toc24746)

[3.2 导入静态库.......................................................................................................... 5](#_Toc5620)

[3.3 依赖库说明.......................................................................................................... 5](#_Toc5896)

[3.4 iOS9中ATS配置.................................................................................................. 6](#_Toc21605)

[3.5 iOS10中麦克风、摄像头权限获取..................................................................... 6](#_Toc12336)

[4 快速集成................................................................................................................... 8](#_Toc8214)

[4.1 设置CGIKey，定义推流地址和播放地址............................................................ 8](#_Toc18880)

[4.2 导入头文件......................................................................................................... 8](#_Toc5921)

[4.3 启动推流及状态回调处理................................................................................... 8](#_Toc27793)

[4.4 关闭采集推流................................................................................................... 10](#_Toc7546)

[5 播放器接入............................................................................................................. 11](#_Toc31039)

[5.1 静态库引入....................................................................................................... 11](#_Toc21474)

[5.2 集成播放器....................................................................................................... 11](#_Toc3540)

[6 使用进阶................................................................................................................. 13](#_Toc1881)

[7 API介绍.................................................................................................................. 14](#_Toc21996)

[7.1参数配置............................................................................................................. 14](#_Toc25920)

[7.2 推流控制............................................................................................................ 15](#_Toc200)

[7.3 信息回调............................................................................................................ 16](#_Toc24982)

[7.4 枚举................................................................................................................... 17](#_Toc13610)

[8 SDK升级历史信息文档变更................................................................................. 19](#_Toc26599)

[9 反馈和建议............................................................................................................. 21](#_Toc22773)

** **

 **
 ** 

<><>[1]()简介和直播云

<>[1.1]()概述

UCloud云计算（上海优刻得信息科技有限公司）是国内技术与服务最为顶尖的基础云服务商，公司专注于基础云计算的产品研发与运营，是上海市云计算基地重点企业，国家工信部首批认证通过的“可信云计算企业”。

我们围绕用户的需求持续创新，通过整合优秀的合作伙伴资源，深耕互联网领域，打造全天候90秒内快速响应的服务体系，在国内云计算领域构筑了独树一帜的竞争优势。

UCloud云计算平台已经为游戏、移动互联网、大数据、电子商务、Saas等多个领域提供IT基础架构支撑，得益于业内领先的云计算技术和技术团队的专业经验，UCloud已成功为国内外上万家企业用户提供服务，大幅降低了用户使用IT基础设施的成本及技术门槛。

UCloud直播云服务（简称“直播云”）基于UCloud UCDN和多媒体技术，为广大开发者提供媒体相关的整体解决方案。

直播云通过提供一系列API及跨终端平台SDK，实现包括媒体存储、编码、转码、内容保护、点播、直播、音视频会议、分析、广告等诸项功能。

媒体应用具有技术专业性强、计算及存储资源门槛高的特点；而通过使用直播云服务，开发者就可轻松利用UCloud技术及平台资源同时，专注于自己的业务，灵活、快捷地构建各种形式的媒体应用。

<>[1.2]()阅读对象

本文档面向所有使用该 SDK 的开发人员、测试人员、合作伙伴以及对此感兴趣的其他用户，要求读者具有一定的 iOS 编程经验。

<>[2 SDK]()说明

<>[2.1]()系统功能

iOS版本

支持iOS 7.0及以上系统

指令集支持

armv7、arm64、i386、 x86\_64

** **

** **

** **

<>[2.2]()推流介绍

参数设置

可以根据需要自定义视频分辨率，帧率、比特率

编码方式

音频AAC硬编码、视频H264硬编码

<>[3 ]()使用方法

<>[3.1 ]()下载SDK

** **

 下载最新版本的iOS直播云SDK:[https://docs.ucloud.cn/video/ulive/ulive\_ios\_sdk](https://docs.ucloud.cn/video/ulive/ulive_ios_sdk)

** **

<>[3.2 ]()导入静态库

将lib文件夹下的Recorder直接拉到Xcode的工程， 

![](file://localhost/Users/Sidney/Library/Group%20Containers/UBF8T346G9.Office/msoclip1/01/clip_image004.gif)

选中**copy items if needed**，选择**Create groups**，选中相关**target**，点击**Finish**；

\*Recorder文件夹中相关文件意义:

CameraServer.h

直播推流类，包含视频数据采集和音频数据相关采集，数据推流服务器操作等；

UCloudRecorderTypeDef.h

直播推流所需常量及配置信息

<>[libUCloudMediaRecorder.a]()

直播推流静态库

NSString+UCloudCameraCode.h

直播状态返回码

FilterManager.h/FilterManager.m

滤镜管理器

Filter文件夹

所有滤镜库，包含美颜滤镜

<>[3.3 ]()依赖库说明 

 添加libUCloudMediaRecorder.a所需引用的系统 framework,如下: 

VideoToolbox.framework

CoreMedia.framework

AVFoundation.framework

AudioToolbox.framework

 libz.thd、 libc++.tbd

如图所示：

![](file://localhost/Users/Sidney/Library/Group%20Containers/UBF8T346G9.Office/msoclip1/01/clip_image006.gif)

[3.]()4 iOS9中ATS配置

由于iOS9引入了AppTransportSecurity(ATS)特性，要求App访问的网络使用HTTPS协议，如果不做特殊设置，http请求会失败，所以需要开发者在工程中增加设置以便可以发送http请求，如下：

在info plist中增加字段：

\< key\>NSAppTransportSecurity\< /key\>

\< dict\>

 \< key\>NSAllowsArbitraryLoads\< /key\>

 \< true/\>

\< /dict\>

配置完后如图所示

![](file://localhost/Users/Sidney/Library/Group%20Containers/UBF8T346G9.Office/msoclip1/01/clip_image008.gif)

[3.]()5 iOS10中麦克风、摄像头权限获取

由于iOS10要求App使用麦克风、摄像头时，需要对相应的设备获得权限，如下：

在info plist中增加字段：

\<key\>NSCameraUsageDescription\</key\>

\<string\>允许此权限才能使用相机功能\</string\>

\<key\>NSMicrophoneUsageDescription\</key\>

\<string\>允许此权限才能录音\</string\>

配置完后如图所示

![](file://localhost/Users/Sidney/Library/Group%20Containers/UBF8T346G9.Office/msoclip1/01/clip_image010.gif)

[4 ]()快速集成

[4]().1 设置CGIKey，定义推流地址和播放地址

//demo中的推流地址仅供demo测试使用，如需更换推流域名地址，请联系客服或者客户经理索取对应的CGIKey

\#define CGIKey @"publish3-key"

//推流地址

\#define RecordDomain(id) [NSString stringWithFormat:@"rtmp://publish3.cdn.ucloud.com.cn/ucloud/%@", id]; 

//播放地址，支持http-flv、RTMP、hls播放

\#define PlayDomain(id) [NSString stringWithFormat:@"http://vlive3.rtmp.cdn.ucloud.com.cn/ucloud/%@.flv", id];

\#define PlayDomain(id) [NSString stringWithFormat:@"rtmp://vlive3.rtmp.cdn.ucloud.com.cn/ucloud/%@", id];

\#define PlayDomain(id) [NSString stringWithFormat:@"http://vlive3.hls.cdn.ucloud.com.cn/ucloud/%@/playlist.m3u8", id];

[4]().2 导入头文件

\#import "CameraServer.h"

\#import "FilterManager.h"

\#import "NSString+UCloudCameraCode.h"

[4]().3 启动推流及状态回调处理

//配置SDK推流鉴权Key

[[CameraServer server] setSecretKey:CGIKey];

//配置推流地址、美颜滤镜

[[CameraServer server] configureCameraWithOutputUrl:path filter:originalFilters messageCallBack:^(UCloudCameraCode code, NSInteger arg1, NSInteger arg2, id data) {

 [weakSelf handlerMessageCallBackWithCode:code arg1:arg1 arg2:arg2 data:data weakSelf:weakSelf];

} deviceBlock:^(AVCaptureDevice \*dev) {

[self handlerDeviceBlock:dev weakSelf:weakSelf];

} cameraData:^CMSampleBufferRef(CMSampleBufferRef buffer) {

 //如果不需要裸流，不建议在这里执行操作，将增加额外的功耗

 return nil;

}];

//推流端回调信息处理

- (void)handlerMessageCallBackWithCode:(UCloudCameraCode)code arg1:(NSInteger)arg1 arg2:(NSInteger)arg2 data:(id)data weakSelf:(ViewController \*)weakSelf

{ 

 if (code == UCloudCamera\_Permission)

 {

 UIAlertView \*alterView = [[UIAlertView alloc] initWithTitle:@"相机授权" message:@"没有权限访问您的相机，请在“设置－隐私－相机”中允许使用" delegate:nil cancelButtonTitle:@"取消" otherButtonTitles:nil, nil];

 [alterView show];

 }

 else if (code == UCloudCamera\_Micphone)

 {

 [[[UIAlertView alloc] initWithTitle:@"麦克风授权" message:@"没有权限访问您的麦克风，请在“设置－隐私－麦克风”中允许使用" delegate:nil cancelButtonTitle:@"取消" otherButtonTitles:nil, nil] show];

 }

 else if (code == UCloudCamera\_SecretkeyNil)

 {

 UIAlertView \*alert = [[UIAlertView alloc] initWithTitle:@"Warning" message:@"密钥为空" delegate:self cancelButtonTitle:@"OK" otherButtonTitles:nil, nil];

 [alert show];

 [weakSelf setBtnStateInSel:1];

 }

 else if (code == UCloudCamera\_AuthFail)

 {

 NSDictionary \*dic = data;

 NSError \*error = dic[@"error"];

 NSLog(@"errcode:%@\\n msg:%@\\n errdesc:%@", dic[@"retcode"], dic[@"message"], error.description);

 }

 else if (code == UCloudCamera\_PreviewOK)

{

  //摄像头准备完成，开启预览

 [self.videoView removeFromSuperview];

 self.videoView = nil;

 [weakSelf startPreview];

 }

 else if (code == UCloudCamera\_PublishOk)

 {

 [ //]()发布操作准备完成，详细代码可以参照sdk使用demo

 }

 else if (code == UCloudCamera\_StartPublish)

 {

 // 开始发布，详细代码可以参照sdk使用demo

 }

 else if (code == UCloudCamera\_OUTPUT\_ERROR)

 {

  // 推流出错，详细代码可以参照sdk使用demo

 }

 else if (code == UCloudCamera\_BUFFER\_OVERFLOW)

 {

 //当前上传网速不给力，详细代码可以参照sdk使用demo

 }

}

- (void)handlerDeviceBlock:(AVCaptureDevice \*)dev weakSelf:(UIViewController \*)weakSelf

{

}

//开启推流预览

- (void) startPreview

{

 UIView \*cameraView = [[CameraServer server] getCameraView];

 cameraView.backgroundColor = [UIColor whiteColor];

 [self.view addSubview:cameraView];

 [self.view sendSubviewToBack:cameraView];

 self.videoView = cameraView;

}

[4]().4 关闭采集推流

[[CameraServer server] shutdown:^{

 if (weakSelf.videoView)

 {

 [weakSelf.videoView removeFromSuperview];

 }

 weakSelf.videoView = nil;

}];

[5 ]()播放器接入

[5.1 ]()静态库引入

 播放器包含ffmpeg库，已知在含有ffmepg的第三方库情况下无法正常运行,可以尝试在编译选项Other linker Flags中加入-force\_load来解决冲突，但不推荐使用。Player文件夹放置的是直播云播放器库，（如果已经有播放器库，可以不添加，自行配置播放器）将Player直接拉进Xcode工程目录中

![](file://localhost/Users/Sidney/Library/Group%20Containers/UBF8T346G9.Office/msoclip1/01/clip_image011.gif)

选中**copy items if needed**，选择**Create groups**，选中相关**target**，点击**Finish**；

[\*]()Player文件夹中相关文件意义:

UCloudMediaPlayer.h

播放器控制类

UCloudMediaPlayback.h

播放器通知类

libUCloudMediaPlayer.a

播放器静态库

UCloudPlayback.h

播放器播放类

UCloudMediaModule.h

播放器显示控制类

\*引入**PlayerUI**，**PlayerUI**是项目中的播放器UI及其管理器类，用户可以自行修改使用。

[5.2 ]()集成播放器

引入头文件

\#import "UCloudMediaPlayer.h"

\#import "UCloudMediaViewController.h"

\#import "PlayerManager.h"

开始播放直播流

self.playerManager = [[PlayerManager alloc] init];

self.playerManager.view = self.view;

self.playerManager.viewContorller = self;

[self.playerManager setPortraitViewHeight: self.view.frame.size.height];

[self.playerManager buildMediaPlayer:self.pathTextField.text];

关闭播放器

[self.playerManager.mediaPlayer.player.view removeFromSuperview];

[self.playerManager.controlVC.view removeFromSuperview];

[self.playerManager.mediaPlayer.player shutdown];

self.playerManager.mediaPlayer = nil;

[6 ]()使用进阶

当你要深入理解 SDK 的一些参数及有定制化需求时，可以从高级功能部分中查询阅读。

width、height;

默认为竖屏方式设置，宽高为360\*640，视频宽高比按照9：16进行设置

fps

帧率，即每一秒所包含的视频帧数，默认15，有效范围[1~30], 超出会提示参数错误;

bitrate

音频和视频总比特率，默认UCloudVideoBitrateMedium = 800，音频码率为128kps,可自行设置，该属性的单位为kbps(kilo bits per second)，视频码率高则画面较清晰，低则画面较模糊，同时数据亦是如此，码率高数据大，码率低数据小；

captureDevicePos

摄像头位置，默认打开前置摄像头；

muted

是否开启静音，默认NO

videoOrientation

视频推流方向，只在采集初始化时设置有效，默认UIDeviceOrientationPortrait；

reconnectInterval

重推流间隔,默认5秒

reconnectCount

重推流次数，默认3次，如果需要不做重推操作，可将此参数设置为0

重推流间隔和次数可根据app场景自行进行设置调整；

视频滤镜渲染

我们提供了两种不同美颜滤镜算法（UCloudGPUImageBeautyFilter和UCloudGPUImageBeautyFilter2）及各种基于GPUImageView的滤镜，用户可以根据自行情况进行选择使用，或者自行编写基于GPUImage的算法；

<>[7 API]()介绍

<>[7]().1参数配置

/\*!

 @property width

 @abstract 视频宽，默认360

 \*/

@property (assign, nonatomic) int width;

/\*!

 @property height

 @abstract 视频高，默认640

 \*/

@property (assign, nonatomic) int height;

/\*!

 @property fps

 @abstract 帧率(15\\20\\25\\30)，默认15

 @discussion video frame per seconds 有效范围[1~30], 超出会提示参数错误

 \*/

@property (assign, nonatomic) int fps;

/\*!

 @property bitrate

 @abstract 音频和视频总比特率UCloudVideoBitrate

 @discussion 默认UCloudVideoBitrateMedium，可自行设置，该属性的单位为kbps(kilo bits per seccond)

 @discussion 视频码率高则画面较清晰，低则画面较模糊，同时数据亦是如此，码率高数据大，码率低数据小

 \*/

@property (assign, nonatomic) int bitrate;

/\*!

 @property captureDevicePos

 @abstract 摄像头位置，默认打开前置摄像头

 \*/

@property (assign, nonatomic) AVCaptureDevicePosition captureDevicePos;

/\*!

 @property muted

 @abstract 是否静音，默认NO

 \*/

@property (nonatomic, assign) BOOL muted;

/\*!

 @property videoOrientation

 @abstract 视频推流方向

 @discussion 只在采集初始化时设置有效，默认UIDeviceOrientationPortrait

 \*/

@property (nonatomic, assign) UCloudVideoOrientation videoOrientation;

/\*!

 @property reconnectInterval

 @abstract 重推流间隔,默认5秒

 \*/

@property (nonatomic, assign) NSTimeInterval reconnectInterval;

/\*!

 @property reconnectCount

 @abstract 重推流次数，默认3次

 @discussion 如果需要不做重推操作，可将此参数设置为0

 \*/

@property (nonatomic, assign) NSInteger reconnectCount;

<>[7]().2 推流控制

/\*!

 @method cameraPrepare

 @abstract 打开摄像头预览，不进行推流上传

 \*/

- (void)cameraPrepare;

/\*!

 @method cameraStart

 @abstract 开始录像采集推流上传

 @return 返回操作结果

 \*/

- (BOOL)cameraStart;

/\*!

 @method cameraRestart

 @abstract 推流失败之后重新推流

 \*/

- (void)cameraRestart;

/\*!

 @method shutdown

 @abstract 关闭录像停止推流

 @param completion 关闭成功回调函数

 \*/

- (void)shutdown:(void(^)(void))completion;

/\*!

 @method getCameraView

 @abstract 获取采集图像

 @return 采集图像视图

 \*/

- (UIView\*)getCameraView;

/\*!

 @method initializeCameraViewFrame:

 @abstract 设置采集图像显示的frame

 @param frame 显示图像的大小

 @discussion 如果需要设置显示图像的frame，iOS8以下请在此先设置，直接使用getCameraView方法获取view进行设置是无作用的，iOS8以上两者都可设置frame

 \*/

- (void)initializeCameraViewFrame:(CGRect)frame;

/\*!

 @method changeCamera

 @abstract 切换摄像头

 \*/

- (void)changeCamera;

/\*!

 @method outBitrate

 @abstract 编码后的实际码率

 @return 码率值，包括视频码率和音频码率

 \*/

- (NSString \*)outBitrate;

/\*!

 @method setTorchState:

 @abstract 设置手电筒状态

 @param state 状态

 @return 设置是否成功

 \*/

- (BOOL)setTorchState:(UCloudCameraState)state;

/\*!

 @method currentCapturePosition

 @abstract 获取当前摄像头的位置

 @return 摄像头位置

 \*/

- (AVCaptureDevicePosition)currentCapturePosition;

/\*!

 @method addFilters:

 @abstract 添加滤镜组

 @param filters 滤镜数组

 \*/

- (void)addFilters:(NSArray \*)filters;

/\*!

 @method openFilter

 @abstract 打开美颜功能

 \*/

- (void)openFilter;

/\*!

 @method closeFilter

 @abstract 关闭美颜功能

 \*/

- (void)closeFilter;

<>[7]().3 信息回调  

/\*!

 @abstract 推流状态回调

 \*/

typedef void(^CameraMessage)(UCloudCameraCode code, NSInteger arg1, NSInteger arg2, id data);

/// 相机回调

typedef void(^CameraDevice)(AVCaptureDevice \*dev);

typedef CMSampleBufferRef (^CameraData)(CMSampleBufferRef buffer);

<>[7]().4 枚举 

typedef NS\_ENUM(NSInteger, UCloudCameraCode)

{

 UCloudCamera\_COMPLETED =0,

 UCloudCamera\_FILE\_SIZE = 1,

 UCloudCamera\_FILE\_DURATION = 2,

 UCloudCamera\_CUR\_POS = 3,

 UCloudCamera\_CUR\_TIME = 4,

 UCloudCamera\_URL\_ERROR = 5,

 UCloudCamera\_OUT\_FAIL = 6,

 /// 推流开始

 UCloudCamera\_STARTED = 7,

 UCloudCamera\_READ\_AUD\_ERROR = 8,

 UCloudCamera\_READ\_VID\_ERROR = 9,

 /// 推流错误

 UCloudCamera\_OUTPUT\_ERROR = 10,

 /// 推流停止

 UCloudCamera\_STOPPED = 11,

 UCloudCamera\_READ\_AUD\_EOS = 12,

 UCloudCamera\_READ\_VID\_EOS = 13,

 /// 推流带宽

 UCloudCamera\_BUFFER\_OVERFLOW = 14,

 /// SDK 密钥为空

 UCloudCamera\_SecretkeyNil = 15,

 /// 推流域名为空

 UCloudCamera\_DomainNil = 16,

 /// SDK 鉴权失败

 UCloudCamera\_AuthFail = 17,

 /// SDK 鉴权返回IP列表为空

 UCloudCamera\_ServerIpError = 18,

 /// 预览视图准备好

 UCloudCamera\_PreviewOK = 19,

 /// 底层推流配置完毕

 UCloudCamera\_PublishOk = 20,

 UCloudCamera\_StartPublish = 21,

 /// SDK dig错误

 UCloudCamera\_DigError = 22,

 /// 推流ID已被占用

 UCloudCamera\_AlreadyPublish = 23,

 /// 推流url对应的服务器连接失败

 UCloudCamera\_CannotConnect = 24,

 /// 摄像头权限

 UCloudCamera\_Permission = 998,

 /// 麦克风权限

 UCloudCamera\_Micphone = 999,

};

typedef NS\_ENUM(NSInteger, UCloudCameraState)

{

 /// 关闭

 UCloudCameraCode\_Off,

 /// 打开

 UCloudCameraCode\_On,

 /// 自动

 UCloudCameraCode\_Auto,

};

/\*\*

 \* @abstract 视频采集方向

 \*/

typedef NS\_ENUM(NSInteger, UCloudVideoOrientation) {

 UCloudVideoOrientationPortrait = UIDeviceOrientationPortrait,

 UCloudVideoOrientationPortraitUpsideDown = UIDeviceOrientationPortraitUpsideDown,

 UCloudVideoOrientationLandscapeRight = UIDeviceOrientationLandscapeRight,

 UCloudVideoOrientationLandscapeLeft = UIDeviceOrientationLandscapeLeft

};

/\*!

 @enum UCloudVideoBitrate

 @abstract 采集的视频流码率，包括视频流码率和音频流码率，音频流码率默认128kbps

 \*/

typedef NS\_ENUM(NSInteger, UCloudVideoBitrate) {

 UCloudVideoBitrateLow = 400,

 UCloudVideoBitrateNormal = 600,

 UCloudVideoBitrateMedium = 800,

 UCloudVideoBitrateHigh = 1000

};

<>[8 ]()SDK升级历史信息文档变更

**版本号**

**发布日期**

**说**** ****明**

1.4.0

2016.9.8

1、推流时加入声音降噪处理

2、播放器端优化hls播放流畅度

1.3.9

2016.8.29

提前摄像头UCloudCamera\_PreviewOK消息通知；调整推出去的流为预览时的垂直翻转；sdk&demo增加对通知栏下拉操作的处理

1.3.8

2016.8.24

拆分CameraServer.h文件为CameraServer.h&UCloudRecorderTypeDef.h

1.3.7

2016.8.18

调整demo重推、重播逻辑；修复demo中filterValues数组在ios7下的问题

1.3.6

2016.7.29

更新播放器库(libUCloudMediaPlayer.a)，库主要优化弱网下音频的播放体验

1.3.5

2016.7.25

增加重推和重播功能

1.3.4

2016.7.19

优化推流端在ios9.2上的内存占用；更新播放器库，优化弱网下声音的播放问题

1.3.3

2016.7.12

调整采集时摄像头的显示模式，适配所有设备上能全屏显示无黑边；增加横竖屏推流模式

1.3.2

2016.6.30

CameraServer.h 增加UCloudCameraCode 23（推流ID已被占用）、24（推流url无法连接）；播放器增加直播追赶策略

1.3.1

2016.6.23

优化推流时打开摄像头的流程；增加直播推流的模拟器库版本

1.3.0

2016.6.16

修改CameraServer.h bitrate属性值的含义，抛弃以前的计算方式，改为总的音视频码率，单位为kbps，默认800kbps，详细可见ViewController.m 235行；新增支持直播过程中调整码率设置；新增UCloudGPUImageBeautyFilter2美颜滤镜，增加人脸边缘检测算法，磨皮效果更自然，提供磨皮、亮度、饱和度三种参数设置，可以在直播过程中动态调整美颜效果

1.2.9

2016.6.7

修复iphone6s推流有噪音的问题，增加推流时静音功能、手电筒功能，调整按钮布局、按钮文字描述

1.2.8

2016.5.19

增加美颜滤镜开关，showMediaPlayer方法增加了urltype参数

1.2.7

2016.5.4

sdk内部增加对摄像头麦克风权限的获取校验，处理特定场景下播放与推流渲染的问题，优化对蓝牙设备、耳机、扬声器的切换处理

1.2.6

2016.4.26

推流界面增加更多推流信息，优化推流时前台后台切换的问题

1.2.5

2016.4.21

修改推流界面，增加debug信息

1.2.1

2016.3.11

优化推流稳定性、优化demo体验、优化demo的滤镜效果预览流畅度、实时性

1.1.1

2016.1.20

加入滤镜功能

1.0.0

2015.12.30

文档初稿，基础推流功能，自定义宽高、帧率、比特率

<>[9 ]()反馈和建议

  对于使用中发现的问题和建议进行反馈,我们的技术人员会同您联系。如果遇到SDK方面的问题，[可以发邮件给我们sdk\_spt@ucloud.cn](mailto:可以发邮件给我们sdk_spt@ucloud.cn)。

说 明

设备型号

iphone7

系统版本

iOS 10

SDK版本

v1.4.0

问题描述

描述问题现象

操作路径

经过了什么样的操作出现所述的问题

附 件

文本形式控制台log、crash报告、其他辅助信息（推流界面截屏或其他）

（问题反馈模板）