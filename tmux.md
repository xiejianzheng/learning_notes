# tmux使用技巧

## 复制粘贴
	
	C-b [    	: 进入复制模式

	R        	: 打开矩阵选择模式，如果不按R，C-SPACE会缺省进入行选择模式
	C-SPACE  	: 开始复制
	C-w, M-w 	: 提交选中的缓冲
	C-b ]    	: 粘贴

## windows相关

	C-b ,		: 设置标题

	swap-window [-s 源窗口id] [-t 目标窗口id]

## pane相关
	
	C-b %		: 垂直分割面板
	C-b "		: 水平分割面板·

	C-b up		: 将光标移动到当前面板上方的面板中
	C-b down	: 将光标移动到当前面板下方的面板中
	C-b left	: 将光标移动到当前面板左方的面板中
	C-b right	: 将光标移动到当前面板右方的面板中



