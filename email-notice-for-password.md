

前提条件
1. 创建一个directory： un***aws.internal
2. 启动一个workspaces实例

架构
见 02-email-notice-arch.png


目前宁夏区域没有Workmail和SES服务，可以用AWS global账户的服务。

一、	Workmail的配置
1.登陆AWS global账户管理界面
2.创建Workmail的OU：mail***.awsapps.com，创建用户admin和user1/user2

3.在手机客户端配置邮件服务器，用三个用户进行收发邮件，确认邮件地址可以使用。
二、	配置SES
1.添加收件人的邮件地址（非mail***的用户邮箱），并进行验证
2.在SES界面测试收件人地址的收发邮件
3.创建并记录SES的SMTP的验证信息：AKSK

三、通知服务器的配置
查找用户和密码期限
1.创建一个EC2实例作为通知服务器，添加role并加入域，并用域的admin登陆
2.在AD用户管理界面，创建多个域用户user01/user02，配置邮件地址user1@mail***.**
3.运行脚本查看用户和密码期限
 脚本中Send-Mailmessage这一行添加 -Port 587

四、	配置Secret Manager
1.把SES的SMTP的AKSK添加到新的Secrets
2.为通知服务器添加Secret Manager的role
五、	测试邮件通知
1.运行脚本，查看邮件通知是否收到
2.将脚本配置为定时执行的任务

