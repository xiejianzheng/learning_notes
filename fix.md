# fix协议学习

## 包格式
	例如：登录包
	8=fix4.2 			//BeginString 	fix版本标示
	9=78	 			//BodyLength	包大小
	35=A	 			//MsgType	消息类型	A表示Logon消息
	34=20	 			//MsgSeqNum	消息序号
	49=matching			//SendCompID	发送方ID
	52=20200212-05:44:10.308	//SendingTime	发送时间
	56=MatchingSever		//TargetCompID	接收方ID
	98=0				//EncryptMethod	加密方式	0表示没有加密
	108=30				//HeartBtInt	心跳间隔	30秒
	10=019				//CheckSum

## SessionID格式
	beginString
	senderCompID
	senderSubID
	targetCompID
	targetSubID

## NewOrderSingle 35=D
	 35 Y MsgType 		消息类型	D NewOrderSingle
	  1 N Account 		资金账号
	 11 Y ClOrdID		客户端订单标号
	526 Y SecondaryClOrdID	母单标识
	 21 Y HandlInst         订单处理指令    1 直通交易 2 允许算法或人工处理 3 人工处理
	 48 Y SecurityID
	 54 Y Side				1 买入 2 卖出
	 60 Y TransactTime	委托时间
	 38 Y OrderQty		委托数量
	 40 Y OrdType		委托类型	1 市价(Market) 2 限价(Limit)
	 44 Y Price		委托价格
	 15 Y Currency		币种		CNY HKD
	 59 Y TimeInForce	订单有限时间	0 当日有效

	167 N SecurityType 	证券类型	CS-Common Stock
						FUT-Future
						OPT-Option
						HKS-港股通
						FUN-基金
						BON-债券

	207 Y SecurityExchange 	交易所		XSSHG 上海证券交易所
						XSSHE 深圳证券交易所
						XSEC  深港通	
						XSSC  沪港通

	 58 N Text		备注		utf8

	847 Y TargetStrategy	目标策略名	int

## ExecutionReport 35=8
	 35 Y MsgType 		消息类型	8 Execution Report
	 37 Y OrderID		订单号
	 11 Y ClOrdID		客户订单号
	 41 N OrigClOrdID	原客户订单号	150=4时必须
	 17 Y ExecID		成交编号
	 20 Y ExecTransType	执行交易类型	0 New 1 Cancel

	150 Y ExecType		执行状态        0 New
						8 Rejected
						4 Canceled
						1 PartiallyFilled
						2 Filled
						D Restated 主动告警

	 39 Y OrdStatus		订单状态	0 New
	 					8 Rejected
						4 Canceled
						1 PartiallyFilled
						2 Filled
	 48 Y SecurityID
	 58 Y Side				1 买入 2 卖出
	 38 Y OrderQty		委托数量
	 40 Y OrdType		委托类型	1 市价(Market) 2 限价(Limit)
	 44 Y Price		委托价格
	 59 Y TimeInForce	订单有限时间	0 当日有效

	 32 Y LastShares	本次成交数量
	 31 Y LastPx		本次成交价格
	151 Y LeavesQty		剩余待成交数量
	 14 Y CumQty		累计成交数量
	  6 Y AvgPx		平均成交价格

	 60 Y TransactTime	委托时间
	 58 N Text		备注		utf8
	434 N CxlRejResponseTo	撤单拒绝原因	35=9时必须填
	847 Y TargetStrategy    策略名 		母单对应的策略名

## OrderCancel/Replace Request 35=G

