# EDM

* SPF（Sender Policy Framework，发信者策略架构）：一种为了防范垃圾邮件的DNS记录，用于登记某个域名拥有的所有用来外发邮件的IP地址；
* MX（Mail Exchanger，邮件交换记录）：一种DNS记录，用于指定负责处理发往收件人域名的邮件服务器。MX记录允许设置一个优先级，当多个邮件服务器可用时，会根据该值决定投递邮件的服务器。简单邮件传输协议（SMTP）会根据MX记录的值来决定邮件的路由过程；
* DKIM（DomainKeys Identified Mail，域名密钥识别邮件标准）：防止电子邮件欺诈；
* DMARC（Domain-based Message Authentication,Reporting & Conformance）：DMARC 协议基于现有的 DKIM 和 SPF 两大主流电子邮件安全协议，由Mail Sender方（域名拥有者Domain Owner）在 DNS 里声明自己采用该协议。当Mail Receiver方（其MTA需支持DMARC协议）收到该域发送过来的邮件时，则进行DMARC校验，若校验失败还需发送一封report到指定 URI（常是一个邮箱地址）。
