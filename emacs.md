# emacs使用锦囊

## 基础命令

	C-h m : 显示当前模式（mode）的帮助信息

### 文本导航
	
	C-f 光标右移一个字符
	C-b 光标左移一个字符
	M-f 光标右移一个word
	M-b 光标左移一个word
	C-v 向下翻动半个屏幕
	M-v 向上翻动半个屏幕
	C-p 上一行
	C-n 下一行
	C-a 行首
	c-e 行末
	M-a 句首
	M-e 句末
	M-< 文首
	M-> 文末
	
### 文本编辑

	C-d 删除当前字符
	M-BACKSPACE 删除前一个单词
	M-d 向后删除一个单词
	C-/ 撤销修改

### window导航
	
	使用 M-x windmove-default-keybindings 激活windmove
	然后就可以使用Shift-Up, Shift-Down, Shift-left, Shift-right在window间移动。
	
## magit

	C-x g(magit-status) 可以激活Magit Status Buffer,Status Buffer中会显示当前仓库的状态。

	TAB: 展开当前条目
	?: 显示帮助
	s: stage 当前选中的文件
	u: unstage 选中的文件
	l: 进入log模式
	d: 进入diff模式
	c: 进入commit模式 按C-c C-c 完成提交
	
	
	

	
