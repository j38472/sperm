> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [mp.weixin.qq.com](https://mp.weixin.qq.com/s/sVz0ZYK7-x9kpHqDjYds0g)

### 前言

今天堂主带大家玩点硬核的：利用 AI 辅助逆向工程，操作一款 2022 年的 macOS 应用 `***editor。`

这款软件默认只有 30 天试用期，但通过 AI 的逻辑分析与补丁，我们将尝试让它的生命力延续到 “掩体纪元”。

* * *

### 一、 目标分析

我们今天的目标是 `***editor。`打开应用点击 **Register，**可以清晰地看到 30 天试用的提醒。

![](https://mmbiz.qpic.cn/sz_mmbiz_png/avC2Wrv2EkN6nHHqeuphp8TxhPdNmdLJtibasiawjqD1kgDN1muX5vHPcyenialxJXfOcso4CbjvPUIpovC6dCCj93zsWneES8Bh4TZWzSlsIk/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=0)

在开始动手前，我们先观察一下它的文件结构。

![](https://mmbiz.qpic.cn/sz_mmbiz_png/avC2Wrv2EkPzIPzcznZMuCd5GKK1yXc20Ux8MCicyHTvbNN6NC4y7hiblopZ7xTqlTGAtGmZjm8IhDJ9vEybYZMR8rPyqzPpxRVlmTGdYVN7w/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=1)

* * *

### 二、 环境准备：导出关键信息

逆向的第一步不是盲目修改，而是通过 IDA Pro 获取程序的逻辑结构。为了让 AI 能更好地理解代码，我们祭出某大佬的开源神兵：**IDA-NO-MCP。**

*   **项目地址：**`https://github.com/P4nda0s/IDA-NO-MCP/`
*   **作用：**将 IDA 中的伪代码和结构高效导出，方便 AI 快速理解逻辑。

#### 安装方法：

1.  下载 `INP.py。`
2.  将其复制到 IDA 的插件目录：

*   **Windows:**`%APPDATA%\Hex-Rays\IDA Pro\plugins\`
*   **Linux/macOS:**`~/.idapro/plugins/`

4.  重启 IDA。

#### 导出操作：

在 IDA 中通过快捷键 `Ctrl-Shift-E` 或菜单栏 `Edit -> Plugins -> Export for AI` 启动导出。

![](https://mmbiz.qpic.cn/sz_mmbiz_png/avC2Wrv2EkMicnmGoibWN1L9UFNmUibegrLIGBAvubcdD2fG64Aa3lSnWOD6WssZqVP1dNyYT2icY9MxdxDGYue1PFM73B5QMbp0aic8aF2uJdNI/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=2)

![](https://mmbiz.qpic.cn/mmbiz_png/avC2Wrv2EkNiacba8icDvB0vLXhPcEuNicV94Are67FTZPuE86EyKA1aYngvGCqS9StCm5NicyZXsdibqIzaXUqa6Q3kH0icAdZGyiby3FN2CEBXdo/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=3)

等待片刻，可以看到导出完成。

![](https://mmbiz.qpic.cn/sz_mmbiz_png/avC2Wrv2EkMOz5DKvrM02HHic6nC3M259WAROGqiaHz64U5WqzABCahY0F2tgrM5poD1xKicicThOygCoQcJycDuicNXBe6zicQuntDCEFbaCcOs8/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=4)

![](https://mmbiz.qpic.cn/mmbiz_png/avC2Wrv2EkN8btAsOc7hNSEJUibkj470RRM4ib3VR8G1micMSI70qZBuib3Vwg5ZSaCCObo8N2UtlHCAT3lNBibjQsK36Pxc30tlKMW7XwL1jnMQ/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=5)

* * *

### 三、 AI 介入：Skill 魔法

拿到导出的信息后，我们请出今天的主角——**Cursor**。为了让 Cursor 具备逆向分析的专有知识，我们需要加载一份特殊的 **Skill**（技能包）。

![](https://mmbiz.qpic.cn/sz_mmbiz_png/avC2Wrv2EkPlfsib9r7FwibBXPI6ic626YhU818JIibvYW0M1ticXkkfhwaWibP51PP1eScgD0PE0eWGxKdChycNPEdEmendy519RyIFiar0HAiab8Y/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=6)

![](https://mmbiz.qpic.cn/mmbiz_png/avC2Wrv2EkOMjR0pmOl7kxmiaYugVuwDyhJpy788zgWvL9LS50R3XKVALg6CeG1p0vuuXINicM7x6uGQ4Nr8XgkQ1ZIp6esVt1H5iaEGqdFoYQ/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=7)

  

1.  将逆向专用 Skill 文件放入 Cursor 的技能目录：`~/.cursor/skills。`  
      
    
2.  在 Cursor 界面中确认 Skill 已成功加载。

* * *

### 四、 见证奇迹：向 AI “许愿”

万事俱备，现在到了最激动的时刻。我们将导出的代码信息喂给 AI，并输入我们的 “许愿” 提示词：

> **Prompt：** 
> 
> ![](https://mmbiz.qpic.cn/sz_mmbiz_png/avC2Wrv2EkNJf8GianTLm5FHsm1kZ1hkbnHQwgMHEdv4NkNkTsYYmJlSzELupv0iahdaAYJ6icfug1giaSyRyibBYuvcZCgeVd70O0nIOOu13KFg/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=8)

AI 开始飞速思考，片刻之后，它便给出了修改建议和 Patch 方案。

开始操作

![](https://mmbiz.qpic.cn/sz_mmbiz_png/avC2Wrv2EkPjJ970wy5bxf8yZGxknDCBrF3l5Nv8z4zIpn8BmYfExp5RhSLCFf5wmoxKR0mZprteibOWS0VA5sTCuU0ysAZ7bTRlVTNdV7CA/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=9)

patch

![](https://mmbiz.qpic.cn/mmbiz_png/avC2Wrv2EkMX0QtrjscwBqosL1NG1dtKTUyxxia9XbIAkOY5sbafibbJ1eq87FlUcr2qvnrjVIlHAoczsWJToSFib6kHfrM9cu6Z9JH8goM1Nw/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=10)

帮忙验证

![](https://mmbiz.qpic.cn/mmbiz_png/avC2Wrv2EkNe1RkYzqNdsdt5SlkzrCibgibC1icJOE7A29QUGBnSl33XzsicicZx6qicQBJ6InCturGicj5QTRYMTcSgkXjqmpvBfJ7ujbjx76pUsk/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=11)

* * *

### 五、 结果验证

我们将 AI 生成的 Patch 应用到程序中，重新编译并运行。

再次打开应用，进入注册页面，随意输入一个用户名和密码，点击 **Check License。**

![](https://mmbiz.qpic.cn/sz_mmbiz_png/avC2Wrv2EkMtuzJiaxAcIXXNC7YribLKVaDM8zsFMWJQ7sNILZzVG5kqvgvg2TPNk27nyStJlWQjULMbzqmiaoNicbZvl0nRA5zmic8D8XSG0icH8/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=12)

**Mission Complete！** 弹窗消失，软件正式进入 “无限使用” 模式。

![](https://mmbiz.qpic.cn/sz_mmbiz_png/avC2Wrv2EkMUnj5PlIsqiceRrFNkByPdtiaTgv38n7iahribA4UUibtnWvUCSncFeGJTjYfCg0qLxMsxYPtbx6w9bDgJCpHjzibmbYc2Bc7fCiccD8/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=13)

![](https://mmbiz.qpic.cn/mmbiz_png/avC2Wrv2EkOemamWKPJflPOuH3Y8t8LL9pMSicLyOA5YKSLnDsEGibGvuFyFia8tIbNiaD1k176c7ibjblMr4xXuZT1vKGvl5Ted0gcwfkEZF1vw/640?wx_fmt=png&from=appmsg&watermark=1#imgIndex=14)

* * *

### 结语

整个过程行云流水，这便是 **AI + 逆向工程** 带来的高效体验。

这类逆向工作，对紫星老师、正己老师等圈内大佬而言不过是探囊取物。但技术的魅力就在于普惠，有了 AI 的辅助，让堂主这样的人，也能窥见高处的风景了。

今天，我们还需要给它配上专属的 Skill 当‘外脑’，还需要手动导出 IDA 数据来‘喂饭’才能完成破解。但谁知道呢？也许就在明天，某次大模型迭代之后，它原生的能力就能直接平推这一切。未来的逆向，或许真的只剩下一句 Prompt 的事了。

ps：对了在完成这个操作以后，堂主立刻删除了这个应用，因为这只是一次以学习为目的的探索之旅。