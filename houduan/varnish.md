#varnish简单介绍
     Varnish Cache是一个Web 应用加速器，也是一个知名的反向代理程序。你可以把它安装在任何http服务器的前端，同时对它进行配置来缓存内容。varnish真的很快，单台代理的分发速度可以达到300 - 1000x。
     我们此次修改为varnish的原因是
     1、原有的lua缓存有各种限制（货币，不同用户组折扣，仅能通过url区分）
     2、varnish 本身支持集群功能，为我们后续的扩展做准备
     3、varnish同样缓存与内存中
     4、varnsih的 vcl配置，及esi更加灵活
     
#<font color='red'>varnish的具体使用及与站点的结合我们会有专门的介绍及分享</font>