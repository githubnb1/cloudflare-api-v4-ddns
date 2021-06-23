# cloudflare-api-v4-ddns

在 Cloudflare 中新建一个 A 记录，如：ddns.xxxxx.com，指向 1.1.1.1（可随意指定，如 123.123.123.123 等等，主要用于后续查看 DDNS 是否生效）

下载 DDNS 脚本，修改配置  
```
sudo wget https://raw.githubusercontent.com/githubnb1/cloudflare-api-v4-ddns/master/cf-v4-ddns.sh -O /usr/local/bin/cf-ddns.sh

sudo chmod +x /usr/local/bin/cf-ddns.sh

sudo nano /usr/local/bin/cf-ddns.sh
```  
修改`default config`下的几个配置变量  

1.CFKEY 就是第一步获取的 global key

2.CFUSER 是登录 cloudflare 的邮箱

3.CFZONE_NAME 是你的一级域名

4.CFRECORD_NAME 则是用于 DDNS 的二级域名

5.CFTTL 是域名生效的 ttl，默认 120 即可

设置定时任务
`crontab -e`  

在最后一行加上`*/2 * * * * /usr/local/bin/cf-ddns.sh >/dev/null 2>&1`  

如果需要日志就换成这条`*/2 * * * * /usr/local/bin/cf-ddns.sh >> /var/log/cf-ddns.log 2>&1`  
