# nginx反向代理配置相关指令

1.
	proxy_pass URL;
	
	设置协议、地址属于一个被代理的服务器，还有一个可选的URI一个位置应该被映射到。
	[$protocol://]$host[:$port][$uri]
	如果$uri不为空，则原路径中的位置部分会被$uri替换掉。


2.	
	proxy_redirect ${需要被替换的路径} ${用于替换的路径}

	proxy_redirect 指令用于设置文本在Location和Refresh头部字段属于一个被代理的服务器的应答。



