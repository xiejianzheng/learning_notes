# 把命令行提示符中的目录进行缩减
	PROMPT_COMMAND='pwd2=$(sed "s:\([^/]\)[^/]*/:\1/:g" <<<$PWD)'
	PS1='\u@\h:$pwd2\$ '
