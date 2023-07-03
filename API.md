## API接口

## 介绍

​	**本文章旨在记录和学习 http抓包 和 android逆向 及 python自动化等技术，并无恶意传播。在此声明不用做任何的推广滥用。有任何疑问欢迎留言。**

### Base Url: https://tv.cctv.com/live

### 频道：首页、直播、听音、节目单、栏目大全、片库、热榜、视频百科、微故事、AI美食

### 1、首页

```java
webview加载入口：
https://tv.cctv.com/m/
```

#### 1.1部分效果图

| <img src="images\1.png" style="zoom:50%;" /> | <img src="images\2.png" style="zoom:50%;" /> |
| -------------------------------------------- | -------------------------------------------- |
| <img src="images\3.png" style="zoom:30%;" /> |                                              |


### 2、直播

```java
url: https://api.cntv.cn/epg/nowepg
{
	Method: GET
	params: 
	{
		c:cctv1,cctv2....[可变参数逗号分割]
		serviceId:tvcctv [default=tvcctv]
		cb:t [default=t]
	}
	response: 处理json：头——>"t("	尾——>");"
}
icon：https://t.live.cntv.cn/imagehd
{
    Method：Get
    params：
    {
        cctvx_01.png [可变参数cctv1_01.png、cctv2_01.png...]
    }
}
每个时段的详情：https://tv.cctv.com/lm/
{
    Method：GET
    params：每个时段的首字母拼音：{例如：第一时间=dysj、正点财经=zdcj}
}
```



#### CCTV1

```java
videoUrl：https://cctvwbndbd.a.bdydns.com/cctvwbnd/cctv1_2/index.m3u8
```

#### CCTV2

```java
1、正点财经时段：
列表详情：https://api.cntv.cn/NewVideo/getVideoListByColumn?id=TOPC1453100395512779&n=100&sort=desc&p=1&bd=20230612&mode=2&serviceId=tvcctv&cb=cb
{
    Method：Get
    params: bd：[例如：20230612]
}
videoUrl：	https://newcntv.qcloudcdn.com/asp/hls/main/0303000a/3/default/312ab1d0a3184ce0b4e668869a9b6fa4/main.m3u8?maxbr=2048
2、
https://ldcctvwbcdks.v.kcdnvip.com/ldcctvwbcd/cdrmldcctv5_1/index.m3u8
```

#### CCTV13

```java
1、cctv13播放时段列表接口：
https://api.cntv.cn/epg/epginfo3?serviceId=shiyi&d=20230612&c=cctv13&cb=LiveTileShow.prototype.getEpg
2、对应时段的详情:
https://vdn.apps.cntv.cn/api/getHttpVideoInfo.do?pid=6e7e815400324e4ca938b8e74b40e824
{
    Method：Get
    params：pid：[播放时段列表中item项的vid值]
}
3、对应时段的视频播放Url：
https://newcntv.qcloudcdn.com/asp/hls/main/0303000a/3/default/6e7e815400324e4ca938b8e74b40e824/main.m3u8?maxbr=2048
{
    来源：取 [对应时段详情接口] 中hls_url字段值
}
```

#### CCTV7

```java
1、cctv7播放时段列表接口：
https://api.cntv.cn/epg/getEpgInfoByChannelNew?c=cctv7&serviceId=tvcctv&d=20230613&t=jsonp&cb=jsonp11111
https://api.cntv.cn/NewVideo/getVideoListByColumn?id=TOPC1564110696628209&n=20&sort=desc&p=1&d=&mode=0&serviceId=tvcctv&callback=lanmu_0

https://api.cntv.cn/lanmu/columnInfoByColumnId?id=TOPC1564110696628209&serviceId=tvcctv&cb=Callback
2、对应时段的详情:
https://vdn.apps.cntv.cn/api/getHttpVideoInfo.do?pid=6487F36FD37DD7092382C7B5A2
{
    Method：Get
    params：pid：[播放时段列表中item项的vid值]
}
3、对应时段视频Url：
https://hls.cntv.kcdnvip.com/asp/hls/main/0303000a/3/default/ebc8ba438a764adda3650ffd076f5e1f/main.m3u8?maxbr=2048
{
    来源：取 [对应时段详情接口] 中hls_url字段值
}
所有的ts流：
https://tracker-00.qvb.qcloud.com/api/tracker/v2/htbt?channel=h5_live_hls_1252894780_default_v3__cctvwbcdbdabdydnscom_cdrmcctv7_1_index&pid=6488128FB148D7092382C864C5&mode=bat
ts流部分：
https://cctvwbcdbd.a.bdydns.com/cctvwbcd/cdrmcctv7_1/cdrmcctv7_1_1350-1686586021.ts
```

### 3、由于cctv更新频率快，准备后期加入python实现部分自动化更新链接，未完待续！！！

