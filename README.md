数据初处理
===
数据源：
---
网易疫情实时动态播报平台

爬取获得5个数据集文件：
---
* 全国各省实时数据集(截止4-1)
* 全国各省历史数据
* 世界各国实时数据(截止4-1)
* 世界各国历史数据
* 中国疫情统计数据(1-20～4-1）<br>

![](https://github.com/MagnatePtLee/2019-nCoV-/raw/master/picture_show/DataType.png) 

处理过程：
---
* rename()函数更改列名
* 缺失值处理： 
 * 填充：当日现存确诊=累计确诊−累计治愈−累计死亡
 * 删除无意义的数据：比如未完全统计信息
* 增加指标
 * 计算病死率

可视化探索
===
世界各国实时数据分析
---
  目前美国累计确诊病例已远远高于其他国家(隔离管控措施有问题)，意大利、西班牙人数也相对较高。而在病死率的图表上意大利则位列第一，可见疫情的严重性，西班牙、法国、伊朗、英国、比利时病死率紧跟其后。然而，累计确诊人数最高的美国病死率却相对较低 <br>
  
![](https://github.com/MagnatePtLee/2019-nCoV-/raw/master/picture_show/当前累计确诊top10国家.png) 

  `原因猜测`：
* 美国医疗资源丰富。根据权威报表可知美国每十万居民拥有将近35个ICU床位，排在世界第一，德国紧跟其后有近30个ICU床位，两国的医疗资源远远高于其他国家。（病死率侧面可反映医疗水平）
* 老龄化没有意大利等国家严重(意大利超过23%都在65岁以上)

全国各省历史数据分析
---
![](https://github.com/MagnatePtLee/2019-nCoV-/raw/master/picture_show/全国病死率.png)

前期病死率偏高，一方面是前期准备工作不足，医疗物资短缺，另一方面是确诊率偏低；后期病死率有所上升，应该主要是因为确诊人数越来越少 <br>
同一种病毒，面对同一人群，病死率应该是大致相同的 <br>
考虑到封城、并发症、医疗物资的影响,省内外病死率相近时接近疫情拐点
即12号～20号

全国各省实时数据分析 
---
![](https://github.com/MagnatePtLee/2019-nCoV-/raw/master/picture_show/全国新增确诊top10地区.png) 

目前我国香港、台湾新增确诊人数最多 <br>
`原因猜测`：一国两制，欧美回港人士检疫措施 <br>
截止3月18号以前，香港感染宗数保持在个位数，防止了第一波疫情的冲击，之后开始有松懈心理 <br>

![](https://github.com/MagnatePtLee/2019-nCoV-/raw/master/picture_show/全国现存确诊top10.png) 

虽然湖北现存确诊人数最多，有1283例，但已经没有新增案例，可见湖北疫情目前已经基本稳定 <br>
除湖北外，香港、台湾、上海、北京、广东现存确诊人数也较多，新增也较多 <br>
`原因猜测`：交通较发达，境外输入病例的主要落脚点

全国历史数据分析
---
![](https://github.com/MagnatePtLee/2019-nCoV-/raw/master/picture_show/全国历史数据.png)

* 我国每日新增确诊经过1月23日武汉封城后在2月12日到达峰值；
* 累计确诊在2月15号左右达到拐点
* 现存确诊人数也已从2月17日起逐步减少。
* 同时，累计治愈人数稳步上升，且随现存确诊人数的下降而逐渐趋于平缓状态。<br>

![](https://github.com/MagnatePtLee/2019-nCoV-/raw/master/picture_show/全国新增确诊.png) 

在单独查看当然新增确诊的曲线时，2月4日达到第一个峰值，发现在2月12日时大幅上升
`上升原因`：在当天国家卫健委调整了确诊的标准，将临床诊断纳入确诊范围

世界各国历史数据分析
---
![](https://github.com/MagnatePtLee/2019-nCoV-/raw/master/picture_show/疫情国家数量.png) 

疫情国家数量在3月26日疫情国家数量达到最大，从2月21开始数量变化的幅度明显变大 <br>

![](https://github.com/MagnatePtLee/2019-nCoV-/raw/master/picture_show/各国.png) 

`GroupBy技术和层次化索引操作` <br>
中韩两国目前累计确诊人数已出现拐点，疫情趋于平稳，而美国在最近几天累计确诊人数呈现爆发性的增长，已位居世界第一。此外，意大利、西班牙两国增长速度也紧跟其后，但意大利的增长已出现明显放缓的迹象 <br>
各国新增确诊人数波动较大，但总体趋势呈上升状态。3月25日起，日本的新增确诊人数明显增大；在3月下旬，美国和西班牙首次单日新增确诊人数破万

疫情数据预测
===
Logistic函数
---
以美国为例：<br>
因为数据集太少，不便于拆分数据集，所以先做线性回归分析模型 <br>

![](https://github.com/MagnatePtLee/2019-nCoV-/raw/master/picture_show/Logistic函数.png) 

`结果`：<br>
预测美国在出现疫情后的80天，也就是5月份达到`130万`左右，考虑到目前的严峻形式，美国如果没有更积极有效的措施，实际数据甚至会在130万以上。

时间序列模型Prophet
---
基于时间序列分解和机器学习的拟合来做的,全自动地预测时间序列未来的走势
以中国为例：<br>

![](https://github.com/MagnatePtLee/2019-nCoV-/raw/master/picture_show/Prophet1.png) 
![](https://github.com/MagnatePtLee/2019-nCoV-/raw/master/picture_show/Prophet2.png) 

`发现`:对于美国的数据做测试的结果不好 <br>
对于一些周期性或者趋势性不是很强的时间序列，用 Prophet 就不合适了

LSTM模型（单变量时间序列）
---
用中国新冠肺炎数据来训练，用美国的数据做测试，时间步长为3 <br>

![](https://github.com/MagnatePtLee/2019-nCoV-/raw/master/picture_show/LSTM.png) 

问题：预测未做 <br>
按照理论做法，需要事先反向提取最后3个数据，以预测第一个新值。然后利用第一个新值，并结合前面2个的数据，预测第二个新值，依次循环下去













