# 成交量加权平均价格 VWAP

VWAP是Volume weighted average price的缩写。是衡量交易算法效果的一个重要指标。

计算公式为：

	VWAP = 累计(dealPrice * dealVol) / 累计vol

# 滑点 Slippage slipBps

滑点是指**算法成交价格**与**实际成交价格**的差值。
如果**算法成交价格**优于**实际成交价格**则为正向滑点，否则为负向滑点。
如果预计成交价格为VWAP，则滑点为：

	VWAP滑点=sgn * (AvgFillPrice - VWAP)/VWAP * 10000

	买单: sgn = +1

	买单: sgn = -1



# 相对表现测量 RPM
RPM是Relative performance measure的缩写。是衡量算法交易效果的一个重要指标。

计算公式为：

	RPM = 优于市场价成交的子单的成交量 / 总成交量

如何判断一个订单是否是优于市场价成交的依据是：
   成交量加权平均价格是否比当前的市场价更优


# 被动单率
不能立即与交易所订单队列中的订单立即成交的订单为被动单。

	被动单率=被动成交数量 / 总成交数量


