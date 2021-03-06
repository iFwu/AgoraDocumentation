
---
title: Build a Client
description: 
platform: iOS
updatedAt: Mon Jul 20 2020 06:36:11 GMT+0800 (CST)
---
# Build a Client
This article describes how to implement the basic features of Single Host.

## Flowchart

Refer to the flowcharts for the following functions:

- Joins and leaves the room.

![](https://web-cdn.agora.io/docs-files/1594377181071)

## Integrate the SDK

Refer to the following table to integrate the SDKs into your project:


| Product | SDK downloads | Integration guide |
| ---------------- | ---------------- | ---------------- |
| [Agora RTC (Real-time Communication) SDK](https://docs.agora.io/en/Interactive%20Broadcast/product_live?platform=All%20Platforms)      | [Agora SDK for iOS](https://docs.agora.io/en/Agora%20Platform/downloads)      | [Start Live Interactive Video Streaming](https://docs.agora.io/en/Interactive%20Broadcast/start_live_ios?platform=iOS) |
| [Agora RTM (Real-time Messaging) SDK](https://docs.agora.io/en/Real-time-Messaging/product_rtm?platform=All%20Platforms) | [Real-time messaging SDK](https://docs.agora.io/en/Real-time-Messaging/downloads) | [Peer-to-peer or Channel Messaging](https://docs.agora.io/en/Real-time-Messaging/messaging_ios?platform=iOS) |
| [Third-party Image Enhancement SDK](https://www.faceunity.com/#/developindex) | N/A | [iOS SDK Integration Guide](https://www.faceunity.com/docs_develop_en/#/nama_api_docs/iOS/docs/iOS_Nama_SDK_Integration_Guide) |


## Core API call sequence

The following diagrams show the core APIs that the Agora Live Demo app uses to implement a Single Host scenario. Refer to them to implement the various functions in your project.

<div class="alert note">The Cloud Service in the demo app is implemented by Agora, and you need to deploy your own cloud service for the same purposes.</div>

- The host joins the room and starts the interactive streaming.

   ![](https://web-cdn.agora.io/docs-files/1595225702765)

## Core API reference

- Agora RTM SDK

| API | Function |
| ---------------- | ---------------- |
| [initWithAppId](https://docs.agora.io/en/Real-time-Messaging/API%20Reference/RTM_oc/Classes/AgoraRtmKit.html#//api/name/initWithAppId:delegate:)       | Creates an RTM Client object.      |
| [loginByToken](https://docs.agora.io/en/Real-time-Messaging/API%20Reference/RTM_oc/Classes/AgoraRtmKit.html#//api/name/loginByToken:user:completion:) | Logs into the Agora RTM system.|
| [createChannelWithId](https://docs.agora.io/en/Real-time-Messaging/API%20Reference/RTM_oc/Classes/AgoraRtmKit.html#//api/name/createChannelWithId:delegate:) | Creates an Agora RTM channel. |
| [joinWithCompletion](https://docs.agora.io/en/Real-time-Messaging/API%20Reference/RTM_oc/Classes/AgoraRtmChannel.html#//api/name/joinWithCompletion:) | Joins the RTM channel.|
| [sendMessage](https://docs.agora.io/en/Real-time-Messaging/API%20Reference/RTM_oc/Classes/AgoraRtmChannel.html#//api/name/sendMessage:completion:) | Sends a channel message, which can be received by all users in the channel. |
| [leaveWithCompletion](https://docs.agora.io/en/Real-time-Messaging/API%20Reference/RTM_oc/Classes/AgoraRtmChannel.html#//api/name/leaveWithCompletion:) | Leaves the RTM channel. |
| [logoutWithCompletion](https://docs.agora.io/en/Real-time-Messaging/API%20Reference/RTM_oc/Classes/AgoraRtmKit.html#//api/name/logoutWithCompletion:) | Logs out of the Agora RTM system. |

- Agora RTC SDK

| API | Function |
| ---------------- | ---------------- |
| [sharedEngineWithAppId](https://docs.agora.io/en/Interactive%20Broadcast/API%20Reference/oc/Classes/AgoraRtcEngineKit.html#//api/name/sharedEngineWithAppId:delegate:)      | Creates an RtcEngine object. |
| [setChannelProfile](https://docs.agora.io/en/Interactive%20Broadcast/API%20Reference/oc/Classes/AgoraRtcEngineKit.html#//api/name/setChannelProfile:) | Sets the channel profile. In a Single Host scenario, the channel profile is set as `Broadcasting`.|
| [setClientRole](https://docs.agora.io/en/Interactive%20Broadcast/API%20Reference/oc/Classes/AgoraRtcEngineKit.html#//api/name/setClientRole:) | Sets the user role in interactive streaming.|
| [enableVideo](https://docs.agora.io/en/Interactive%20Broadcast/API%20Reference/oc/Classes/AgoraRtcEngineKit.html#//api/name/enableVideo) | Enables video.|
| [setupLocalVideo](https://docs.agora.io/en/Interactive%20Broadcast/API%20Reference/oc/Classes/AgoraRtcEngineKit.html#//api/name/setupLocalVideo:) | Sets the local video view. Call this method on the host's client to configure the view of the host on the local device. |
| [joinChannelByToken](https://docs.agora.io/en/Interactive%20Broadcast/API%20Reference/oc/Classes/AgoraRtcEngineKit.html#//api/name/joinChannelByToken:channelId:info:uid:joinSuccess:) | Joins the RTC channel. |
| [leaveChannel](https://docs.agora.io/en/Interactive%20Broadcast/API%20Reference/oc/Classes/AgoraRtcEngineKit.html#//api/name/leaveChannel:) | Leaves the channel. Use this method to quick switch to another live-broadcast channel. |

## Additional functions

**Image enhancement**

The Agora Live Demo app uses a third-party SDK for image enhancement. You can refer to the source code in the faceunity file to implement the function.

**Network quality detection**

Use the `reportRtcStats` callback to detect and report the network quality in real-time. Triggered once every two seconds during a live broadcast, this callback reports statistics, including the sending and receiving bitrate and packet loss rate.

**Mute the local audio and video**

Call `muteLocalAudioStream` or `muteLocalVideoStream` to stop sending local audio or video streams.

**In-ear monitoring**

Call `enableInEarMonitoring` to enable the in-ear monitor function on the host's client.

**Audio mixing**

After joining the channel, call `startAudioMixing` on the host's client to play background music.

## Open-source sample project

Agora provides an open-source sample project for [Single Host](https://github.com/AgoraIO-Usecase/AgoraLive) on GitHub for you to download as a source code reference.
