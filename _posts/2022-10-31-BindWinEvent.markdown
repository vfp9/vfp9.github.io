---
layout: post
title:  "BindWinEvent"
date:   2022-10-31 16:00:00 -0500
categories: vfpx update
---

[BindWinEvent](https://github.com/JoelLeach/BindWinEvent) 是一个小框架，允许对Windows消息事件进行多重绑定。来自VFP帮助文件中的BindEvent()主题：
*当绑定到 Windows 消息 (Win Msg) 事件时，只有一个到 Windows 消息配对的 hWnd 可以存在。*

当多个VFP程序试图绑定到同一个Windows消息事件时，这可能会导致冲突。这个框架通过有效地将Win Msg事件转换为标准的Fox事件并相应地跟踪它们。
