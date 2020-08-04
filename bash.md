# 把命令行提示符中的目录进行缩减

PROMPT_COMMAND='pwd2=$(sed "s:\([^/]\)[^/]*/:\1/:g" <<<$PWD)'
PS1='\u@\h:$pwd2\$ '

# tmux中启动的窗口是非login Shell，不会加载.bashrc中的指令

需要处理的化，直接在运行一个bash就可以



