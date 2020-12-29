## 2.安装

### 2.1准备

> 安装之前假设你已经安装好了python3

- sphinx版本:3.4
- 以下以Linux命令为主,window可以手动创建目录,然后在cmd执行pip和初始化即可.

```shell
#安装sphinx/主题/markdown
pip install sphinx recommonmark sphinx_rtd_theme
#创建一个目录docs
mkdir docs
#切换至docs目录
cd docs
#初始化一个sphinx
sphinx-quickstart
```

在执行命令`sphinx-quickstart`的时候，会让你输入配置，除了以下几个个性化配置外，其他的都可以按照默认的来（回车默认配置）。
```shell
> Separate source and build directories (y/n) [n]:n
> Project name: how-to-use-sphinx
> Author name(s): jonnyan404
> Project release []: 0.1
> Project language [en]: zh_CN
```

执行完毕后，就可以看见创建的工程文件

- _build：文件夹，当你执行`make html`的时候，生成的html静态文件都存放在这里
- _static：文件夹：图片,js等存放地址
- _templates：文件夹:模板文件存放
- make.bat：bat脚本
- Makefile:编译文件
- index.rst:索引文件,文章目录大纲
- conf.py:配置文件

### 2.2编写文章

在docs目录下新建hello.rst,内容如下:

```rst
hello,world
=============
```
如果会markdown语法,无需学习rst语法,可参考文末语法转换网站.

`index.rst`修改如下:

```shell
.. toctree::
   :maxdepth: 2

   hello
```

然后在docs目录下执行 `make html`,进入 `_build/html` 目录后用浏览器打开 `index.html`

### 2.3更改主题和添加md支持

vim conf.py #更改如下配置:
```shell
html_theme = "sphinx_rtd_theme"
extensions = ['recommonmark']
```
然后再次运行 `make html` 即可.
关于markdown的用法形式与rst一样,直接更换后缀并在文件内已markdown语法写内容即可.

## 3.与GitHub联动

上传代码至GitHub仓库,然后去 <https://readthedocs.org/> 注册账号,并关联GitHub仓库.
然后需要在GitHub仓库根目录下,增加一个名称为 `.readthedocs.yml` 的配置文件:
```shell
# .readthedocs.yml
# Read the Docs configuration file
# See https://docs.readthedocs.io/en/stable/config-file/v2.html for details

# Required
version: 2

# Build documentation in the docs/ directory with Sphinx
sphinx:
  configuration: docs/conf.py

# Build documentation with MkDocs
#mkdocs:
#  configuration: mkdocs.yml

# Optionally build your docs in additional formats such as PDF
formats:
  - pdf

# Optionally set the version of Python and requirements required to build your docs
python:
  version: 3.7
  install:
    - requirements: docs/requirements.txt

```

再去 `docs` 目录下,新建一个名称为 `requirements.txt` 的文件,在这个文件内增加你所使用的包名称.
例如我的是:
```shell
sphinx
sphinx-rtd-theme
recommonmark
```
如果以上两个文件不添加,那么自动构建出来的文章,与你在本地的生成的会不一致,因为 readthedocs 网站默认使用mkdocs来构建.

## 4.后记

- [conf.py配置详解](https://www.sphinx-doc.org/zh_CN/latest/usage/configuration.html)
- [中文sphinx使用手册](https://zh-sphinx-doc.readthedocs.io/en/latest/markup/index.html)
- [语法转换网站](https://pandoc.org/try/)
