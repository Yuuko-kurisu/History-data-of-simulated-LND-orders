# History data of simulated LND orders

This is the simulation data for the paper [“](https://www.sciencedirect.com/science/article/abs/pii/S1474034623003853)[Preliminary exploration for long-distance non-standardized delivery](https://ieeexplore.ieee.org/abstract/document/10225615)[”](https://www.sciencedirect.com/science/article/abs/pii/S1474034623003853)

Authors: H Jiang, J You, Z Chen, Y Shi, S Qiu, X Ming, Poly Z.H Sun

```
@ARTICLE{10225615,
  author={Jiang, Hongwei and You, Jiapeng and Chen, Zhiyang and Shi, Yida and Qiu, Siqi and Ming, Xinguo and Sun, Poly Z. H.},
  journal={IEEE Transactions on Intelligent Transportation Systems}, 
  title={Preliminary Exploration for Long-Distance Non-Standardized Delivery}, 
  year={2023},
  volume={24},
  number={12},
  pages={14347-14361},
  doi={10.1109/TITS.2023.3299618}}

```



这个仓库给出了仿真的LND订单的部分数据，考虑到数据的隐私性，我们对数据中的具体信息都进行了脱敏。

## Description

这个仓库提供了两个数据集，一个是实验部分是仿真订单数据，其中包括每个订单的总体信息以及划分成子订单后各个子订单的交付信息。另一个数据集是讨论章节建模司机乐观程度所需要的数据集范例，我们认为**在得到司机的订单交付信息之后，物流公司可以对每个司机的乐观程度进行建模，从而为司机分配做出最佳决策**是一个很好的点子，但是尚未在实验中实践。两个数据集在仓库中的位置和基本描述整理如下：

-  仿真订单数据
   -  本仓库提供了100个仿真订单数据的主要信息，具体数据位于根目录的`order_describe`和`order_detail`文件夹中。其中`order_describe`文件夹给出了每个订单的总体信息，使用`txt`文件存储；`order_detail`文件夹给出了订单被拆分为多个子订单之后每一个子订单的具体交付信息，使用`csv`文件存储。
-  司机历史交付数据范例
   -  本仓库提供了一位司机的历史接单信息，具体数据位于根目录的`driver`文件夹中，使用`csv`文件存储。平台可以根据已有的司机乐观程度模型对该司机的历史交付数据进行拟合，并在后续的运营过程中动态更新每一个司机的乐观程度建模，从而更好的进行司机分配。

## Data

下面给出了每个文件夹里面数据的具体介绍。

### order_describe

| Column           | Description                                    |
| :--------------- | :--------------------------------------------- |
| order_index      | 订单的索引                                     |
| order_start_time | 订单的开始时刻，即客户向平台下单的时间点       |
| order_end_time   | 订单的结束时间，客户要求的交付期限             |
| start_point      | 订单起始位置                                   |
| end_point        | 订单的终点                                     |
| start_station    | 订单的起点站，一般是离订单起始位置最近的中转站 |
| end_station      | 订单的终点站                                   |
| path             | 划分子订单时，平台为订单规划的路径             |

### order_detail

| Column            | Description                                      |
| :---------------- | :----------------------------------------------- |
| suborder_index    | 子订单的执行序位                                 |
| suborder_distance | 子订单的距离                                     |
| start_station     | 子订单的起始站点                                 |
| end_station       | 子订单的终点站                                   |
| start_time        | 子订单的起始时间，即平台为子订单分配时间的时间点 |
| end_time          | 子订单的终止时间，即司机到达子订单终点站的时间   |
| promise_time      | 司机接单时提供的承诺交付时间                     |
| actual_time       | 司机的实际交付时间                               |
| driver_price      | 平台给司机的定价                                 |

### driver

| Column            | Description                                      |
| :---------------- | :----------------------------------------------- |
| driver_id         | 司机的识别编号                                   |
| suborder_distance | 子订单的距离                                     |
| start_station     | 子订单的起始站点                                 |
| end_station       | 子订单的终点站                                   |
| start_time        | 子订单的起始时间，即平台为子订单分配时间的时间点 |
| end_time          | 子订单的终止时间，即司机到达子订单终点站的时间   |
| promise_time      | 司机接单时提供的承诺交付时间                     |
| actual_time       | 司机的实际交付时间                               |
| driver_price      | 平台给司机的定价                                 |
