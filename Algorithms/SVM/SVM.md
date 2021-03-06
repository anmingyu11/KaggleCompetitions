# SVM
>
> [SVM 中的正则化和损失是什么?](https://www.zhihu.com/question/30230784/answer/47837249)
>
> [SVM 等于HingeLoss+L2正则](http://breezedeus.github.io/2015/07/12/breezedeus-svm-is-hingeloss-with-l2regularization.html)
>
> [SVM 优缺点](https://zhuanlan.zhihu.com/p/77750026)
>

## 优缺点 

#### 优点

- 有严格的数学理论支持，可解释性强，不依靠统计方法，从而简化了通常的分类和回归问题；
- 能找出对任务至关重要的关键样本（即：支持向量）；
- 采用核技巧之后，可以处理非线性分类/回归任务；
- 最终决策函数只由少数的支持向量所确定，计算的复杂性取决于支持向量的数目，而不是样本空间的维数，这在某种意义上避免了“维数灾难”。

#### 缺点

- 训练时间长。当采用 SMO 算法时，由于每次都需要挑选一对参数，因此时间复杂度为 O(N^2) ，其中 N 为训练样本的数量；
- 当采用核技巧时，如果需要存储核矩阵，则空间复杂度为 O(N^2)；
- 模型预测时，预测时间与支持向量的个数成正比。当支持向量的数量较大时，预测计算复杂度较高。
- 因此支持向量机目前只适合小批量样本的任务，无法适应百万甚至上亿样本的任务。