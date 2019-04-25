# 在线教育
随着互联网技术的发展，在线教育行业呈现出全新的商机和市场机遇，在线教育利用互联网实时音视频技术，将老师与学生通过网络连接到一个虚拟教室中授课，使用方便快捷，不受地域限制，随时随地上课，解决了传统教育中教育资源分配不均、通勤成本高等问题。

常见的几种在线教育场景及特点：
> 1V1教学：老师与学生1对1在线连麦专属辅导，低延迟强互动，专属服务提分效果明显。

> 互动小班课: 1个老师与几个学生在线上课，充分利用教师资源的同时保障低延迟强互动的良好体验。

> 千人大班课: 老师开课，学生通过手机或PAD端观看，同时可以举手与老师互动，满足海量并发场景。

## 典型场景
老师端通过PC客户端创建课程并开始上课，学生端通过手机或PAD端进入课堂，与老师进行连线互动，老师与学生能互相看到对方视频，老师端可以共享桌面课件进行教学，同时可以通过在线白班互动，整个授课过程可以录制成视频文件进行点播回看。

# DEMO体验
1. 学生端下载：
   * 安卓端 http://pgyer.com/3T_Class_Android
   * iOS端 https://itunes.apple.com/cn/app/3t-class/id1404763415?mt=8
2. 老师端下载：
   * Windows端 http://ftp.3ttech.cn/3tclass.exe

# 实现步骤

#### 准备工作
1. 在三体云官网SDK下载页 [http://3ttech.cn/index.php?menu=53]() 下载对应平台的 视频通话SDK。
2. 登录三体云官网 [http://dashboard.3ttech.cn/index/login]() 注册应用账号，进入控制台新建自己的应用并获取APPID。

#### SDK集成
##### 初始化及频道相关
1. 初始化SDK。
- TTTRtcEngine_Initialize
2. 设置参数（加入频道前调用）。
- TTTRtcEngine_SetAppID - 设置AppID
- TTTRtcEngine_SetChannelProfile - 设置频道模式（直播模式或者通信模式）
- TTTRtcEngine_SetClientRole - 设置本地用户的频道角色（主播或者副播）
- TTTRtcEngine_SetServerAddr - 设置服务器地址
- TTTRtcEngine_ConfigPublisher - 设置CDN推流地址
3. 加入频道
- TTTRtcEngine_JoinChannel - 加入成功后会收到onJoinChannel回调
4. 离开频道
- TTTRtcEngine_LeaveChannel - 调用后会收到onLeaveChannel回调
5. 释放SDK
- TTTRtcEngine_Release
##### 视频功能
1. 获取本地视频设备信息
- TTTRtc_VDeviceGetCount - 获取本地视频设备数量
- TTTRtc_VDeviceGetInfo - 获取本地视频设备信息
2. 打开/关闭本地视频功能（打开视频功能才能有效调用其它的视频相关接口）
- TTTRtcEngine_EnableVideo
- TTTRtcEngine_DisableVideo
3. 开始/停止检测本地视频设备
- TTTRtcEngine_StartLocalVideoTest
- TTTRtcEngine_StopLocalVideoTest
4. 创建/释放本地视频（创建后不会显示在画布上）
- TTTRtcEngine_CreateLocalVideo
- TTTRtcEngine_EnableVideoMixer - 主动或者被动开启上传本地视频流
- TTTRtcEngine_ReleaseLocalVideo
5. 开始/停止预览本地视频（开始后显示在画布上）
- TTTRtcEngine_StartPreview
- TTTRtcEngine_StopPreview
6. 修改本地视频设置
- TTTRtcEngine_ReconfigLocalVideo
7. 创建/释放远端视频（创建后直接显示在画布上）
- TTTRtcEngine_CreateRemoteVideo
- TTTRtcEngine_ReleaseRemoteVideo
8. 创建/释放混屏视频（创建后直接显示在画布上）
- TTTRtcEngine_CreateMixerVideo
- TTTRtcEngine_ReleaseMixerVideo
9. 注册/反注册监控视频（注册后，在onCaptureVideoFrame回调中收到本地视频的视频截图）
- TTTRtcEngine_RegisterVideoFrameObserver
- TTTRtcEngine_UnregisterVideoFrameObserver
10. 设置混屏
- TTTRtcEngine_SetVideoMixerBackgroundImgUrl - 设置混屏背景
- TTTRtcEngine_AddVideoMixer - 增加参与混屏的用户视频，需要在设置SEI前调用
- TTTRtcEngine_SetVideoCompositingLayoutJson - 设置混屏SEI（Json格式）
- TTTRtcEngine_DelVideoMixer - 删除参与混屏的用户视频，需要在设置SEI后调用
11. 开始/停止本地屏幕录制
- TTTRtcEngine_StartPushScreenCaptureRect
- TTTRtcEngine_StopPushScreenCapture
##### 音频输出功能
1. 获取本地音频输出设备信息
- TTTRtcEngine_GetNumOfPlayoutDevices - 获取本地音频输出设备的数量
- TTTRtcEngine_GetPlayoutDeviceName - 获取指定的本地音频输出设备的名称
2. 设置本地音频输出设备信息
- TTTRtcEngine_setPlayDevice - 设置需要使用的本地音频输出设备
- TTTRtcEngine_setSpeakerphoneVolume - 设置本地音频输出设备的音量
- TTTRtcEngine_EnableAudioVolumeIndication - 音量回调开关，打开后会收到onAudioVolumeIndication回调
3. 开始/停止测试本地音频输出设备
- TTTRtcEngine_startPlaybackDeviceTest
- TTTRtcEngine_stopPlaybackDeviceTest
4. 本地音频暂停/恢复
- TTTRtcEngine_pauseAudio
- TTTRtcEngine_resumeAudio
5. 本地视频高质量开关
- TTTRtcEngine_setHighQualityAudioParameters
##### 音频输入功能
1. 获取本地音频输入设备信息
- TTTRtcEngine_GetNumOfRecordingDevices - 获取本地音频输入设备的数量
- TTTRtcEngine_GetRecordingDeviceName - 获取指定的本地音频输入设备的名称
2. 设置本地音频输入设备信息
- TTTRtcEngine_SetRecordDevice - 设置需要使用的本地音频输入设备
- TTTRtcEngine_SetRecordVolume - 设置本地音频输入设备的音量
3. 开始/停止测试本地音频输入设备
- TTTRtcEngine_startRecordingDeviceTest
- TTTRtcEngine_stopRecordingDeviceTest
##### 静音功能
1. 本地音频静音开关
- TTTRtcEngine_MuteLocalAudioStream
2. 远端音频静音开关
- TTTRtcEngine_muteRemoteAudioStream
##### 回调
1. TTTRtcEngineCallback - 调用TTTRtcEngine_Initialize时注册的回调
- onJoinChannel - 加入频道成功
- onLeaveChannel - 离开频道
- onUserJoined - 远端用户进入频道
- onUserOffline - 远端用户离开频道
- onUserEnableVideo - 远端用创建/释放视频
- onMixerVideoCreate - 创建混屏视频
- onAudioVolumeIndication - 本地音频输入设备音量回调
- onConnectionLost本地SDK - 与服务器断开彻底连接，不再重连
2. TTTRtcVideoObserver - 调用TTTRtcEngine_RegisterVideoFrameObserver时注册的回调
- onCaptureVideoFrame - 获得指定的本地视频的截图


#### iOS-SDK集成
##### 初始化及频道相关
1. 初始化SDK,加载资源.
- sharedEngineWithAppId:delegate:
2. 设置参数（加入频道前调用）.
- setServerIp:port: - 设置服务器地址
- setBeautyFaceStatus:beautyLevel:brightLevel: - 设置美颜效果
- setChannelProfile: - 设置频道模式（直播模式或者通信模式）
- setClientRole - 设置角色
- enableVideo - 开启视频模式
- enableAudioVolumeIndication:smooth: - 启用说话者音量提示
- setVideoProfile:swapWidthAndHeight: - 设置视频编码属性(分辨率、宽高转换)
- enableVideoMixer - 是否使用混频
3. 加入频道
- joinChannelByKey:channelName:uid:joinSuccess: - 加入成功后会收到didJoinChannel:回调
4. 离开频道
- leaveChannel:nil - 调用后会收到didLeaveChannelWithStats:回调

##### 视频相关
1. 开启/停止本地视频预览.
- startPreview 
- stopPreview
2. 设置本地视频帧采集格式.
- setLocalVideoFrameCaptureFormat:
3. 禁用/启用本地视频功能.
- enableLocalVideo:
4. 设置本地视频显示.
- setupLocalVideo:
5. 允许/禁止播放指定的远端视频流.
- muteRemoteVideoStream:mute:

##### 音频相关
1. 禁用/启用本地音频功能.
- muteLocalAudioStream:
2. 静音指定远端用户/对指定远端用户取消静音.
- muteRemoteAudioStream:mute:

##### 回调相关
1. 自己进入频道成功的回调.
- rtcEngine:didJoinChannel:withUid:elapsed:
2. 自己进入频道失败的回调.
- rtcEngine:didOccurError:
3. 自己成功离开频道的回调.
- rtcEngine:didLeaveChannelWithStats:
4. 其他用户进入频道成功的回调.
- rtcEngine:didJoinedOfUid:clientRole:isVideoEnabled:elapsed:
5. 用户离线的回调.
- rtcEngine:didOfflineOfUid:reason:
6. 用户被踢出频道的回调.
- rtcEngine:didKickedOutOfUid:reason:
7. 用户启用/关闭视频回调.
- rtcEngine:didVideoEnabled:byUid:
8. 远端首帧视频接收解码回调.
- rtcEngine:firstRemoteVideoFrameDecodedOfUid:size:elapsed:
9. 本地视频采集回调.
- rtcEngine:localVideoFrameCaptured:
10. 混屏创建回调.
- (void)rtcEngineVideoMixerCreated:
11. 网络连接丢失回调.
- rtcEngineConnectionDidLost:
12. 网络重连超时回调.
- rtcEngineReconnectServerTimeout:
13. 网络重连成功回调.
- rtcEngineReconnectServerSucceed:


# 注意事项
1. 如需白班插件可单独联系三体云销售。
