# 把命令行提示符中的目录进行缩减

	PROMPT_COMMAND='pwd2=$(sed "s:\([^/]\)[^/]*/:\1/:g" <<<$PWD)'
	PS1='\u@\h:$pwd2\$ '

# tmux中启动的窗口是非login Shell，不会加载.bashrc中的指令
	
	需要处理的化，直接在运行 source ~/.bashrc

# 删除find指定的文件

其中一种执行方案是：使用find的exec命令。
exec是find用来对搜索结果执行命令的的子指令。
格式是：

	-exec <命令名> {} ;

	{}	是find结果文件名的占位符
	;  	是exec子命令结束标志，在bash环境中";"会被当成命令的分隔符需要使用反斜杠来防止转译。\;
	


