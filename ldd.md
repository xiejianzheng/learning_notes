# ldd 使用说明

ldd 是 load dependencies的缩写

格式是：
	ldd [选项] ... 文件 ....

ldd的作用是打印所依赖的动态对象被需要可执行程序或共享对象在命令行上指定。

ldd还会打印出依赖对象的加载地址。

在通常情况下，ldd调用标准动态链接器(ld.so)。这会导致动态链接器会检查程序的
动态依赖并查找加载对象那些满足那些依赖。

对每个依赖，ldd会显示匹配对象的地址还有16进制的加载地址。

如：

$ ldd /bin/ls
	linux-vdso.so.1 (0x00007ffcc3563000)
	libselinux.so.1 => /lib64/libselinux.so.1 (0x00007f87e5459000)
	libcap.so.2 => /lib64/libcap.so.2 (0x00007f87e5254000)
	libc.so.6 => /lib64/libc.so.6 (0x00007f87e4e92000)
	libpcre.so.1 => /lib64/libpcre.so.1 (0x00007f87e4c22000)
	libdl.so.2 => /lib64/libdl.so.2 (0x00007f87e4a1e000)
	/lib64/ld-linux-x86-64.so.2 (0x00005574bf12e000)
	libattr.so.1 => /lib64/libattr.so.1 (0x00007f87e4817000)
	libpthread.so.0 => /lib64/libpthread.so.0 (0x00007f87e45fa000)



