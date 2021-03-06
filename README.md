# tgym

基于[OpenAI Gym](https://gym.openai.com/)的程序化交易环境模拟器, 旨在为沪深A股基于增强学习的交易算法提供方便使用, 接近真实市场的交易环境

撮合规则:

- 基于最高，最低价成交
- 对交易量不作限制

下单按照A股的规则，买卖按照1手100股为基本交易单位

有拆分时，会根据复权因子对持仓进行相应的倍增, 以保持与真实市场一致

## 安装指南

支持: MacOS/Linux(window未测试), python 2.7, python 3.5+, 推荐使用 python3.7

**依赖**

[tushare](https://github.com/waditu/tushare), [gym](https://github.com/openai/gym)

**安装**

```
git clone https://github.com/iminders/tgym
cd tgym
pip install -r requirements.txt
pip install -e .
```

## 使用

设置 tushare token[(token获取)](https://tushare.pro/register?reg=124861):

```
export TUSHARE_TOKEN=YOUR_TOKEN
```

[Examples](tgym/envs)

场景               | 实现         | action              | observation           | reward     | 使用例子
---------------- | ---------- | ------------------- | --------------------- | ---------- | ---------------
单支股票, 每日先卖再买     | simple.py  | [v_sell, v_buy]     | 股票信息(后复权)+指数信息+部分账户信息 | 盈利=1,否则=-1 | simple_test.py
多支股票平均分仓, 每日先卖再买 | average.py | [v_sell, v_buy] * n | 股票信息(后复权)+指数信息+部分账户信息 | 盈利=1,否则=-1 | average_test.py

场景(TODO):

- [x] 单支股票, 全仓操作
- [] 多支股票, 均匀分仓操作, on going
- [] 单支股票, 支持仓位控制
- [] 多支股票，支持仓位控制
