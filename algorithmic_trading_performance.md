# VWAP 市场成交量加权平均价格

VWAP是Volume weighted average price的缩写。

计算公式为：

	VWAP = 累计(dealPrice * dealVol) / 累计vol

一般VWAP指的是市场VWAP。
VWAP是衡量交易市场算法绩效的一个重要指标。

做算法绩效评估时，可以用算法的平均成交均价和市场VWAP做比较， bps越低越好。

# VWAP滑点

**VWAP滑点**是衡量算法成交均价与VWAP偏差的的一个指标。参考标准为VWAP， 计数单位为BPS(基点)

计算公式为：

	VWAP滑点=sgn * (AvgFillPrice - VWAP)/VWAP * 10000

	买单: sgn = -1

	买单: sgn = +1

	如果**算法成交价格**优于**实际成交价格**则为正向滑点，否则为负向滑点。


# RPM 相对表现测量 
RPM是Relative performance measure的缩写。是衡量算法交易效果的一个重要指标。

计算公式为：

	RPM = 优于市场价成交的子单的成交量 / 总成交量

如何判断一个订单是否是优于市场价成交的依据是：
   成交量加权平均价格是否比当前的市场价更优

# 到达中间价 Arrival Mid Price

# 被动单 Passive order

# 被动单率
不能立即与交易所订单队列中的订单立即成交的订单为被动单。

	被动单率=被动成交数量 / 总成交数量


