# BA_PROJECT


---

- [1. 城市共享单车需求预测]
- 任务：回归（按小时/天预测租车量）太简单
- 数据集：UCI Bike Sharing（首都共享单车 2011–2012，包括时间，天气，温度，风速等，小且干净）个位数M量级
- https://www.kaggle.com/datasets/lakshmi25npathi/bike-sharing-dataset?utm_source=chatgpt.com&select=day.csv
- 初步思路：可以用lightGBM,XGBoost,RF做回归预测，也可以带上时间序列做LSTM，商业价值就是根据天气，日期，季节这些去做需求预测，然后来控制单车投放量。
-- Pro：
  1. 简单，快速上手，快速落地
  2. 特征基本都是numerical，不需要做太多工作
- Con：
  1. 数据量太小，作为final project可能显得太简单？
---
- [2. Mercari 动态定价]
- 任务：回归（预测二手商品的合理标价）
- 数据集：Kaggle Mercari Price Suggestion Challenge（文本 + 类别 + 少量数值，常见字段包括 name, item_condition_id, category_name, brand_name, shipping, item_description, price）。总体为500 MB 量级
- https://www.kaggle.com/c/mercari-price-suggestion-challenge/data?select=test.tsv.7z&utm_source=chatgpt.com
- 初步思路：可以用lightGBM,XGBoost,RF做回归预测，对比模型性能，缺失值可以设未知桶，类别变量编码器转化。商业价值实现为通过输入产品信息得到建议价，可以搭载到一些二手网站（闲鱼，ebay）
- Pro：
  1. 数据集构成比较简单，除了编码问题以外不需要太多预处理和特征工程，可以直接上
  2. 用树base的模型基本就可以cover，不需要整太多花里胡哨的模型。
- Con：
  1. 类别变量太多了，one-hot code可能会维度爆炸，也许采用目标编码？（根据价格/销量平均值编码）
  2. 特征长尾比较严重，目标编码可能造成数据泄露，encoder待定。
---
- [3. 零售销量多步预测（M5）] 
- 任务：预测商品/门店未来销量
- 数据集：Kaggle M5 Forecasting – Accuracy，沃尔玛日级销量 + 日历 + 售价（多层级，42,840 条时间序列，特征主要就是商品类别，门店地区，价格） 400mb
- https://www.kaggle.com/competitions/m5-forecasting-accuracy/data?select=sales_train_evaluation.csv
- 初步思路：先用树模型做baseline，然后构建时间窗口做LSTM,可以通过预测销量提前备货，制定销售策略，举办促销活动，判断门店收益等。
- Pro：
  1. 商业应用比较多，方向多，report好写
- Con
  1. 数据集长得比较奇怪，前期数据处理不知道会不会比较麻烦
  2. 特征类别比较单一，感觉可能会踩过拟合或者信息泄露的坑
  3. 强需求LSTM，感觉树模型不太能cover，不知道有没有必要
