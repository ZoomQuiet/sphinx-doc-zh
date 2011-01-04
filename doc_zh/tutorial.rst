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

Now that you have added some files and content, let's make a first build of the
docs.  A build is started with the :program:`sphinx-build` program, called like
this::

   $ sphinx-build -b html sourcedir builddir

where *sourcedir* is the :term:`source directory`, and *builddir* is the
directory in which you want to place the built documentation.  The :option:`-b`
option selects a builder; in this example Sphinx will build HTML files.

|more| See :ref:`invocation` for all options that :program:`sphinx-build`
supports.

However, :program:`sphinx-quickstart` script creates a :file:`Makefile` and a
:file:`make.bat` which make life even easier for you:  with them you only need
to run ::

   $ make html

to build HTML docs in the build directory you chose.  Execute ``make`` without
an argument to see which targets are available.


Documenting objects
-------------------

One of Sphinx' main objectives is easy documentation of :dfn:`objects` (in a
very general sense) in any :dfn:`domain`.  A domain is a collection of object
types that belong together, complete with markup to create and reference
descriptions of these objects.

The most prominent domain is the Python domain.  To e.g. document the Python
built-in function ``enumerate()``, you would add this to one of your source
files::

   .. py:function:: enumerate(sequence[, start=0])

      Return an iterator that yields tuples of an index and an item of the
      *sequence*. (And so on.)

This is rendered like this:

.. py:function:: enumerate(sequence[, start=0])

   Return an iterator that yields tuples of an index and an item of the
   *sequence*. (And so on.)

The argument of the directive is the :dfn:`signature` of the object you
describe, the content is the documentation for it.  Multiple signatures can be
given, each in its own line.

The Python domain also happens to be the default domain, so you don't need to
prefix the markup with the domain name::

   .. function:: enumerate(sequence[, start=0])

      ...

does the same job if you keep the default setting for the default domain.

There are several more directives for documenting other types of Python objects,
for example :rst:dir:`py:class` or :rst:dir:`py:method`.  There is also a
cross-referencing :dfn:`role` for each of these object types.  This markup will
create a link to the documentation of ``enumerate()``::

   The :py:func:`enumerate` function can be used for ...

And here is the proof: A link to :func:`enumerate`.

Again, the ``py:`` can be left out if the Python domain is the default one.  It
doesn't matter which file contains the actual documentation for ``enumerate()``;
Sphinx will find it and create a link to it.

Each domain will have special rules for how the signatures can look like, and
make the formatted output look pretty, or add specific features like links to
parameter types, e.g. in the C/C++ domains.

|more| See :ref:`domains` for all the available domains and their
directives/roles.


Basic configuration
-------------------

Earlier we mentioned that the :file:`conf.py` file controls how Sphinx processes
your documents.  In that file, which is executed as a Python source file, you
assign configuration values.  For advanced users: since it is executed by
Sphinx, you can do non-trivial tasks in it, like extending :data:`sys.path` or
importing a module to find out the version your are documenting.

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

