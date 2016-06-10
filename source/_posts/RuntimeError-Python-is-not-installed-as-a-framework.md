---
title: Runtime Error Python is not installed as a framework.
date: 2016-06-06 00:44:42
categories:

tags: 
- Errors
- Python
---

# Python Virtulenv 安装matplotlib出错

今天在mac上配置python2.7的virtualenv，并且安装matplotlib，安装没有问题，但是出现如下报错。

``` 
Traceback (most recent call last):
  File "../test.py", line 2, in <module>
    import matplotlib.pyplot as plt
  File "/Users/wnz/Projects/datapython2/lib/python2.7/site-packages/matplotlib-1.5.2rc2+1932.g75a35ef-py2.7-macosx-10.11-x86_64.egg/matplotlib/pyplot.py", line 113, in <module>
    _backend_mod, new_figure_manager, draw_if_interactive, _show = pylab_setup()
  File "/Users/wnz/Projects/datapython2/lib/python2.7/site-packages/matplotlib-1.5.2rc2+1932.g75a35ef-py2.7-macosx-10.11-x86_64.egg/matplotlib/backends/__init__.py", line 55, in pylab_setup
    [backend_name], 0)
  File "/Users/wnz/Projects/datapython2/lib/python2.7/site-packages/matplotlib-1.5.2rc2+1932.g75a35ef-py2.7-macosx-10.11-x86_64.egg/matplotlib/backends/backend_macosx.py", line 19, in <module>
    from matplotlib.backends import _macosx
RuntimeError: Python is not installed as a framework. The Mac OS X backend will not be able to function correctly if Python is not installed as a framework. See the Python documentation for more information on installing Python as a framework on Mac OS X. Please either reinstall Python as a framework, or try one of the other backends. If you are Working with Matplotlib in a virtual enviroment see 'Working with Matplotlib in Virtual environments' in the Matplotlib FAQ 
```

# 解决方法
后来在 [官方网站] [matplotlib] 上找到了解决方法。主要意思是说matplotlib依赖于一些GUI的框架，因为需要渲染并且展示渲染的结果\[[2] [backend]\]。但是多数的GUI框架pip都没办法直接安装，因此部署安装的时候需要多一步操作。
    
    
原网页提供了一些workarouds，其中结尾提到的[virtualenv-pythonw-osx](https://github.com/gldnspud/virtualenv-pythonw-osx)，感觉更方便一些，但是github网页里没有写怎么安装，所以在这里记录一下。

1. 首先用brew安装Python，但是必须要加参数 --framework
    brew install python --framework
    
2. 然后
    git clone https://github.com/gldnspud/virtualenv-pythonw-osx.git

3. 切换到虚拟的python工作环境，可以用which看一下是否切换成功
    source /..virtualenvpath../bin/activate
    cd virtualenv-pythonw-osx
    python setup.py install
    
4. 虚拟python环境的bin/目录下会出现一个可执行文件fix-osx-virtualenv，然后执行
    fix-osx-virtualenv `which python`/../..

就可以了，然后试试看:)

[matplotlib]: http://matplotlib.org/faq/virtualenv_faq.html
[backend]: http://my.oschina.net/swuly302/blog/94915

# References:
1. [Working with Matplotlib in Virtual environments](http://matplotlib.org/faq/virtualenv_faq.html)
2. [matplotlib中什么是后端](http://my.oschina.net/swuly302/blog/94915)
3. [virtualenv-pythonw-osx](https://github.com/gldnspud/virtualenv-pythonw-osx)
