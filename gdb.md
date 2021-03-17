# gdb常用调试操作锦集

## 常用功能

* run 运行程序

* b, break 设置断点

	break <代码位置>
	break if <条件>
	info break 查看所有<断点序号>
	condition <断点序号> <条件>
	
* n, next 	下一步，跳过函数细节

* step 	进入函数内部
* finish 	退出函数内部

* c, continue 	继续



* ctrl-c 中断程序执行
	
* 检查变量

	print <变量名>
	
* 设置监视点，监控变量的变化
	
	watch <条件>
	
* 上下移动调用栈

	函数调用期间，与调用关联的运行时信息存储在称为栈帧（stack frame）的内存区域中。
	每一次发生函数调用时，栈中都会创建一个新的栈帧，栈顶的帧对应当前正在执行的函数。
	
	frame 命令可以在不同栈帧中移动。
	        -----------
	frame-> | 0 frame |
	        -----------
			| 1 frame |
	        -----------
			| 3 frame |

	frame <目标帧号>
	
	bracktrace 查看整个堆栈

## 调试经验

* gdb热加载程序

	也就是说，你可以在程序重新编译后在继续在gdb中调试，无需退出当前的gdb session。
	你原来设置的断点还好继续生效。


* gdb调试有配置参数且有环境变量的程序

如形式如下的：

	LD_PRELOAD=./libkcpd_results.so ./kcbp-worker --so ./lbm_launcher.so --entry "Launch" --funcid 0 -n "hello"

要如何调试该程序：

	1.通过gdb加载程序：gdb ./kcbp-worker
	2.设置LD_PRELOAD环境变量： gdb environment LD_PRELOAD=./libkcpd_results.so
	3.设置合适的断点
	4.run运行程序

	
	

	
	

	
  
