AEX RESTful API 协议说明文档 （V2）
---

**目前V2版本只提供公开数据接口，暂不提供用户数据接口。**

[英文版](/english.md)

# 目录
+ [公开数据接口](#请求应答)
   + [获取所有交易对信息](#获取所有交易对信息)
   + [获取指定交易对信息](#获取指定交易对信息)
   + [获取指定交易对行情数据](#获取指定交易对行情数据)
   + [获取指定交易对深度](#获取指定交易对深度)
   + [获取指定交易对最新成交数据](#获取指定交易对最新成交数据)
   + [获取指定交易对历史成交数据](#获取指定交易对历史成交数据)
+ 用户数据接口（暂未实现）

# 错误码
错误码 | 说明
-----  | ---------
0      | 正常
1001   | 系统错误
4001   | 无效请求
5001   | 未认证
6001   | 已认证
7001   | 系统繁忙
8001   | 计价币不存在
9001   | 交易币不存在
10001  | 无效交易区
11001  | 该币在当前交易区不可交易

# 请求/应答
## 获取所有交易对信息   

  请求URL
  ```
  GET /v2/allpair.php
  ```
  请求参数: 无
  
  应答（json）
  ```
  {
    "eno":0,     // 错误码
    "emsg":"",   // 错误描述
    "data":[
      {
        "market":"usdt",  // 市场
        "coin":"btc",     // 币名
        "limits":{
          "PricePrecision":0,  // 挂单价格精度
          "AmtPrecision":6,    // 挂单数量精度
          "AmtMax":"10000000.00000000",  // 最大挂单数量
          "AmtMin":"0.00000100",         // 最小挂单数量
          "PriceMax":"1000000.00000000", // 最大挂单价格
          "MoneyMin":"1.00000000"        // 最小挂单资金 <= 挂单价格* 挂单数量
        }
      }
    ]
  }	
  ```
## 获取指定交易对信息   

  请求URL
  ```
  GET /v2/pair.php?market={market}&coin={coin}
  ```
  请求参数:   
  
  参数名  | 说明
  -----  | ---------
  market | 交易区，比如 cnc
  coin   | 币名，比如 btc
  
  
  应答（json）
  ```
  {
    "eno":0,     // 错误码
    "emsg":"",   // 错误描述
    "data":[
      {
        "market":"usdt",  // 市场
        "coin":"btc",     // 币名
        "limits":{
          "PricePrecision":0,  // 挂单价格精度
          "AmtPrecision":6,    // 挂单数量精度
          "AmtMax":"10000000.00000000",  // 最大挂单数量
          "AmtMin":"0.00000100",         // 最小挂单数量
          "PriceMax":"1000000.00000000", // 最大挂单价格
          "MoneyMin":"1.00000000"        // 最小挂单资金 <= 挂单价格* 挂单数量
        }
      }
    ]
  }	
  ```  
## 获取指定交易对行情数据   

  请求URL
  ```
  GET /v2/tickers.php?market={market}&coin={coin}
  ```
  请求参数:   
  
  参数名  | 说明
  -----  | ---------
  market | 交易区，比如 cnc
  coin   | 币名，比如 btc
  
  
  应答（json）
  ```
  {
    "eno":0,     // 错误码
    "emsg":"",   // 错误描述
    "data":[
      {
        "market":"cnc",   // 市场
        "coin":"btc",     // 币名
        "ticker":{
          "high":75501,     // 24小时内的最高价
          "low":72231,      // 24小时内的最低价
          "last":74654,     // 最近1次成交价
          "vol":6448.69997, // 24小时成交量
          "buy":74666,      // 当前买1价
          "sell":74728,     // 当前卖1价
          "range":0.0257    // 最新成交价跟24小时之前成交价的波动比例
        }
      }
    ]
  }
  ```  
## 获取指定交易对深度   

  请求URL
  ```
  GET /v2/depth.php?market={market}&coin={coin}
  ```
  请求参数:   
  
  参数名  | 说明
  -----  | ---------
  market | 交易区，比如 cnc
  coin   | 币名，比如 btc
  
  
  应答（json）
  ```
  {
    "eno":0,    // 错误码
    "emsg":"",  // 错误描述
    "data":{
      "bids":[
        [
          74665,    // 买价
          0.13298   // 买量
        ]
      ],
      "asks":[
        [
          74734,    // 卖价
          1.198882  // 卖量
        ]
      ]
    }
  }
  ```    
## 获取指定交易对最新成交数据   

  请求URL
  ```
  GET /v2/lasttrades.php?market={market}&coin={coin}&limit={limit}
  ```
  请求参数:   
  
  参数名  | 说明
  -----  | ---------
  market | 交易区，比如 cnc
  coin   | 币名，比如 btc
  limit  | 查询数量，可选，默认是10，最大为50
  
  
  应答（json）
  ```
  {
    "eno":0,    // 错误码
    "emsg":"",  // 错误描述
    "data":[
      {
        "tradeid":3428804,  // 成交ID
        "time":1563413853,  // 成交时间，单位秒
        "type":"buy",       // 成交类型: buy=买, sell=卖
        "price":40200,      // 成交价
        "amount":0.004975   // 成交数量
      }
    ]
  }
  ```      
## 获取指定交易对历史成交数据   

  请求URL
  ```
  GET /v2/trades.php?market={market}&coin={coin}&fromid={fromTradeID}&limit={limit}
  ```
  请求参数:   
  
  参数名  | 说明
  -----  | ---------
  market | 交易区，比如 cnc
  coin   | 币名，比如 btc
  fromid | 从哪个交易ID开始查询，结果包含此交易ID
  limit  | 查询数量，可选，默认是10，最大为50
  
  
  应答（json）
  ```
  {
    "eno":0,    // 错误码
    "emsg":"",  // 错误描述
    "data":[
      {
        "tradeid":3428804,  // 成交ID
        "time":1563413853,  // 成交时间，单位秒
        "type":"buy",       // 成交类型: buy=买, sell=卖
        "price":40200,      // 成交价
        "amount":0.004975   // 成交数量
      }
    ]
  }
  ```      
  
  
