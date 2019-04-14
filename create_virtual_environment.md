### virtual environment for windows
说明：在进行虚拟环境安装之前，首先要确保自己的电脑上有安装相关版本的python解释器，并且可以使用pip 命令。安装过程中需要连接到网络。

1、进入你想要创建python虚拟环境的目录下。我这里演示的是在D盘下新建了一个空的文件夹project，进入project文件夹里面

2、使用pip工具安装virtualenv软件包：
pip install virtualenv

3、使用virtualenv命令创建一个名字为 Django 的新环境目录。我这里起的名为 Django，因为我要用python3做一个 django 项目
virtualenv --no-site-packages Django

4、查看新的python的文件目录结构，这个时候目录已经创建好了

5、在命令行下进入Scripts的目录下，进入虚拟环境。进入Scripts后输入 activate 回车即可完成虚拟环境的创建，完成之后看到路径的最前面有一个括号，括号里面是之前创建的目录名，就表示虚拟环境已经创建好了

6、在虚拟环境安装你要开发应用的第三方包，所有安装的第三方包都只能在这个虚拟环境中使用，在虚拟环境外是不能使用的

7、可以在虚拟环境中进行任何python相关的操作，并且不会对外部环境造成任何影响

8、操作完成之后，可以使用命令deactivate退出虚拟环境。

9、可以通过chdir 命令来查看当前位置的绝对路径。

### virtual environment for ubuntu
安装虚拟环境的命令 :

sudo pip3 install virtualenv
sudo pip3 install virtualenvwrapper


安装完虚拟环境后，如果提示找不到mkvirtualenv命令，须配置环境变量：

1、创建目录用来存放虚拟环境
mkdir $HOME/.virtualenvs

2、打开~/.bashrc文件，并添加如下：
export WORKON_HOME=$HOME/.virtualenvs
source /usr/local/bin/virtualenvwrapper.sh

3、运行
source ~/.bashrc


创建虚拟环境的命令 :
提示：如果不指定python版本，默认安装的是python2的虚拟环境
在python2中，创建虚拟环境

mkvirtualenv 虚拟环境名称
例 ：
mkvirtualenv py_flask


在python3中，创建虚拟环境

mkvirtualenv -p python3 虚拟环境名称
例 ：
mkvirtualenv -p python3 py3_flask


进入虚拟环境

workon 虚拟环境名称

退出虚拟环境
deactivate

删除虚拟环境
rmvirtualenv 虚拟环境名称
