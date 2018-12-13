Proxy Pool
==========
包含http(s)/socks的极简代理池服务。


> python3.6  
> windows 


### 说明

* 为什么叫极简？

	你可能已经搜过关于代理池，大多用到了数据库储存，打分，提前验证什么的，定时刷新（嗯..这个功能我用一种相比更简单的方式也加上了），复杂、不那么简单，动手做的过程中慢慢发现了问题。。。
		
	免费代理根本不需要用数据库做保存，也不需要验证好了放数据库，需要的时候拿。免费代理就像丢盔弃甲的残兵败将，有力气的还能挥两下钝剑，也就那两下，上一秒活着，下一秒就死了，又或者这一秒躺着像个死人，下一秒又爬起来走两步，
	
	**极低的质量和极低的稳定性**根本**不值得**提前做验证使用数据库当宝一样保存起来。就用pickle就好。
		
	这个代理池的核心部分也就100来行，即便是初学者，也能快速开始使用。建议你先从爬代理的两个py开始看。
		

* 啥功能?

	通过requests get方法获取一个socks代理 
	
	```requests.get('localhost:5000/socks/').text```
	
	<img src="https://github.com/Shaw-lib/Proxy-pool/raw/master/getsocks.png" width="20%" height="20%">
		
	通过requests get方法获取一个http(s)代理 
	
	```requests.get('localhost:5000/https/').text```
	
	<img src="https://github.com/Shaw-lib/Proxy-pool/raw/master/gethttps.png" width="20%" height="20%">
		
	通过requests get方法手动刷新proxypool，如果需要的话。
	
	```requests.get('localhost:5000/refresh/').text```
	
	 定时任务是每过10分钟自动刷新一次
	
	 ```scheduler.add_job(
    func=refresh,
    trigger=IntervalTrigger(minutes=10),
    id='refresh_ProxyPool',
    name='Refresh ProxyPool every ten minutes',
    replace_existing=True)```
	
	
	 **注：** 
	 
	 GatherProxy.com的服务器很脆弱，服务器经常崩掉请求不到数据，请爱护它 0.0

--------------

### 那么，开始吧

* 准备

	1.建议使用虚拟环境
	
	```virtualenv proxypool```
	  
	```cd proxypool/Scripts```
	  
	```activate```
	  
	2.需要的第三方库，你可以通过requirements.txt安装，也可以直接复制下面这条命令
	
	```pip install requests lxml beautifulsoup4 flask apscheduler ```
	
	3.开启服务
	
	```python app.py ```
	
	4.打开浏览器试验一下
	
	```localhost:5000/```
	
	<img src="https://github.com/Shaw-lib/Proxy-pool/raw/master/localhost.png" width="20%" height="20%">

到此，服务部署完了！

* PLUS

	**Tips:** usage.py是一个使用代理池服务的小爬虫案例，有点麻烦只是，你需要在爬虫项目中通过requests获得一个随机的代理，我不能保证这个代理就能用，毕竟免费的，所以我们直接给爬虫用，不行就换一个。


------------


**欢迎交流:**

	QQ:584927688
