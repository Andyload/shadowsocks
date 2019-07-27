1，登录远程服务器
	ssh root@xxx	----> xxx 远程服务器ip地址

2，安装ShadowsocksR软件（如果没安装wget，则先执行该命令：yum -y install wget）
	wget --no-check-certificate https://freed.ga/github/shadowsocksR.sh; bash shadowsocksR.sh

补充：如果后面想查看SSR账号信息的话，输入以下命令即可。
	bash ssr.sh
