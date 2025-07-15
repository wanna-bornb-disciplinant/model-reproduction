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

[4] Multi30K数据集来源：基于Flickr30K图像描述，包含英文-德文-法文多语言平行文本;主要用途：机器翻译、多模态学习;常用任务：英→德、英→法 翻译
标准的数据格式为：
```
multi30k/
├── train.en
├── train.de
├── val.en
├── val.de
├── test_2016_flickr.en
├── test_2016_flickr.de
├── ...

```
数据维度为：

| 文件                    | 每行内容  | 行数（样本数）    | 每行长度         |
| --------------------- | ----- | ---------- | ------------ |
| `train.en`            | 英语句子  | **29,000** | 不定，平均 13 个单词 |
| `train.de`            | 德语句子  | **29,000** | 不定，平均 12 个单词 |
| `val.en`              | 验证英语句 | **1,014**  | 同上           |
| `val.de`              | 验证德语句 | **1,014**  | 同上           |
| `test_2016_flickr.en` | 测试英语句 | **1,000**  | 同上           |
| `test_2016_flickr.de` | 测试德语句 | **1,000**  | 同上           |

处理后的数据维度应该是(32是batch_size,50是max_len)：

| 名称           | 形状              | 含义                              |
| ------------ | --------------- | ------------------------------- |
| `src`        | (32, 50)        | 已 tokenized + padded 英语         |
| `tgt_input`  | (32, 50)        | 德语句，右移后用于 decoder 输入            |
| `tgt_output` | (32, 50)        | 德语句，真实标签                        |
| `src_mask`   | (32, 1, 1, 50)  | encoder padding mask            |
| `tgt_mask`   | (32, 1, 50, 50) | decoder 自回归 mask + padding mask |

      
