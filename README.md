## 一、概述

本赛题任务是利用二手车的信息，训练模型，预测二手车交易价格。我的解决方案主要有三大亮点：第一用类别特征对与label高相关的数值特征做统计描述；第二充分利用匿名特征信息，两两间做特征交互；第三构造简单六层神经网络模型。最后成绩**46/9885（Top0.47%）**

![image-20210302040458188](https://raw.githubusercontent.com/XiaoYuan00/picture/master/image-20210302040458188.png)

## 二、数据处理

1、box-cox变换目标值“price”，解决长尾分布。 

2、删除与目标值无关的列，例如“SaleID”，“name”。这里可以挖掘一下“name”的频度作为新的特征。

3、异常点处理，删除训练集特有的数据，例如删除“seller”==1的值。

4、缺失值处理，分类特征填充众数，连续特征填充平均值。

5、其他特别处理，把取值无变化的列删掉。

6、异常值处理，按照题目要求“power”位于0～600，因此把“power”>600的值截断至600，把"notRepairedDamage"的非数值的值替换为np.nan，让模型自行处理。

## 三、特征工程 

#### 时间地区类   

从“regDate”，“creatDate”可以获得年、月、日等一系列的新特征，然后做差可以获得使用年长和使用天数这些新特征。