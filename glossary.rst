.. _glossary:

词汇表
========

.. glossary::

   builder
      A class (inheriting from :class:`~sphinx.builders.Builder`) that takes
      parsed documents and performs an action on them.  Normally, builders
      translate the documents to an output format, but it is also possible to
      use the builder builders that e.g. check for broken links in the
      documentation, or build coverage information.

      See :ref:`builders` for an overview over Sphinx' built-in builders.

   configuration directory
      The directory containing :file:`conf.py`.  By default, this is the same as
      the :term:`source directory`, but can be set differently with the **-c**
      command-line option.

   directive
      A reStructuredText markup element that allows marking a block of content
      with special meaning.  Directives are supplied not only by docutils, but
      Sphinx and custom extensions can add their own.  The basic directive
      syntax looks like this::

         .. directivename:: argument ...
            :option: value

            Content of the directive.

      See :ref:`directives` for more information.

   指令
      reStructuredText 标记元素,赋予标记块内容特殊含义.
      指令不算 docutils 的特技,只是Sphnix 自行进行了扩展.
      基础指令看起来象这样 ::

         .. directivename:: 参数 ...
            :option: 值

            指令内容.

      参考 :ref:`directives` .

   document name
      Since reST source files can have different extensions (some people like
      ``.txt``, some like ``.rst`` -- the extension can be configured with
      :confval:`source_suffix`) and different OSes have different path separators,
      Sphinx abstracts them: :dfn:`document names` are always relative to the
      :term:`source directory`, the extension is stripped, and path separators
      are converted to slashes.  All values, parameters and such referring to
      "documents" expect such document names.

      Examples for document names are ``index``, ``library/zipfile``, or
      ``reference/datamodel/types``.  Note that there is no leading or trailing
      slash.

   文档名
      因为 rST 文件可以使用不同的后缀
      (有人喜欢 ``.txt`` , 俺就愛 ``.rst`` -- 这可以在配置文件中定义 :confval:`source_suffix` )
      而且不同的操作系统也有不同的路径指引要求,
      Sphnix 使用相对于 term:`资源目录` 的:dfn:`document names` 来统一这些问题,
      后綴可忽略,路径使用正斜线分隔,例如:
        - ``index``
        - ``library/zipfile``
        - ``reference/datamodel/types``
      注意: 不能前导正斜线!

   domain
      A domain is a collection of markup (reStructuredText :term:`directive`\ s
      and :term:`role`\ s) to describe and link to :term:`object`\ s belonging
      together, e.g. elements of a programming language.  Directive and role
      names in a domain have names like ``domain:name``, e.g. ``py:function``.

      Having domains means that there are no naming problems when one set of
      documentation wants to refer to e.g. C++ and Python classes.  It also
      means that extensions that support the documentation of whole new
      languages are much easier to write.  For more information about domains,
      see the chapter :ref:`domains`.

   environment
      A structure where information about all documents under the root is saved,
      and used for cross-referencing.  The environment is pickled after the
      parsing stage, so that successive runs only need to read and parse new and
      changed documents.

   master document
      The document that contains the root :rst:dir:`toctree` directive.

   主控文档
      此文档包含根文档,以及 :rst:dir:`toctree` 指令.

   object
      The basic building block of Sphinx documentation.  Every "object
      directive" (e.g. :rst:dir:`function` or :rst:dir:`object`) creates such a block;
      and most objects can be cross-referenced to.

   role
      A reStructuredText markup element that allows marking a piece of text.
      Like directives, roles are extensible.  The basic syntax looks like this:
      ``:rolename:`content```.  See :ref:`inlinemarkup` for details.

   角色
      reStructuredText 标记元素,可以标记一段文本.
      如同指令,角色是可扩展的.
      基本语法类似:
      ``:rolename:`content```.  参考 :ref:`inlinemarkup` .

   source directory
      The directory which, including its subdirectories, contains all source
      files for one Sphinx project.

   资源目录
      此目录及子目录应该包含所有 Sphnix 工程需要的文件.
      (即:source directory)

   Zoom.Quiet
      男，纯种Pythoner，自由软件原教旨主义者:      
        - 中文Python用户组(CPyUG)创始人,管理员之一/哲思自由软件社区核心成员/Erlang中国用户组(ECUG)宣传部长/教育大发现社区(sociallearnlab.org)高级顾问。致力于软件过程改进的工作；以及中国自由软件社区发展；关注社会化教育及知识管理；喜爱SF和摄影。
        - 工作信仰：过程改进乃是催生可促生靠谱的人的组织！
        - 技术信仰：Simple is better！
        - 尝试使用Pythonic体验感化国人主动进入自由软件世界体验/学习/再创作。
        - 个人网站: `zoomquiet.org <http://zoomquiet.org>`_



