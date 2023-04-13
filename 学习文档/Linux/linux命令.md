Yum (centos) 

-  列出所有可更新的软件清单命令：**yum check-update**
-  更新所有软件命令：**yum update**
-  仅安装指定的软件命令：**yum install <package_name>**
-  仅更新指定的软件命令：**yum update <package_name>**
-  列出所有可安裝的软件清单命令：**yum list**
-  删除软件包命令：**yum remove <package_name>**
-  查找软件包命令：**yum search     <keyword>**



apt (ubuton)



# Linux export 命令用于设置或显示环境变量。



```shell
export [-fnp][变量名称]=[变量设置值]
```

- -f 　代表[变量名称]中为函数名称。
- -n 　删除指定的变量。变量实际上并未删除，只是不会输出到后续指令的执行环境中。
- -p 　列出所有的shell赋予程序的环境变量。

 # 添加用户

useradd

- -c<备注> 　加上备注文字。备注文字会保存在passwd的备注栏位中。
- -d<登入目录> 　指定用户登入时的起始目录。
- -D 　变更预设值．
- -e<有效期限> 　指定帐号的有效期限。
- -f<缓冲天数> 　指定在密码过期后多少天即关闭该帐号。
- -g<群组> 　指定用户所属的群组。
- -G<群组> 　指定用户所属的附加群组。
- -m 　自动建立用户的登入目录。
- -M 　不要自动建立用户的登入目录。
- -n 　取消建立以用户名称为名的群组．
- -r 　建立系统帐号。
- -s<shell>　 　指定用户登入后所使用的shell。
- -u<uid> 　指定用户ID。

