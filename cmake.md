# CMake使用锦囊

## 查找链接库
	find_library (<目标变量名> <库名> [<路径1> <路径2> ...])
	
## 链接库	
	target_link_libraries(<链接目标> [<项1> <项2> .....])
	<项>可以是源文件、静态库、动态库
	
## 添加整个目录的源文件
	aux_source_directory(<目录名> <变量名>)


	
	
