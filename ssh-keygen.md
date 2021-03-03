# ssh-keygen openSSH 认证钥匙工具

ssh-keygen负责生成、管理和转换认证钥匙。

生成钥匙对

ssh-keygen -t <加密算法> -C <注释>

*-t <加密算法类型>

指定加密算法类型，目前支持dsa、ecdsa、ecdsa-sk、ed25519-sk、rsa

*-C <注释>
给sshkey加注释，这个注释会加到生成的公key中。


