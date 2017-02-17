- Fiddler

  - Fiddler在Chrome无法抓取，IE没有问题，出现这种情况一般是SwitchySharp设置了代理，直接选取System Proxy即可。
  
- VPN
  - gzremote.theknot.us 113.108.131.227 if gzremote cannot use. directly use the ip to connect.


- svn
svn://114.33.138.24:3361/wlp-web
svn://114.33.138.24:3361/wlp-admin
svn://114.33.138.24:3361/wlp-doc
svn://114.33.138.24:3361/wlp-time

install less
npm install -g less@latest

useage:
lessc a.less > a.css

sudo grunt build_compile
sudo docker ps [-a]
sudo docker start fe-tkp-dev

http://localhost/reports
Service Unavailable
HTTP Error 503. The service is unavailable.
解决方法:
http://stackoverflow.com/questions/8139778/what-might-cause-a-503-service-unavailable-for-reports-area-of-an-asp-net-mvc3-a

I fixed it with the following command:
netsh http delete urlacl url=http://+:80/Reports

原因：
SQL Server Report强制把Reports接管了，删除即可


果了Q3023284403
