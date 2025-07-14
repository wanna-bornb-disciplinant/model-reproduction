[1] ```__init__.py```文件在Python中的作用是将目录标记成一个“包”，可以通过```import```导入其中的模块或子包

[2] ```__init__.py```只负责当前目录中的行为，如果希望子文件夹也能被调用，需要在子文件夹同样添加```__init__.py```    
类似下面的结构：  
```
project/
├── __init__.py
├── module1.py
└── subpackage/
    ├── __init__.py
    └── module2.py
```

[3] 从Python3.3开始，可以不写```__init__.py```同样能导入模块，但为了兼容性(兼容低版本Python)、明确性(明确部分代码是包)；另外，```__init__.py```最大的一个作用是内部的代码会被执行，因此可以设置变量、加载配置(“Initializing package...”)等,还可以在```__init__.py```里面定义公共接口，例如一个文件中有多个函数和类，可以在```__init__.py```中定义import的部分，使得调用时只能访问具体函数，而无法访问整个文件，例如：
```python
from .module1 import func1
from .module2 import func2

__all__  = ["func1","func2"]
```
      
      
