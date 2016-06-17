
参考文章:
-----------
[1. Access Services 2013 Setup for an On-Premises Installation] (https://blogs.msdn.microsoft.com/kaevans/2013/07/14/access-services-2013-setup-for-an-on-premises-installation/)

[2. White Paper: Office 2013--Access Services Setup for an On-Premises Installation] (https://www.microsoft.com/en-us/download/details.aspx?id=30445)

[3. 为 SharePoint 相关应用程序配置环境 (SharePoint 2013)] (https://technet.microsoft.com/zh-cn/library/fp161236(office.15).aspx)


要点步骤：
---------

1. 首先要 **为应用程序配置SharePoint Server**

    1) 设置DOMAIN的DNS： 部署SPS App时， SPS 会通过DNS 的设置来查找本地服务器。

    2）配置要使用的应用程序 URL

2. 使用SPS配置向导安装场， 建议删除以下服务后，然后按 应用程序配置环境 说明手工重建：

    1) App Management Service

 3. 必须创建一个 根目录的网站集， 然后才能通过ACCESS 2013 来创建子目录WEB APP下如：如要在http://xxx.com/sites 下创建 Access APP， 必须有先创建一个Http://xxxx.com/的网站集， 否则会报错。

4. 如果 Secure Store Service  的 密钥生成是出错， 请检查 Claims to Windows Token Service 是否启动

    Central Administration--》Application Management --》Manage services on server --》

    手工启动后， 需重新启动IIS

5. 设置SPS 服务器管理帐号和服务运行帐号

    1） 不能使用服务器管理帐号做为APP部署帐号， SPS安全设置不允许

    2）服务运行帐号与SPS管理员帐号不一致，需要设置对应的权限，包括 SPS服务器本地管理员及SQL服务器对应数据库访问的权限：
•App Server DB
•WSS_Content
•SharePoint_Config

    3) SPS不建议将SPS管理帐号做为服务运行帐号， 以避免不必要的安全问题

6. 为应用程序配置SharePoint Server后， 再按白皮书的步骤设置ACCESS服务本地服务器

Tip:
----

1. 安装中文版SPS2013， 卸载后再装英文版，在配置时出现：The language is not supported on the server 的错误，需删除注删表：

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Shared Tools\Web Server Extensions 键

然后再重新安装英文版 SPS 2013

2.测试时出现SQL Server 和 SPS 不在同一台服务器时， 能创建和导入本机创建的APP, 导入其他服务器创建的APP出错. 如果出现这种情况， 可能是SQL SDK TOOLS安装不全导致。 ·解决方法：`把SQL SERVER 和 SPS 安装在同一台服务器， 确认APP能正常创建和导入后， 这时可以卸载SQL SERVER, 然后再重装SQL SDK TOOLS, 问题解决（SQL SDK TOOLS内容参见白皮书）`
