# History data of simulated LND orders

这个仓库给出了仿真的LND订单的部分数据，考虑到数据的隐私性，我们对数据中的具体信息都进行了脱敏。

## Description

这个仓库提供了两个数据集，一个是实验部分是仿真订单数据，其中包括每个订单的总体信息以及划分成子订单后各个子订单的交付信息。另一个数据集是讨论章节建模司机乐观程度所需要的数据集范例，我们认为**在得到司机的订单交付信息之后，物流公司可以对每个司机的乐观程度进行建模，从而为司机分配做出最佳决策**是一个很好的点子，但是尚未在实验中实践。两个数据集在仓库中的位置和基本描述整理如下：

-  仿真订单数据
   -  本仓库提供了100个仿真订单数据的主要信息，具体数据位于根目录的`order_describe`和`order_detail`文件夹中。其中`order_describe`文件夹给出了每个订单的总体信息，使用`txt`文件存储；`order_detail`文件夹给出了订单被拆分为多个子订单之后每一个子订单的具体交付信息，使用`csv`文件存储。
-  司机历史交付数据范例
   -  本仓库提供了一位司机的历史接单信息，具体数据位于根目录的`driver`文件夹中，使用`csv`文件存储。平台可以根据已有的司机乐观程度模型对该司机的历史交付数据进行拟合，并在后续的运营过程中动态更新每一个司机的乐观程度建模，从而更好的进行司机分配。

## Data

The dataset comes from a [tracking schema](https://meta.wikimedia.org/wiki/Schema:TestSearchSatisfaction2) that we use for assessing user satisfaction. Desktop users are randomly sampled to be anonymously tracked by this schema which uses a "I'm alive" pinging system that we can use to estimate how long our users stay on the pages they visit. The dataset contains just a little more than a week of EL data.

### order_describe

| Column          | Value   | Description                                                  |
| :-------------- | :------ | :----------------------------------------------------------- |
| uuid            | string  | Universally unique identifier (UUID) for backend event handling. |
| timestamp       | integer | The date and time (UTC) of the event, formatted as YYYYMMDDhhmmss. |
| session_id      | string  | A unique ID identifying individual sessions.                 |
| group           | string  | A label ("a" or "b").                                        |
| action          | string  | Identifies in which the event was created. See below.        |
| checkin         | integer | How many seconds the page has been open for.                 |
| page_id         | string  | A unique identifier for correlating page visits and check-ins. |
| n_results       | integer | Number of hits returned to the user. Only shown for searchResultPage events. |
| result_position | integer | The position of the visited page's link on the search engine results page (SERP). |

- 

### Example

| uuid                             | timestamp      | session_id       | group | action           | checkin | page_id          | n_results | result_position |
| :------------------------------- | :------------- | :--------------- | :---- | :--------------- | ------: | :--------------- | --------: | --------------: |
| 4f699f344515554a9371fe4ecb5b9ebc | 20160305195246 | 001e61b5477f5efc | b     | searchResultPage |      NA | 1b341d0ab80eb77e |         7 |              NA |
| 759d1dc9966353c2a36846a61125f286 | 20160305195302 | 001e61b5477f5efc | b     | visitPage        |      NA | 5a6a1f75124cbf03 |        NA |               1 |
| 77efd5a00a5053c4a713fbe5a48dbac4 | 20160305195312 | 001e61b5477f5efc | b     | checkin          |      10 | 5a6a1f75124cbf03 |        NA |               1 |
| 42420284ad895ec4bcb1f000b949dd5e | 20160305195322 | 001e61b5477f5efc | b     | checkin          |      20 | 5a6a1f75124cbf03 |        NA |               1 |
| 8ffd82c27a355a56882b5860993bd308 | 20160305195332 | 001e61b5477f5efc | b     | checkin          |      30 | 5a6a1f75124cbf03 |        NA |               1 |
| 2988d11968b25b29add3a851bec2fe02 | 20160305195342 | 001e61b5477f5efc | b     | checkin          |      40 | 5a6a1f75124cbf03 |        NA |               1 |

This user's search query returned 7 results, they clicked on the first result, and stayed on the page between 40 and 50 seconds. (The next check-in would have happened at 50s.)
