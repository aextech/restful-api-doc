AEX RESTful API 协议说明文档 （V2）
---

**目前V2版本只提供公开数据接口，暂不提供用户数据接口。**

# 目录
+ [公开数据接口](#请求应答)
   + [获取所有交易对信息](#cmd-1-深度变化通知-服务器主动通知客户端)
   + [获取指定交易对信息](#cmd-2-关注交易对最多关注10个)
   + [获取指定交易对行情数据](#cmd-4-签名认证)
   + [获取指定交易对深度](#cmd-5-获取余额)
   + [获取指定交易对最新成交数据](#cmd-6-挂单)
   + [获取指定交易对历史成交数据](#cmd-7-撤单)
+ [用户数据接口（暂未实现）]()

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

  请求
  ```
  GET /v2/allpair.php
  ```
  应答（json）
  ```
  {
    "eno":0,
    "emsg":"",
    "data":[
      {
        "market":"usdt",
        "coin":"btc",
        "limits":{
          "PricePrecision":0,
          "AmtPrecision":6,
          "AmtMax":"10000000.00000000",
          "AmtMin":"0.00000100",
          "PriceMax":"1000000.00000000",
          "MoneyMin":"1.00000000"
        }
      }
    ]
  }	
  ```
## 获取指定交易对信息   

  请求（比如：market=cnc, coin=btc）
  ```
  GET /v2/pair.php?market={market}&coin={coin}
  ```
  应答（json）
  ```
  {
    "eno":0,
    "emsg":"",
    "data":[
      {
        "market":"cnc",
        "coin":"btc",
        "limits":{
          "PricePrecision":0,
          "AmtPrecision":6,
          "AmtMax":"10000000.00000000",
          "AmtMin":"0.00000100",
          "PriceMax":"1000000.00000000",
          "MoneyMin":"1.00000000"
        }
      }
    ]
  }	
  ```  
## 获取指定交易对行情数据   

  请求（比如：market=cnc, coin=btc）
  ```
  GET /v2/tickers.php?market={market}&coin={coin}
  ```
  应答（json）
  ```
  {
    "eno":0,
    "emsg":"",
    "data":[
      {
        "market":"cnc",
        "coin":"btc",
        "ticker":{
          "high":75501,
          "low":72231,
          "last":74654,
          "vol":6448.69997,
          "buy":74666,
          "sell":74728,
          "range":0.0257
        }
      }
    ]
  }
  ```  
## 获取指定交易对深度   

  请求（比如：market=cnc, coin=btc）
  ```
  GET /v2/depth.php?market={market}&coin={coin}
  ```
  应答（json）
  ```
  {
    "eno":0,
    "emsg":"",
    "data":{
    "bids":[
        [
          74665,
          0.13298
        ]
      ],
    "asks":[
        [
          74734,
          1.198882
        ]
      ]
    }
  }
  ```    
## 获取指定交易对最新成交数据   

  请求（比如：market=cnc, coin=btc, limit可选，默认为10，最大50）
  ```
  GET /v2/lasttrades.php?market={market}&coin={coin}&limit={limit}
  ```
  应答（json）
  ```
  {
    "eno":0,
    "emsg":"",
    "data":[
      {
        "tradeid":3428804,
        "time":1563413853,
        "type":"buy",
        "price":40200,
        "amount":0.004975
      }
    ]
  }
  ```      
## 获取指定交易对历史成交数据   

  请求（比如：market=cnc, coin=btc, limit可选，默认为10，最大50）
  ```
  GET /v2/trades.php?market={market}&coin={coin}&fromid={fromTradeID}&limit={limit}
  ```
  应答（json）
  ```
  {
    "eno":0,
    "emsg":"",
    "data":[
      {
        "tradeid":3428804,
        "time":1563413853,
        "type":"buy",
        "price":40200,
        "amount":0.004975
      }
    ]
  }
  ```      
  
  
