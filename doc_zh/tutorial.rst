.. highlight:: rst

Sphinx初尝
=======================

本文旨在给出一个教程样的概览,以便大家快速明了 Sphnix 如何使用,
点击绿色箭头的 "详细" 链接将进入对应操作的高级手册.



配置文档资源
------------------------------------

包含所有文档原始文本的目录称作: :term:`资源目录`.
此目录也包含 Sphnix 配置文件 :file:`conf.py`,
Sphnix 根据此文件的声明查阅和生成文档. [#]_


Sphnix 内置了一个脚本 :program:`sphinx-quickstart`
可以自动生成默认的 :file:`conf.py`, 只需调用之 ::

   $ sphinx-quickstart

并回答几个问题.  (注意,对 "autodoc" 回答 Yes.)


定义文档结构
---------------------------

假定已经用 :program:`sphinx-quickstart` 生成了 :term:`资源目录` 并包含了:file:`conf.py` 
以及主文档 :file:`index.rst` .
:term:`主控文档` 作为欢迎页,也包含了"内容树索引"(或 *toctree*).
这是 Sphnix 对reStructuredText 增加的主要特性之一: 快速在层次文档中关联多个文件.


.. sidebar:: reStructuredText 指令s

   ``toctree`` 是 reStructuredText :term:`指令`, 一种非常灵活的标记.
   指令可以包含参数/选项和内容.

   *Arguments* ~参数是紧跟在指令后,前缀两个冒号的名称.
   每个指令都可以附加一个或多个参数.

   *Options* ~ 选项在参数之后声明,使用 "字段列表" 格式.
   比如说 ``maxdepth`` 就是 ``toctree`` 的可选择项之一.

   *Content* 跟在选项之后,用一个空行引导.
   每个指令各自决定是否包含内容和怎么使用.

   指令的常见问题是
   **每行内容必须缩进到选项的同一层级**


toctree 指令起初是空的内容,类似::

   .. toctree::
      :maxdepth: 2

我们可以增补文档列表到 *内容* 区块 ::

   .. toctree::
      :maxdepth: 2

      intro
      tutorial
      ...

这样就可以精确的控制文档的内容树展示.
被包含的文档得使用 :term:`文档名`\ s 进行声明,
即,省去后綴名,并不用正斜线前导的相对路径.


|more| 参阅 :ref:`the toctree directive <toctree-directive>`.

现在可以创建 toctree 中列出的内容文件,并且他们的章节名也将就地逐层显示(高于"maxdepth"层次的章节),
同时,Sphnix 也理解包含文档的顺序.
(被包含的文件一樣可使用 ``toctree`` 指令)



追加内容
--------------

在Sphnix 源文件中,我们可以使用绝大多数 标准reStructuredText 的特性.
同时还有2 Sphnix 增补的一系列新功能.
例如,可以通过 :rst:role:`ref` 角色指令追加交叉引用(对所有输出都兼容).
当前的HTML输出版本文档中,就可以在侧栏通过 "Show Source" 链接查阅源文本;


|more| 参考 :ref:`rst-primer` 学习reStructuredText ,
以及 :ref:`sphinxmarkup` 查阅所有 Sphnix 增补的标记.


运行构建
-----------------

现在我们已添加了一些文件,就可以尝试进行首次文档编译了.
使用 :program:`sphinx-build` 脚本进行调用 ::

   $ sphinx-build -b html sourcedir builddir


*源目录*在 :term:`资源目录` ,*编译目录* 是我们指定的期望编译输出的目标目录.
:option:`-b` 选项可选择编译器; 当前实例Sphnix 将编译输出 HTML 文档. 


|more| 参考 :ref:`invocation` 可知所有 :program:`sphinx-build` 支持的选项.

其实 :program:`sphinx-quickstart` 脚本已经创建了 :file:`Makefile` 以及 :file:`make.bat` 
可以令我们更加简单的随时进行编译,只要 ::

   $ make html

将在我们指定的目录中完成HTML 渲染. [#make]_
如果执行 ``make`` 时没有跟任何选项,将看到相关说明. ::

    $ make
    Please use `make <target>' where <target> is one of
      html       to make standalone HTML files
      dirhtml    to make HTML files called index.html in directories
      singlehtml to make one big HTML file
      text       to make text files
      man        to make manual pages
      pickle     to make pickle files
      json       to make json files
      htmlhelp   to make HTML files and a HTML help project
      qthelp     to make Qt help files and project
      devhelp    to make Devhelp files and project
      epub       to make an epub file
      latex      to make LaTeX files, you can set PAPER=a4 or PAPER=letter
      latexpdf   to make LaTeX files and run pdflatex
      gettext    to make PO message catalogs
      changes    to make an overview over all changed/added/deprecated items
      linkcheck  to check all external links for integrity



文档对象
--------------------------------------

一个Sphnix 的通用文档 :dfn:`objects` 是 :dfn:`domain` (域).
一个域是通过标记来创建和定义的一批自定文档对象.

大多数域就是Python域.
比如说内部函式 ``enumerate()``, 我们可以直接应用到源文本中 ::

   .. py:function:: enumerate(sequence[, start=0])

      返回一个迭代对象,递归式处理字典结构的索引或是其它类似序列内容
      
呈现类似:

.. py:function:: enumerate(sequence[, start=0])

    返回一个迭代对象,递归式处理字典结构的索引或是其它类似序列内容

这一指令的参数 :dfn:`signature` ,是我们自行描述的文档内容,可以在行内给多个. [#signature]_

Python 域名是作为默认域来尝试的,所以,不必在函式标记前聲明 ::

   .. function:: enumerate(sequence[, start=0])

      ...

执行结果和之前一样.

另外还有一系列的Py对象类型的文档指令,
比如 :rst:dir:`py:class` 或是 :rst:dir:`py:method` .
也有类型对象都可用的交叉引用的 :dfn:`role` .
这类标记将创建一个文档链接给 ``enumerate()`` ::

   :py:func:`enumerate` 函式可用作...

这儿可以检验一下效果: :func:`enumerate`.

再次提示,这儿的 ``py:`` 可以忽略,效果一样.
我们不用关心真实的 ``enumerate()`` 文档在哪个文件中,
Sphnix 将找到它并正确链接上.

每个域,都是为某个特殊领域内容的良好输出,或是为参数什么的自动追加链接,比如说 C/C++ 域.

|more| 参考 :ref:`domains` 可知所有可用域以及指令/角色.


基本配置
-------------------

之前提及我们使用 :file:`conf.py` 脚本来控制 Sphinx 怎么处理文档.
实际上这是个标准的 Python 脚本,
对于高级用户:可以嵌入自个儿的特殊任务,比如: 变更 :data:`sys.path`,
或是导入另外的模块自动探察当前的文档版本.

配置项...
The config values that you probably want to change are already put into the
:file:`conf.py` by :program:`sphinx-quickstart` and initially commented out
(with standard Python syntax: a ``#`` comments the rest of the line).  To change
the default value, remove the hash sign and modify the value.  To customize a
config value that is not automatically added by :program:`sphinx-quickstart`,
just add an additional assignment.

Keep in mind that the file uses Python syntax for strings, numbers, lists and so
on.  The file is saved in UTF-8 by default, as indicated by the encoding
declaration in the first line.  If you use non-ASCII characters in any string
value, you need to use Python Unicode strings (like ``project = u'Exposé'``).

|more| See :ref:`build-config` for documentation of all available config values.


Autodoc
-------

When documenting Python code, it is common to put a lot of documentation in the
source files, in documentation strings.  Sphinx supports the inclusion of
docstrings from your modules with an :dfn:`extension` (an extension is a Python
module that provides additional features for Sphinx projects) called "autodoc".

In order to use autodoc, you need to activate it in :file:`conf.py` by putting
the string ``'sphinx.ext.autodoc'`` into the list assigned to the
:confval:`extensions` config value.  Then, you have a few additional directives
at your disposal.

For example, to document the function ``io.open()``, reading its
signature and docstring from the source file, you'd write this::

   .. autofunction:: io.open

You can also document whole classes or even modules automatically, using member
options for the auto directives, like ::

   .. automodule:: io
      :members:

autodoc needs to import your modules in order to extract the docstrings.
Therefore, you must add the appropriate path to :py:data:`sys.path` in your
:file:`conf.py`.

|more| See :mod:`sphinx.ext.autodoc` for the complete description of the
features of autodoc.


More topics to be covered
-------------------------

- Other extensions (math, intersphinx, viewcode, doctest)
- Static files
- Selecting a theme
- Templating
- Using extensions
- Writing extensions


.. include:: tutorial-footnote.rst

