---
title: Unity网络通同步工具-Photo
date: 2020-07-03 13:22:02
tags: 
    - Photon
categories: 
    - 游戏引擎
    - Unity
    - Photon
cover: /img/cover3.png
top_img: /img/cover3.png
mathjax: false
description: 简单了解在Unity引擎中使用Photon进行简单的网络同步测试
---
## 申请photon账号
## 申请游戏appid
## 申请登录中国区Photoncloud服务器
## 下载安装PUN2
&ensp;&ensp;&ensp;&ensp;在Unity中新建项目并下载安装PUN2.设置PhotonServerSettings中Setting  的AppId
## 修改Photon的配置使程序可以使用中国区Photon cloud
### 在loadBalancingClient.cs找到NameServerHost
### 将国外域名改为国内域名
&ensp;&ensp;&ensp;&ensp;将public string NameServerHost = "ns.exitgames.com";改为"ns.photonengine.cn"
### 在\Assets\Photon\PhotonUnityNetworking\Resources中找到PhotonServerSettings
### 在setting中将FixedRegion改为cn
## 建立登陆场景Start并测试是否可以登录Photoncloud
### 建立UI button，文本“联机游戏”
### Create Empty 并改名NetworkManager
### 建立NetworkManager.cs并加载到NetworkManager
### 修改NetworkManager.cs 并测试联网

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

//导入 
using Photon.Pun;
using Photon.Realtime;

public class NetworkManager : MonoBehaviourPunCallbacks //修改为MonoBehaviourPunCallbacks
{
    //---------------------------连接---------------------------------//
    public void Connect()
    {
        if (PhotonNetwork.IsConnected) //如果已经连接 Photon cloud
        {
            //进入房间，开始游戏
            PhotonNetwork.JoinRandomRoom();
        }
        else//如果没有连接 Photon cloud
        {
            //取消离线模式
            PhotonNetwork.OfflineMode = false;
            //玩家名称 PhotonNetwork.NickName = "Player";
            //游戏版本 PhotonNetwork.GameVersion = gameVersion;
            //开始连接
            PhotonNetwork.ConnectUsingSettings();
        }
        
    }
    //---------------------连接master回调函数---------------------------
    public override void OnConnectedToMaster()
    {
        Debug.Log("PUNBasicsTutorial/Launcher:OnConnectedToMaster() was called by PUN");
        Debug.Log("--------------连接成功！--------------");

        //加入随机room
        PhotonNetwork.JoinRandomRoom();

    }

    public override void OnDisconnected(DisconnectCause cause)
    {
        Debug.LogWarningFormat("PunEvent Basics Tutorial/Launcher:OnDisconnected() was called by PUN with reason{0}",cause);
        Debug.Log("--------------断开连接！--------------");
    }

    //-----------------加入Room回调函数---------------------------
    public override void OnJoinRandomFailed(short returnCode, string message)
    {
        Debug.Log("");
        Debug.Log("--------------加入房间失败！-----------------");
        Debug.Log("--------------建立新房间!-------------------");
        PhotonNetwork.CreateRoom(null, new RoomOptions{ MaxPlayers = 8});
    }

    public override void OnJoinedRoom()
    {
        Debug.Log("");
        Debug.Log("---------加入Room成功！");

        //Load 一个游戏场景
        PhotonNetwork.LoadLevel("GameLevel1");
    }
}
```



## 建立单机游戏场景 GameLevel1

略

## 将单机游戏场景改为多人联网游戏

* 建立游戏场景管理者

* 建立游戏资源文件夹保存需要同步的player和子弹bullet 为prefab

  PS.注意，一定要放在asset下的Resources文件下

* playe prefab 加载 PhotonView组件

* 将player的Transform拖到Photon View上 

* bullet prefab 加载 PhotonView组件

* 将bullet 的Transform拖到Photon View上 

* 判断是否本机玩家

```
using Photon.Pun;
public class PlayerController : MonoBehaviourPun //改为MonoBehaviourPun
...

//检测是否本机玩家 ,如果不是，不做控制
        if(photonView.IsMine == false && PhotonNetwork.IsConnected == true)
        {
            return;
        }
```

* 为敌人添加Photon view组件，并同步位置
* 使用Photon的PhotonNetwork.Instantiate方法同步生成子弹对象
* 使用Photon的PhotonNetwork.Destory方法同步销毁子弹对象

```
using Photon.Pun;
public class bulletMove:MonoBehaviiourPun{
...
PhotonNetwork.Destory(gameobject);
```

* 在生成敌人时判断玩家是否是主玩家或者采用单例模式 避免重复生成敌人

```
if(PhotonNetwork.IsMasterClient)//玩家是不是master
{

}
```



## 开始游戏

# 方法类

