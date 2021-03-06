# 利用GitHub action自动运行脚本

简单介绍，有问题请提issue

## 主要流程

1. fork本项目

2. Settings - Secrets    填写cookie信息，此处专用于保存私密信息

3. 将其命名为`JD_COOKIE`

4. 可能需要提交一次修改才会启动workflow (很多人反馈fork后没有自动运行，原因可能在此)

   ![Snipaste_2020-08-13_20-09-30](p/Snipaste_2020-08-13_20-09-30.png)

请严格按照以下格式填写，以免[jdCookie.py](https://github.com/Zero-S1/JD_tools/blob/master/jdCookie.py)识别不了；多个账号换行

```
pt_pin=aaaaaaa&pt_key=bbbbbbbbbbbbbb
pt_pin=ccccccccc&pt_key=dddddddddddddd
```



## 查看运行状态

actions 查看对应的workflow

![](p/Snipaste_2020-08-13_20-17-12.png)

进入 build  查看具体情况

![Snipaste_2020-08-13_20-18-10](p/Snipaste_2020-08-13_20-18-10.png)



## 关于cron定时运行

需要修改的，请至`.github/workflows`修改对应的yml文件

其中cron 语法使用的是UTC (世界标准时间)，中国处于东八区，因此中国的时间需要加8，

例如 

```shell
cron 0 0 * * *   #此处表示在国际标准时间0点（北京时间+8，即早上8点）运行
```

注意：计划的action最多可能会延迟15分钟。这样做是为了在繁忙时间（例如，UTC上午12:00）保持可靠性。预定的工作流程不应假定它们以最新的准确性启动。


## 参考
http://www.ruanyifeng.com/blog/2019/09/getting-started-with-github-actions.html
