# CentOS 7下安装Python3.5

## 安装python3.6可能使用的依赖
```python
yum install openssl-devel bzip2-devel expat-devel gdbm-devel readline-devel sqlite-devel
```
 

## 到python官网找到下载路径, 用wget下载
```python
wget https://www.python.org/ftp/python/3.6.4/Python-3.6.4.tgz
```
## 解压tgz包
```python
tar -zxvf Python-3.6.4.tgz
```
## 把python移到/usr/local下面
```python
mv Python-3.6.4 /usr/local
```
## 删除旧版本的python依赖
```python
ll /usr/bin | grep python

rm -rf /usr/bin/python
```
## 进入python目录
```python
cd /usr/local/Python-3.6.4/
```
## 配置
```python
./configure
```
## 编译 make
```python
make
```
## 编译，安装
```python
make install
```
## 删除旧的软链接，创建新的软链接到最新的python
```python
rm -rf /usr/bin/python  # 可以不用删除，当前系统中已经没有python的链接了

ln -s /usr/local/bin/python3.6 /usr/bin/python
# 这一步完成之后，使用 python 打开的是 python3，原来的 python2 可以使用 python2 打开
```
```python
python -V
```
