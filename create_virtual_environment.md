## virtual environment for windows
说明：在进行虚拟环境安装之前，首先要确保自己的电脑上有安装相关版本的 python 解释器，并且可以使用 pip  命令。安装过程中需要连接到网络。

1、进入你想要创建python虚拟环境的目录下。我这里演示的是在D盘下新建了一个空的文件夹 project，进入 project 文件夹里面

2、使用 pip 工具安装 virtualenv 软件包：
```
pip install virtualenv
```

3、使用 virtualenv 命令创建一个名字为 Django 的新环境目录。我这里起的名为 Django，因为我要用python3做一个 django 项目
```
virtualenv --no-site-packages Django
```

4、查看新的 python 的文件目录结构，这个时候目录已经创建好了

5、在命令行下进入 Scripts 的目录下，进入虚拟环境。进入 Scripts 后输入 `activate` 回车即可完成虚拟环境的创建，完成之后看到路径的最前面有一个括号，括号里面是之前创建的目录名，就表示虚拟环境已经创建好了

6、在虚拟环境安装你要开发应用的第三方包，所有安装的第三方包都只能在这个虚拟环境中使用，在虚拟环境外是不能使用的

7、可以在虚拟环境中进行任何 python 相关的操作，并且不会对外部环境造成任何影响

8、操作完成之后，可以使用命令 deactivate 退出虚拟环境。

9、可以通过 `chdir` 命令来查看当前位置的绝对路径。

## virtual environment for ubuntu 16.04
### 安装虚拟环境的命令 :
```
sudo pip3 install virtualenv
sudo pip3 install virtualenvwrapper
```

安装完虚拟环境后，如果提示找不到mkvirtualenv命令，须配置环境变量：

- 1、创建目录用来存放虚拟环境
```
mkdir $HOME/.virtualenvs
```
- 2、打开~/.bashrc文件，并添加如下：
```
export WORKON_HOME=$HOME/.virtualenvs
source /usr/local/bin/virtualenvwrapper.sh
```
- 3、运行
```
source ~/.bashrc
```

### 创建虚拟环境的命令 :
提示：如果不指定python版本，默认安装的是python2的虚拟环境
在python2中，创建虚拟环境

mkvirtualenv 虚拟环境名称
例 ：
```
mkvirtualenv py_flask
```

在python3中，创建虚拟环境
```
mkvirtualenv -p python3 虚拟环境名称
```

## Ubuntu18.04 安装python虚拟环境

最近重新安装了Ubuntu虚拟机，由于要做项目开发，需要使用到不同的开发环境，所以考虑安装python虚拟环境。但是我按着之前的方法一通安装下去，发现各种不顺畅，于是就各种尝试，终于找到了最完美的解决方法。

请提前安装好 python 环境和 pip 包管理工具，本次安装 python 虚拟环境使用的是 python3(安装虚拟机就自动安装好了 python3.6) 和 pip3(需要手动安装)

#### 安装 virtualenv
```python
pip3 install virtualenv
```

#### 安装 virtualenvwrapper
```python
sudo pip3 install virtualenvwrapper
```

#### 设置配置项
```text
1、 创建目录用来存放虚拟环境：mkdir ~/.virtualenvs
2、 编辑 ~/.bashrc 文件：vim ~/.bashrc
3、 将下面配置添加到文件中：
    export WORKON_HOME=$HOME/.virtualenvs
    export PROJECT_HOME=$HOME/DEVEL
    export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3
    source /usr/local/bin/virtualenvwrapper.sh
```
- 如果此时提示：`bash: /usr/local/bin/virtualenvwrapper.sh: 没有那个文件或目录`
则将`source /usr/local/bin/virtualenvwrapper.sh`改为：`source $HOME/.local/bin/virtualenvwrapper.sh`
- 因为在我的Ubuntu系统中第一次将`virtualenvwrapper.sh`安装在了`/usr/local/bin/`目录下，第二次安装在了`$HOME/.local/bin/`目录下，所以根据自己的系统确定一下路径

#### 出现错误
如果此时执行 `source ~/.bashrc` 的话，是不会报错的，但是在执行创建虚拟环境的时候，如 `mkvirtualenv flask` ，就会提示异常：
```python
ERROR: virtualenvwrapper could not find virtualenv in your path
```
#### 问题所在
这是因为在当前版本的 ubuntu 系统中，virtualenv没有被安装到 `$HOME/.virtualenvs` 目录下，所以 virtualenvwrapper 找不到 virtualenv 命令

通过不断寻找，最后才找到了该命令被安装到了 `$PATH:~/.local/bin` 目录下，所以需要在配置文件中指定 virtualenv 命令的环境变量

#### 解决办法
重新打开 `~/.bashrc` 文件，在文件中添加如下内容：
```python
PATH=$PATH:~/.local/bin
```

再次执行
```python
source ~/.bashrc
```
没有报错

然后尝试创建虚拟环境：
```python
mkvirtualenv flask
```

没有任何提示，是不是说明已经创建好了呢？试一下就知道了，输入 `workon` 然后按两次 `table` ，出现了刚才创建的虚拟环境名字 `flask` ，进入虚拟环境成功

至此，所有创建 python 虚拟环境过程完成
例 ：
mkvirtualenv -p python3 py3_flask


进入虚拟环境

workon 虚拟环境名称

退出虚拟环境
deactivate

删除虚拟环境
rmvirtualenv 虚拟环境名称
