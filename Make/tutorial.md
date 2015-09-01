#Linux下make指令

- configure是一个shell脚本，一般用来生成Makefile，为下一步的编译做准备，在configure后加上参数来对安装进项控制。例如./configure --prefix=/usr 即将软件安装在/usr下面

- make，即编译，大多数的源代码包都要经过编译。如果make过程出现error，仔细研究错误代码

- make install，用这条命令进行安装。