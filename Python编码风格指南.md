# Python编码风格指南

## 代码布局

### 缩进

* 每级缩进使用4个空格。

* 无论什么情况下，都需要注意以下几点
  * 第一行没有参数并且使用更多的缩进来区别它本身和连续行。
    * 风格良好：

      ```python
      # 与分界符对齐
      foo = long_function_name(var_one,var_two,
                              var_three,var_four)
        # 包括更多的缩进以区分于其他的
        def long_function_name(
            var_one,var_two,var_three,
            var_four):
            print(var_one)
        # 悬挂缩进应增加一个级别
        foo = long_function_name(
            var_one,var_two,
        	var_three,var_four)
      ```
      
      
      
    * 风格不良：
    
        ```python
         # 第一行参数禁止不适用垂直对齐
            foo = long_function_name(var_one,var_two,
                var_three,var_four)
            # 当无法区分缩进时，需要进一步缩进
            def long_function_name(
                var_one,var_two,var_three,
                var_four):
                print(var_one)
        ```
    
    * 对于连续行，4个空格规则是可选的。
        可选的：
    
        ```python
        # 悬挂缩进可能缩进不是4个空格
        foo = long_function_name(
          var_one,var_two,
          var_three,var_four)
        ```
        
        
        
    * if语句条件块足够长时需要编写多行，值得注意的是两个字符组成的关键字（例如if），加上一个空格，加上开括号为多行条件的后续行创建一个4个空格的缩进。这可以给嵌入if内的缩进语句产生视觉冲突，这也自然被缩进4个空格。这个PEP没有明确如何（是否）进一步区分条件行和if语句内的嵌入行。这种情况下，可以接受的选项包括，但不仅限于：
    
        ```python
        # 没有额外的缩进
        if (this_is_one_thing and
            that_is_another_thing):
            do_something()
        # 添加一行注释，这将为编译器支持语法高亮提供一些区分
        if (this_is_one_thing and
            that_is_another_thing):
            # Since both conditons are true, we can frobnicate.
            do_something()
        # 在条件接续行，增加额为的缩进
        if (this_is_one_thing 
            	and that_is_another_thing):
            do_something()
        ```
    
        
    
    * 多行结构中的结束花括号/中括号/圆括号是最后一行的第一个非空白字符
    
        ```python
        my_list = [
            1,2,3,
            4,5,6
        ]
        result = some_function_that_takes_argument(
        	'a','b','c',
            'd','e','f',
        	)
        ```
    
        
    
    * 或者是最后一行的第一个字符
    
        ```python
        my_list = [
            1,2,3,
            4,5,6
        ]
        result = some_function_that_takes_argument(
        	'a','b','c',
            'd','e','f',
        )
        ```

### 制表符还是空格

* 空格是缩进方法的首选。
* 制表符仅用于与已经用制表符做缩进的代码保持一致。
* Python3不允许混用制表符和空格来缩进。
* Python2代码混用制表符和空格缩进，将被转化为只使用空格。
* 调用Python2命令行解释器时使用-t选项，可对代码中非法混用制表符和空格发出警告。当使用-tt选项，警告将变成错误。

### 行的最大长度

* 限制所有行最多79个字符。

* 下垂的长块结构限制为更少的文本（文档字符串或注释），行的长度应该限制在72个字符。

* 绝大多数工具的默认折叠会破坏代码的可视化结构，使其更难以理解。编辑器中的窗口宽度设置为80个字符。即使该工具将在最后一列中标记字形。一些基于网络的工具可能不会提供动态的自动换行。

* Python标准库采取保守做法，要求行限制到79个字符（文档字符串/注释到72个字符）。
    折叠长行的首选方法是在小括号，中括号，大括号中使用Python隐式换行。长行可以在表达式外面使用小括号来变成多行。连续行使用反斜杠更好。

* 反斜杠有时可能仍然是合适的。例如，长的多行的with语句不能用隐式续行，可以用反斜杠：

    ```python
    with open('/path/to/some/file/you/want/to/read') as file_1,\
    	 open('/path/to/some/file/being/written','w') as file_2:
    	file_2.write(file_1.read())
    ```

### 换行应该在二元操作符的前面还是后面

* 过去二十年我们都是推荐放在二元操作符的后面。但是这种做法会以两种方式伤害可读性：多个二元操作符在屏幕上不在一列，另外如果你想知道对一个被操作的对象做了什么操作，需要向上找一行。这导致你的眼睛不得不上下往返很多次才能搞清楚哪个数字是被加的，哪个数字是被减的：

    ```python
    # 不好的作法：操作符被操作的对象是分离的
    income = (gross_wages +
             taxable_interest + 
             (dividends - qualified_dividends) - 
             ira_deductico - 
             student_loan_interest)
    ```

    

* 为了解决可读性问题，数学家和印刷业者通常是在二元操作符之前换行的。Donald Knuth在他的《计算机与排版》系列文章中解释了这个传统规则：“虽然写在一段话中的公式经常在二元操作符的后面换行，但是单独展示的公式通常是在二元操作符的前面换行。”出于遵循数学传统，所以我们这样写这段代码将更加可读：

    ```python
    # 好的做法：很容易勘察二元操作符和被操作对象的关系
    income = (gross_wages 
    		 + taxable_interest 
              + (dividends - qualified_dividends) 
              - ira_deductico 
              - student_loan_interest)
    ```

### 空行

* 顶级函数和类的定义之间有两行空行。

* 类内部的函数定义之间有一行空行。

* 额外的空行用来（谨慎地）分离相关的功能组。相关的行（例如：一组虚拟实现）之间不使用空行。

* 在函数中谨慎地使用空行来表示逻辑部分。

* Python接受control-L（即^L）换页符作为空白符；许多工具把这些字符作为分页符，所以可以使用它们为文件中的相关部分分页。注意，一些编辑器和基于Web的代码查看器可能不能识别control-L是换页，将显示另外的字形。



### 源文件编码

* Python核心发布中的代码应该始终使用UTF-8（或Python2中用ASCII）。

* 文件使用ASCII（Python2中）或UTF-8（Python3中）不应有编码声明。

* 在标准库中，非默认编码仅用于测试目的或注释或文档字符串需要提及包含非ASCII字符的作者名；否则，使用\x，\u，\U，或\N是字符串中包含非ASCII数据的首先方式。

* Python3.0及以上版本，为标准库（参见PEP 3131）规定以下策略：Python标准库中的所有标识符必须使用ASCII标识符，在可行的地方使用英文单词（在很多例子中，使用非英文的缩写和专业术语）。另外，字符串和注释必须用ASCII。仅有的例外是（a）测试非ASCII的特点，（b）测试作者名。不是基于拉丁字母表的作者名必须提供一个他们名字的拉丁字母表的音译。

    

### 导入

* 导入通常是单独一行

    * 风格良好：

        ```python
        import os
        import sys
        ```

        

    * 风格不良：

        ```python
        import sys, os
        ```

        

    * 这样也是可以的：

        ```python
        from subprocess import Popen, PIPE
        ```

        

* 导入常常位于文件顶部，在模块注释和字符串文档之后，在模块的全局变量和常量之前。

* 导入应该按照以下顺序分组：
    * 标准库导入
    * 相关的第三方导入
    * 特定的本地应用/库导入
    * 在每个导入组之间放一行空行。

* 把任何相关__all__规范放在导入之后。

* 推荐绝对导入，因为它们更易读，并且如果导入系统配置的不正确（例如当包中的一个目录结束于sys.path）它们有更好的表现（至少给出更好的错误信息）：

    ```python
    import mypkg.sibling
    from mypkg import sibling
    from mypkg.sibling import example
    ```

    

* 明确的相对导入可以用来接受替代绝对导入，特别是处理复杂包布局时，绝对导入过于冗长。

    ```python
    from . import sibling
    from . sibling import example
    ```

    

* 标准库代码应该避免复杂包布局并使用绝对导入。

* 从一个包含类的模块中导入类时，通常下面这样是好的写法：

    ```python
    from myclass import myClass
    from foo.bar.yourclass import YourClass
    ```

* 如果这种写法导致本地名字冲突，那么就这样写：

    ```python
    import myclass
    import foo.bar.yourclass
    ```

    

* 并使用“myclass.MyClass”和“foo.bar.yourclass.YourClass”来访问。
* 避免使用通配符导入（from <模块名> import *），因为它们使哪些名字出现在命名空间变得不清楚，这混淆了读者和许多自动化工具。通配符导入有一种合理的使用情况，重新发布一个内部接口作为一个公共API的一部分（例如，重写一个纯Python实现的接口，该接口定义从一个可选的加速器模块并且哪些定义将被重写提前并不知道）



### 模块级别的内置属性

* 模块级别的内置属性（名字有前后双下划线的），例如__all__, __author__, __version__，应该放置在模块的文档字符串后，任意import语句之前，from __future__导入除外。Python强制要求from __future__导入必须在任何代码之前，只能在模块级文档字符串之后。

    ```python
    """
    This is the example module.
    This module does stuff.
    """
    
    from __future__ import barray_as_FLUFL
    
    __all__ = ['a', 'b', 'c']
    __version__ = '0.1'
    __author__ = 'Cardinal Biggles'
    
    import os
    import sys
    ```

    

### 字符串引号

* Python中，单引号字符串和双引号字符串是一样的。本PEP不建议如此。建议选择一条规则并坚持下去。当一个字符串包含单引号字符或双引号字符时，使用另一种字符串引号来避免字符串中使用反斜杠。这提高可读性。

* 三引号字符串，与PEP 257 文档字符串规范一致总是使用双引号字符。



### 表达式和语句中的空格

* 以下情况避免使用多余的空格：
    * 紧挨着小括号，中括号或大括号。

        ```python
        Yes: spam(ham[1], {eggs:2})
        No:  spam( ham[ 1 ], { eggs: 2 } )
        ```

        

    * 紧挨在逗号，分号或冒号前：

        ```python
        Yes: if x == 4: print x, y; x, y = y, x
        No:  if x == 4 : print x , y ; x , y = y , x
        ```

        

* 在切片中冒号像一个二元操作符，冒号两侧的有相等数量空格（把它看作最低优先级的操作符）。在一个扩展切片中，两个冒号必须有相等数量的空格。例外：当一个切片参数被省略时，该空格被省略。

    ```python
    Yes:
    
    ham[1:9], ham[1:9:3], ham[1::3],ham[1:9:]
    ham[lower:upper], ham[lower:upper:],ham[lower::step],
    ham[lower+offset : upper+offset]
    ham[:upper_fn(x) : step_fn(x), ham[:: step_fn(x)]]
    ham[lower + offset : upper + offset]
    
    No:
        
    ham[lower + offset:upper + offset]
    ham[1: 9], ham[1 :9], ham[1:9 :3]
    ham[lower : : upper]
    ham[ : upper]
    ```

    

![article4.png](https://qiniumedia.freelycode.com/1/0a1737170228433a97b0706b909c911e.png)

* 紧挨着左括号之前，函数调用的参数列表的开始处：

    ```python
    Yes: spam(1)
    No:  spam（1）
    ```

    

* 紧挨着索引或切片开始的左括号之前：

    ```python
    Yes: dct['key'] = lst[index]
    No:  dct ['key'] = lst [index]
    ```

    

* 为了与另外的赋值（或其它）操作符对齐，不止一个空格。

    ```python
    Yes:
    
    x = 1
    y = 2
    long_variable = 3
    
    No:
    x             = 1
    y             = 2
    long_variable = 3
    ```

* 始终避免行尾空白。因为它们通常不可见，容易导致困惑：如果\后面跟了一个空格，它就不是一个有效的续行符了。很多编辑器不保存行尾空白，CPython项目中也设置了commit前检查以拒绝行尾空白的存在。

* 始终在这些二元操作符的两边放置一个空格：赋值（= ），增强赋值（+= ，-= 等），比较（== ， < ， > ， != ， <> ， <= ， >= ，in ， not in ，is ，is not ），布尔（and ，or ，not ）。

* 如果使用了不同优先级的操作符，在低优先级操作符周围增加空格（一个或多个）。不要使用多于一个空格，二元运算符两侧空格数量相等。

    ```python
    Yes:
    
    i = i + 1
    submitted += 1
    x = x*2 - 1
    hypot2 = x*x + y*y
    c = (a+b) * (a-b)
    
    No:
    
    i=i+1
    submitted +=1
    x = x * 2 - 1
    hypot2 = x * x + y * y
    c = (a + b) * (a - b)
    ```

    

* 当=符号用于指示关键字参数或默认参数值时，它周围不要使用空格。

    ```python
    Yes:
        
    def complex(real, imag=0.0):
        return magic(r=real, i=imag)
    
    Yes:
        
    def complex(real, imag= 0.0):
        return magic(r = real , i = imag)
    ```

    

* 带注解的函数使用正常的冒号规则，并且在->两侧增加一个空格：

    ```python
    Yes:
    
    def munge(input: AnyStr): ...
    def munge() -> AnyStr: ...
    
    No:
    
    def munge(input:AnyStr): ...
    def munge()->AnyStr: ...
    ```

    

* 如果参数既有注释又有默认值，在等号两边增加一个空格（仅在既有注释又有默认值时才加这个空格）。

    ```python
    Yes:
    
    def munge(sep: AnyStr = None): ...
    def munge(input: AnyStr, sep: Anystr = None, limmit=1000): ...
    
    No:
    
    def munge(input:AnyStr=None): ...
    def munge(input: Anystr, limit): ...
    ```

    

* 不鼓励使用复合语句（同一行有多条语句）。\

    ```python
    # 好的做法
    if foo == 'blah':
        do_blah_thing()
    do_one()
    do_two()
    do_three()
    
    # 请不要：
    
    if foo == 'blah':do_blah_thing()
    do_one();do_two();do_three()
    ```

    

* 尽管有时if/for/while的同一行跟一小段代码，在一个多条子句的语句中不要如此。避免折叠长行！

    ```python
    # 最好不用：
    
    if foo == 'blah': do_blah_thing()
    for x in lst: total += x
    while t < 10: t = delay()
    
    # 绝对不要：
    
    if foo == 'blah': do_blah_thing()
    else: do_non_blah_thing()
    
    try: something()
    finally:cleanup()
    
    do_one(); do_two(); do_three(long, argument,
    						   list, like, this)
    						   
    if foo == 'blah': one(); two(); three()
    ```

    

### 什么时候使用尾部逗号

* 尾部逗号通常都是可选的，除了一些强制的场景，比如元组在只有一个元素的时候需要一个尾部逗号。为了代码更加清晰，元组只有一个元素时请务必用括号括起来（语法上没有强制要求）：

    ```python
    # 好的做法：
    FILES = ('stup.cfg',)
    
    # 技术还行，但是看起来很困惑：
    
    FILES = ('stup.cfg',)
    ```

    

* 当尾部逗号不是必须时，如果你用了版本控制系统那么它将很有用。当列表元素、参数、导入项未来可能不断增加时，留一个尾部逗号是一个很好的选择。通常的用法是（比如列表）每个元素独占一行，然后尾部都有逗号，在最后一个元素的下一行写闭标签。如果你的数据结构都是写在同一行的，就没有必要保留尾部逗号了。

    ```python
    # 好的做法
    
    FILES = [
        'setup.cfg',
        'tox.ini',
    ]
    initiialize(FILES,
        	    error=Ttue,
    		   )
    
    # 不好的做法
    
    FILES = ['setup.cfg', 'tox.ini',]
    initiialize(FILES,error=Ttue,)
    ```

    

### 注释

* 同代码相矛盾的注释比没有注释更差。当代码修改时，始终优先更新注释！

* 注释应该是完整的句子。如果注释是一个短语或句子，它的第一个单词的首字母应该大写，除非它是一个以小写字母开头的标识符（不更改标识符的情况下！）。

* 如果注释很短，末尾可以不加句号。注释块通常由一个或多个段落组成，这些段落由完整的句子组成，并且每个句子都应该以句号结尾。

* 在句尾的句号后边使用两个空格。

* 写英语注释时，遵循断词和空格。

* 非英语国家的Python程序员：请用英语书写注释，除非你120%的确定，所有看你代码的人都和你说一样的语言。



### 注释块

* 注释块通常适用于一些（或全部）紧跟其后的代码，并且那些代码应使用相同级别的缩进。注释块的每行以一个#和一个空格开始（除非注释里面的文本有缩进）。

* 注释块内的段落之间由仅包含#的行隔开。



### 行内注释

* 谨慎地使用行内注释。

* 行内注释就是注释和代码在同一行，它与代码之间至少用两个空格隔开。并且它以#和一个空格开始。

* 如果行内注释指出的是显而易见，那么它就是不必要的。 不要这样做：

    ```python
    x = x + 1  # Increment x
    ```

    

* 但有时，这样是有用的：

    ```python
    x = x + 1  # Compensate for border
    ```

    

### 文档字符串



* 编写好的文档字符串（即“代码”）约定在PEP 257中是永存的。

* 为所有公共模块，函数，类和方法书写文档字符串。对非公开的方法书写文档字符串是没有必要的，但应该写注释描述这个方法是做什么的。这些注释应该写在def行后面。
    PEP 257描述了好的文档字符串约定。最重要的是，多行文档字符串以一行"""结束，例如：

    ```python
    """Return a foobange
    
    Option plotz says to frobnicate the bizbaz first.
    """
    ```

    

* 对于只有一行的文档字符串，"""同一行上。



### 命名规范

* Python库的命名规范有点儿混乱，所以我们不会将他们变得完全一致——不过，这是目前推荐的命名标准。新模块和包（包括第三方框架）应该按这些标准书写，但对有不同的风格的已有库，保持内部一致性是首选。

### 根本原则

* 用户可见的API的公开部分的名称，应该遵循反映用法而不是实现的约定。

* 描述：命名风格
    * 下面的命名风格是最常见的：
        * b（单个小写字母）
        * B（单个大写字母）
        * 小写字符串
        * 带下划线的小写字符串
        * 大写字符串
        * 带下划线的大写字符串
        * 首字母大写的字符串（或CapWords，或驼峰命名法）
          * 注意：当CapWords中使用缩写，大写所有的缩写字母。因此HTTPServerError优于HttpServerError。
        * 混用大小写的字符串（与首字母大写字符串不同的是它以小写字母开头）
        * 带下划线的首字母大写字符串（令人厌恶的！）

* 另外，以下特殊形式，前导或后置下划线是公认的（一般可以与任何约定相结合）：
    * 单前导下划线:弱“内部使用”标志。例如 from M import *不会导入以下划线开头的对象。
    * 单后置下划线：按惯例使用避免与Python关键字冲突，例如。
       * Tkinter.Toplevel(master, class_='ClassName')

    * 双前导下划线：当命名类属性，调用时名称改编（类FooBar中，__boo变成 _FooBar__boo；见下文）。
    * 前导和后置都是双下划线：存在于用户控制的命名空间的“神奇”的对象或属性。

    

### 规定：命名约定

#### 避免采用的名字

* 不要使用字符‘l’（小写字母el），‘O’（大写字母oh）或‘I’（大写字母eye）作为单字符变量名。
* 在某些字体中，这些字符与数字1和0是没有区别的。当想使用‘l’时，用‘L’代替。

#### 包名和模块名

* 模块名应该短，所有的字母小写。可以在模块名中使用下划线来提高可读性。Python包名也应该短，所有的字母小写，不鼓励使用下划线。

* 当一个C或C++书写的扩展模块，伴随Python模块来提供了一个更高层次（例如更面向对象）的接口时，C/C++模块名有一个前导下划线（如_socket）。

#### 类名

* 类名通常使用首字母大写字符串的规则。

* 函数的命名规则 主要用来可调用的。

* 在接口被记录并且主要用作调用的情况下，用函数的命名规则来代替类名的命名规则。

* 注意内置名有一个单独的规则：大多数的内置名是一个单词（或两个单词一起），首字母大写字符串的规则仅用于异常名和内置常量。

#### 类型变量名称

* 类型变量名称应该首字母大写，并且尽量短，比如：T, AnyStr, Num。对于协变量和有协变行为的变量，建议添加后缀__co或者__contra。

    ```python
    for typing import TypeVar
    
    VT_co = TypeVar('VT_co', covariant=True)
    KT_contra = TypeVar('KT_contra', contravariant=True)
    ```

#### 异常名

* 因为异常应该是类，所以类的命名规则在这里也同样适用。然而，异常名（如果这个异常确实是一个错误）应该使用后缀“Error”。

#### 全局变量名

* （希望这些变量是在一个模块内使用。）这些规则和那些有关函数的规则是相同的。

* 模块设计为通过from M import *来使用，应使用__all__机制防止导出全局变量，或使用加前缀的旧规则，为全局变量加下划线（可能你像表明这些全局变量是“非公开模块”）。

#### 函数名

* 函数名应该是小写字母，必要时单词用下划线分开以提高可读性。

* 混合大小写仅用于这种风格已经占主导地位的上下文（例如threading.py），以保持向后兼容性。



#### 函数和方法参数



* 使用self做实例化方法的第一个参数。

* 使用cls做类方法的第一个参数。

* 如果函数的参数名与保留关键字冲突，最好是为参数名添加一个后置下划线而不是使用缩写或拼写错误。

* 因此class_ 比clss好。（也许使用同义词来避免更好。）。



#### 方法名和实例变量

* 采用函数命名规则：小写字母，必要时单词用下划线分开以提高可读性。

* 仅为非公开的方法和实例变量使用一个前导下划线。

* 为了避免和子类命名冲突，使用两个前导下划线调用Python的名称改编规则。

* Python用类名改编这些名字：如果类Foo有一个属性名为__a，通过Foo.__a不能访问。（可以通过调用Foo._Foo__a来访问。）通常，两个前导下划线仅用来避免与子类的属性名冲突。
    * 注意：关于__names的使用存在一些争论（见下文）。



#### 常量

* 常量通常定义于模块级别并且所有的字母都是大写，单词用下划线分开。例如MAX_OVERFLOW和TOTAL。

#### 继承的设计

* 确定类的方法和实例变量（统称为：“属性”）是否公开。如果有疑问，选择非公开；之后把其变成公开比把一个公开属性改成非公开要容易。

* 公开属性是那些你期望与你的类不相关的客户使用的，根据你的承诺来避免向后不兼容的变更。非公开属性是那些不打算被第三方使用的；你不保证非公开属性不会改变甚至被删除。

* 非公共属性是那些不打算被第三方使用的，你不能保证非公开的属性不会改变甚至被删除。

* 此处没有使用术语“private”，因为Python中没有真正私有的属性（没有通常的不必要的工作）。

* 属性的另一个类别是“API子集”的一部分（在其它语言常被称为“protected”）。某些类被设计为基类，要么扩展，要么修改某些方面的类的行为。在设计这样的类的时候，要注意明确哪些属性是公开的，哪些是API子类的一部分，哪些是真正只在你的基类中使用。

* 清楚这些之后，这是Python特色的指南：
    * 公开属性没有前导下划线。
    * 如果公开属性名和保留关键字冲突，给属性名添加一个后置下划线。这比缩写或错误拼写更可取。（然而，尽管有这样的规定，对于任何类的变量或参数，特别是类方法的第一个参数，‘cls’是首选的拼写方式）
        * 注1：参见上面对类方法的参数名的建议。
    * 对于简单的公开数据属性，最好只暴露属性名，没有复杂的访问器/修改器方法。记住，Python为未来增强提供了一条简单的途径，你应该发现简单的数据属性需要增加功能行为。在这种情况下，使用属性来隐藏简单数据属性访问语法后面的功能实现。
        * 注1：特性仅工作于新风格的类。
        * 注2：尽量保持功能行为无副作用，尽管副作用如缓存通常是好的。
        * 注3：计算开销较大的操作避免使用特性，属性注解使调用者相信访问（相对）是廉价的。
    * 如果确定你的类会被子类化，并有不想子类使用的属性，考虑用两个前导下划线无后置下划线来命名它们。这将调用Python的名称改编算法，类名将被改编为属性名。当子类不无意间包括相同的属性名时，这有助于帮助避免属性名冲突。
        * 注1：注意改编名称仅用于简单类名，如果一个子类使用相同的类名和属性名，仍然会有名字冲突。
        * 注2：名称改编会带来一定的不便，如调试和__getattr__()。然而，名称改编算法有良好的文档，也容易手工执行。
        * 注3：不是每个人都喜欢名称改编。尝试平衡避免意外的名称冲突和高级调用者的可能。



#### 公共和内部接口

* 任何向后兼容性保证只适用于公共接口。因此，重要的是用户能够清楚地区分公开和内部接口。

* 文档接口被认为是公开的，除非文档明确声明他们是临时或内部接口，免除通常的向后兼容保证。所有非文档化的接口应假定为内部接口。

* 为了更好的支持自省，模块应该使用__all__属性显示声明他们公开API的名字， __all__设置为一个空列表表示该模块没有公开API。
* 即使__all__设置的适当，内部接口（包，模块，类，函数，属性或者其它名字）仍应以一个前导下划线作前缀。

* 一个接口被认为是内部接口，如果它包含任何命名空间（包，模块，或类）被认为是内部的。

* 导入名被认为是实现细节。其它模块必须不依赖间接访问这个导入名，除非他们是一个明确的记录包含模块的API的一部分，例如os.path或包的__init__模块，从子模块暴露功能。

#### 程序设计建议

* 编写的代码应该不损害其他方式的Python实现（PyPy，Jython，IronPython，Cython，Psyco等等）。
    * 例如，不要依赖CPython的高效实现字符串连接的语句形式 += b或a = a + b。这种优化即使在CPython里也是脆弱的（它只适用于某些类型），并且在不使用引用计数的实现中它完全不存在。在库的性能易受影响的部分，应使用''.join()形式。这将确保跨越不同实现的连接发生在线性时间。

* 与单值比如None比较使用is 或is not ，不要用等号操作符。

* 同样，如果你真正的意思是if x is not None，谨防编写if x。例如，当测试一个默认是None的变量或参数是否被置成其它的值时。这个其它值可能是在布尔上下文为假的类型（例如容器）。

* 使用is not 操作符而不是not...is。虽然这两个表达式的功能相同，前者更具有可读性并且更优。

    ```python
    Yes:
    
    if foo is not None:
    
    No:
    
    if not foo is None:
    ```

* 当实现有丰富的比较的排序操作时，最好实现所有六个操作符（__eq__，__ne__，__lt__，__le__，__gt__，__ge__）而不是依靠其它代码只能进行一个特定的比较。

* 为了减少所涉及的工作量，functools.total_ordering()装饰器提供了一个工具来生成缺失的比较函数。

* PEP 207表明，Python假定自反性规则。因此，编译器可以交换y > x和x < y，y >= x和x <= y，也可以交换参数x == y和x != y。sort()和min()操作保证使用< 操作符并且max()功能使用> 操作符。不管怎样，最好实现所有六个操作，这样在其它上下文就不会产生混淆了。

* 使用def语句而不是使用赋值语句将lambda表达式绑定到标识符上。

    ```python
    Yes:
    
    def f(x):return 2*x
    
    No:
    
    f = lambda x: 2*x
    ```



* 第一种形式意味着所得的函数对象的名称是‘f’而不是一般的‘<lambda>’。这在回溯和字符串表示中更有用。赋值语句的使用消除了lambda表达式可以提供显示def声明的唯一好处（例如它可以嵌在更大的表达式里面）。

* 从Exception而不是BaseException中派生出异常。直接继承BaseException是保留那些捕捉几乎总是错的异常的。

* 设计异常层次结构基于区别，代码可能需要捕获异常，而不是捕获产生异常的位置。旨在以编程方式回答问题“出了什么问题？”，而不是只说“问题产生了”（参见PEP 3151对这节课学习内置异常层次结构的一个例子）

* 类的命名规则适用于此，只是当异常确实是错误的时候，需要在异常类名添加“Error”后缀。用于非本地的流控制或其他形式的信号的非错误的异常，不需要特殊的后缀。

* 适当使用异常链。Python3中，“raise X from Y”用来表明明确的更换而不失去原来追踪到的信息。

* 当故意替换一个内部异常（Python 2中使用“raise X”而Python 3.3+中使用“raise X from None”），确保相关的细节被转移到新的异常中（比如当转换KeyError为AttributeError时保留属性名，或在新的异常消息中嵌入原始异常的文本）。

* Python 3中产生异常，使用raise ValueError('message')替换老的形式raise ValueError,'message'。

* 后一种形式是不合法的Python 3语法。

* 目前使用的形式意味着当异常的参数很长或包含格式化字符传时，多亏了小括号不必再使用续行符。

* 捕获异常时，尽可能提及特定的异常，而不是使用空的except：子句。
    例如，使用：

    ```python
    try:
    	import platfrom_specific_module
    except ImportError:
    	platfrom_specific_module = None
    ```

* 空的except：子句将捕获SystemExit和KeyboardInterrupt异常，这使得很难用Control-C来中断程序，也会掩饰其它的问题。如果想捕获会导致程序错误的所有异常，使用except * * Exception:（空异常相当于except BaseException:）
    * 一条好的经验法则是限制使用空‘except’子句的两种情况：
           * 如果异常处理程序将打印或记录跟踪；至少用户将会意识到有错误发生。
           * 如果代码需要做一些清理工作，但是随后让异常用raise抛出。处理这种情况用try...finally更好。

* 当用一个名字绑定捕获异常时，更喜欢Python2.6中添加的明确的名称绑定语法。

    ```python
    try:
    	process_data()
    except Exception as exc:
    	raise DataProcessingFailedError(str(exc))
    ```

* 这是Python3中唯一支持的语法，并避免与旧的基于逗号的语法有关的歧义问题。

* 捕获操作系统异常时，更喜欢Python 3.3引进的明确的异常层次，通过errno值自省。

* 另外，对于所有的try/except子句，限制try子句到必须的绝对最少代码量。这避免掩盖错误。

    ```python
    Yes:
    try:
    	value = collection[key]
    except KeyError:
    	return key_not_found(key)
    else:
    	return handle_calue(value)
    
    No:
    
    try:
    	# Too broad!
    	return handle_value(collection[key])
    except KeyError:
    	# will also catch KetError raised by handle_value()
    	return key_not_founf(key)
    ```

    

* 当一个资源是一个局部特定的代码段，它使用后用with语句确保迅速可靠的将它清理掉。也可以使用try/finally语句。

* 无论何时做了除了获取或释放资源的一些操作，应该通过单独的函数或方法调用上下文管理器。例如：

    ```python
    Yes:
     with conm.begin_transaction():
     	do_stuff_in_rtansaction(conn)
     	
    No:
    
    with comn:
    	do_stuff_in_rtansaction(conn)
    ```

* 后者的例子没有提供任何信息表明__enter__和__exit__方法做了什么除了事务结束后关闭连接。 在这种情况下，明确是很重要的。

* 返回语句保持一致。函数中的所有返回语句都有返回值，或都没有返回值。如果任意一个返回语句有返回值，那么任意没有返回值的返回语句应该明确指出return None，并且明确返回语句应该放在函数结尾（如果可以）。

* ```python
    Yes:
    
    def foo(x):
        if x >= 0;
        	return math.sqrt(x)
        else:
            return None
        
    def bar(x):
        if x < 0:
            return None
        return math.sqrt(x)
    
    No:
        
    def foo(x):
        if x >= 0;
        	return math.sqrt(x)
        
    def bar(x):
        if x < 0:
            return
        return math.sqrt(x)
    ```

    

* 使用字符串方法代替string模块。

* 字符串方法总是更快并且与unicode字符串使用相同的API。如果必须向后兼容Python2.0以前的版本，无视这个原则。
* 使用“.startswith() ”和“.endswith()”代替字符串切片来检查前缀和后缀。

* startswith()和endswith()更清晰，并且减少错误率。例如：

    ```python
    Yes: if foo.startwith('bar'):
    No:  if type(obj) is type(1):
    ```

    

* 对象类型的比较使用isinstance()代替直接比较类型。

    ```python
    Yes: if isinstance(obj, int):
    No:  if type(obj) is type(1):
    ```

    

* 当检查一个对象是否是字符串时，牢记它也可能是一个unicode字符串！Python 2中，str和unicode有共同的基类basestring，所以你可以这么做：

    ```python
    if isinstance(obj, basestring):
    ```

    

* 注意，Python3中， unicode和basestring不再存在（只有str），并且字节对象不再是string（而是一个integers序列）

* 对于序列（字符串，列表，元组），利用空序列是false的事实。

    ```python
    Yes: if not seq:
    	 if seq:
    	
    No: if len(seq):
    	if not len(seq):
    ```

* 不要书写依赖后置空格的字符串。这些后置空格在视觉上无法区分，并且有些编辑器（或最近，reindent.py）将去掉他们。

* 不要用==来将布尔值与True或False进行比较。

    ```python
    Yes:   if greeting:
    No:	   if greeting == True:
    worse: if greeting is True:
    ```

    

* Python标准库不使用函数注解，由于它将给一个特定的注释风格造成过早的承诺。相反，注释是留给用户去发现和试验的有用的注释样式。

* 建议第三方实验注释使用一个相关的修饰符表明解释器如果解释注解来试验注解。

* 早期的核心开发人员尝试使用显示不一致的函数注解，特别的注释风格。例如：[str]是模糊的，它是代表一个字符串列表还是一个可以是str或None的值。

* 符号open（file:(str,bytes))被用于值是 bytes或str替代包含一个str紧跟一个bytes值的二元元组。

* seek(whence:int)注解展示出了一个规定外和规范内的混合：int限制太多（任何与__index__将被允许），它还不够严格（只有值0，1，和2是允许的）。同样的，write(b:bytes)注解也有太多限制（任何支持缓冲协议的将被允许）。

* 有些注解如read1(n:int=None)是自相矛盾的因为None不是一个int值。有些注解如assource_path(self,fullname:str) -> object，令人困惑它的返回类型是什么。

* 除了以上的，注解在具体类型和抽象类型的使用上是不一致的：int与Integral相对，set/frozenset与MutableSet/Set相对。
* 抽象基类的一些注解是不正确的规范。例如，set-to-set操作需要Other是另一个Set的实例而不是一个Iterable。

* 另一个问题是注解成为规范的一部分，但它没有被测试。

* 在大多数情况下，文档字符串已经包含了类型规范，并且比函数注解更清晰。在其余的情况下，一旦注解被移除文档字符串将改进。
* 所见到的函数注解太特别而且与一个自动类型检查或参数验证的连贯系统不一致。在代码中留下这些注解将使它以后更难做出改变以便自动化工具支持。