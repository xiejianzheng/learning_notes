# 链接和加载

## 链接器和加载器是干什么的？

链接器和加载器的目的都是： *符号*绑定到一个底层的内存*地址*。
	
## 链接器和加载器的历史
	
在有操作系统之前，程序可以使用全部的地址空间，因此*符号*的地址可以是固定的，不需要*加载器*。

但操作系统出现后，操作系统会甚至其他程序会占用一部分地址空间，因此程序的加载地址不是固定的，
这时就需要*加载器*在运行时实现*符号*和*地址*的绑定。

