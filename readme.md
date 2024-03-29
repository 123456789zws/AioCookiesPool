# AioCookiesPool

基于python asyncio的web网站cookie管理项目；目前提供周期性的登陆获取指定网站Cookie，检测Cookie是否有效，
异常账号睡眠，通过API获取Cookie以及查看Cookie使用情况等功能。

> 项目逻辑参考[cookiespool](https://github.com/Python3WebSpider/cookiespool) 项目。

模块功能简介：
- api：对外接口服务，随机获取cookie，添加账号等
- generator：生成器，依次登陆账号生成cookie
- tester：测试器，测试cookie是否有效
- monitor：监视器，非必要，监控账号黑名单
- scheduler：调度器，调度其他模块

> monitor模块：在实际业务中，1，当tester检测失败时，可以让账号休眠一段时间（放入黑名单），等再次重试；2，由于tester模块测试链接是单一的，比较局限，
> 会出现tester检测时cookie可用，客户端使用时出现被网站
> '封禁'的情况，此时需要客户端通过API回传'被封禁'的账号，将此账号放入黑名单的休眠一段时间，黑名单中的账号不会参与generator和tester，
> monitor模块就是为了检测黑名单中的账号封禁了多久？判断是否可以重新启用（从黑名单中删除）。

demo编写：
- [ ] weibo.com 微博cookie管理
- [ ] gsxt.gov.cn 企业信息公示系统cookie管理
- [ ] 欢迎pr

更多问题，欢迎进入群聊讨论：[TG群聊](https://t.me/+If_iQcOzumthOGI1)


# 安装和运行
安装
```shell
pip install -r requirements.txt
```
运行全部模块
```shell
python main.py
```
```shell
2023-12-13 15:28:49.520 | INFO     | aiocookiespool.scheduler:api:50 - API接口开始运行
DEBUG:asyncio:Using selector: KqueueSelector
======== Running on http://0.0.0.0:5200 ========
(Press CTRL+C to quit)
2023-12-13 15:28:49.761 | INFO     | aiocookiespool.scheduler:generator:23 - Cookies生成进程开始运行
2023-12-13 15:28:49.762 | INFO     | aiocookiespool.scheduler:tester:32 - Cookies检测进程开始运行
2023-12-13 15:28:49.762 | INFO     | aiocookiespool.scheduler:monitor:41 - 黑名单检测程序开始运行
```
运行指定模块
```shell
python main.py --processor generator
```
```shell
2023-12-13 15:27:46.031 | INFO     | aiocookiespool.scheduler:generator:23 - Cookies生成进程开始运行
```

