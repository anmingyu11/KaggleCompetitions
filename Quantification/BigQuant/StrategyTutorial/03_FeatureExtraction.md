> 导语 ：在第一步中我们通过证券代码列表模块确定好训练集和预测集的股票范围以及数据起止时间，本文介绍如何获取和计算因子数据。

如下图所示，找因子的步骤大致需要两个小步骤：

- 一是先确定符合自己需求的特征组合列表
- 二是进行特征的抽取计算。

![](https://cdn.bigquant.com/community/uploads/default/optimized/3X/0/d/0d1e5b579d759507fd9d555d027698956a37fe93_1_1380x878.jpeg)

## 一、 特征列表模块

确定了股票集后和目标条件之后，现在需要通过特征列表模块把策略的关注的数据指标输入到策略中，下面我们就介绍如何添加特征列表并传入其他关联的模块中。

#### 第一步： 在模块列表的 数据输入输出 下找到“ 输入特征列表 “ 模块并拖入画布。

![](https://cdn.bigquant.com/community/uploads/default/original/3X/3/d/3d3c206d16039d6043a0dfff5d40c5d0e60dccfe.png)

#### 第二步：点击选中输入特征列表，在属性栏特征数据文本框中编辑特征公式。

![](https://cdn.bigquant.com/community/uploads/default/original/3X/1/7/17cf95698e4a612ad0b718e64e7b3670e2981bbf.png)

我们默认封装好的模块里初始化了13个特征条件：

- return_n-表示“近n日收益率”；
- avg_amount_0/avg_amount_5-表示“当日平均成交额和5日平均成交额比值”；
- rank_avg_amount_0/rank_avg_amount_5-表示“当日平均成交额排名和5日平均成交额排名比值”；
- rank_return_0-表示“当日收益率排名”；
- rank_return_0/rank_return_5-表示“当日收益率和5日收益率比值”；
- pe_ttm_0-表示“当日市盈率”。

#### 第三步：通过模块之间的连线，将输入特征列表模块中的因子列表传入到训练集和预测集的特征抽取模块中，如下图示。

![](https://cdn.bigquant.com/community/uploads/default/original/3X/5/1/5109360fe15e0646f05d9a386b76b987f0b922fb.png)

## 二、基础特征模块和衍生特征模块

这两个模块之间可直接进行串联，作为一组特征抽取模块。

- 基础特征模块会解析特征列表模块中传入的基础因子并进行数据抽取
- 衍生特征抽取模块则会根据抽取的基础因子对复杂的表达式进行运算求值。

例如，我们在输入特征列表中输入’return_0+1’这个因子，那么首先会由基础特征模块解析并抽取return_0这个因子的数据，随后由衍生特征抽取模块计算return_0+1这个表达式的值作为因子值，最终返回列名为‘return_0+1‘的因子数据。

对于训练集与测试集而言，由于证券代码列表模块的时间段设置不同，因此各需要一组特征抽取模块。以训练集因子数据抽取流程为例：

#### 第一步： 在模块列表的 特征抽取 下找到 “ 基础特征抽取 “ 模块并拖入画布。

![](https://cdn.bigquant.com/community/uploads/default/original/3X/0/4/04a7ca727fed5e0ea4cd7b9ad16c9783d31ebdce.png)

#### 第二步： 将“输入特征列表”模块和“证券代码列表”模块的输出端与“基础特征抽取”模块的输入端连接，“基础特征抽取”模块和“输入特征列表”的输出端与“衍生特征抽取”模块的输入端连接。

![](https://cdn.bigquant.com/community/uploads/default/original/3X/4/0/40002c838b75d44b2bd3092dd99101eea87f2fd0.png)

#### 第三步：点击选中“基础特征抽取”，在属性栏中对相应的配置进行编辑。

- “开始日期”与“结束日期”，保持与前面对应的训练集一致；
- “向前取数据天数”，可根据自己需求更改天数，例如：要计算5日的收益率之和因子sum(close_0,5)那我们至少要有5个交易日的close_0基础数据才能计算这个因子的值，考虑到这里填入的是自然日天数，可能会跨假期，那么这里可以填入20以保证因子计算能够得到有效的结果。

![](https://cdn.bigquant.com/community/uploads/default/original/3X/3/6/36ed8538f03fa9e35440eccf54561a39b40159f2.png)

#### 第四步：点击选中“衍生特征抽取”，在属性栏中保持默认配置即可。

![](https://cdn.bigquant.com/community/uploads/default/original/3X/8/5/85909df22451b5d17957ad3fcc951339fd8fbfe3.png)

> 结语：因子的构建在机器学习中也称为特征工程，对模型构建的效果至关重要。
> 
> 根据定义目标的不同，因子的选择与组合是各不相同。
> 
> 在金融市场中，单个的因子统计量也被认为是市场的一个信息流，根据因子值的变化进行投资也看做为一个投资策略。
> 
> 市场中能够持续稳定获取超额收益的因子也称为alpha因子，而无法产生持续稳定超额收益的因子一般也称为风险beta因子。
> 
> 优秀的因子通过组合可以实现预测效果的提升，因此说找到优秀的因子是AI策略质量的关键。

