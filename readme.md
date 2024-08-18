# API说明文档

## 根部API https://vvk3.com

### 登录，前提条件要访问机器人 START 后 才会注册用户
### /tglogin
- Method: POST
- Request: 【body】
```json
{
    "initData": "Telegram.WebApp.initData", //Telegram 用户数据
    "fingerprint": "详情 ： https://demo.fingerprint.com/" //指纹
}
```
- Response:
```json
{
    "token": "xxxxxx",
    "code": "0正常,其余的会有msg 提示错误，游戏中如需提示需要转当前选择的语言文案提示"
}
```

### 背包
#### /backpack
- Method: POST
- Request: 【body】
```json
{
    "token": "/tglogin 返回的token",
    "userid": 12345678
}
```
- Response:

```json
{
  "code": "0正常,其余的会有msg 提示错误，游戏中如需提示需要转当前选择的语言文案提示",
  "data": [
    {
      "id": 1,
      "goodsID": "101",
      "time": 1623871713132,//时间戳
    }
  ]
}
```

### 切换武器
#### /weapons
- Method: POST
- Request: 【body】
```json
{
    "token": "/tglogin 返回的token",
    "userid": 12345678,
    "goodsID": 101 //武器ID
}
```
- Response:
```json
{
    "code": "0正常,其余的会有msg 提示错误，游戏中如需提示需要转当前选择的语言文案提示"
}
```


### 开始游戏
#### /startgame 
- Method: POST
- Request: 【body】
```json
{
    "token": "/tglogin 返回的token",
    "userid": 12345678
}
```
- Response:
```json
{
    "code": "0正常,其余的会有msg 提示错误，游戏中如需提示需要转当前选择的语言文案提示"
}
```


### 拾取奖励
#### /pickup 
- Method: POST
- Request: 【body】
```json
{
    "token": "/tglogin 返回的token",
    "userid": 12345678
}
```
- Response:
```json
{
    "code": "0正常,其余的会有msg 提示错误，游戏中如需提示需要转当前选择的语言文案提示"
}
```


### 签到界面初始化
#### /sign 
- Method: POST
- Request: 【body】
```json
{
    "token": "/tglogin 返回的token",
    "userid": 12345678
}
```
- Response:
```json
{
  "code": "0正常,其余的会有msg 提示错误，游戏中如需提示需要转当前选择的语言文案提示",
  "data": {
    "list": [],//签到列表奖励内容 展示
    "count": 1,//当前签到次数，如果是0 从未签到过，以此类推 如果是7则所有签到完成
  }
}
```


### 签到动作
#### /singnin 
- Method: POST
- Request: 【body】
```json
{
    "token": "/tglogin 返回的token",
    "userid": 12345678
}
```
- Response:
```json
{
    "code": "0正常,其余的会有msg 提示错误，游戏中如需提示需要转当前选择的语言文案提示"
}
```


### 转盘初始化
#### /turntable 
- Method: POST
- Request: 【body】
```json
{
    "token": "/tglogin 返回的token",
    "userid": 12345678
}
```
- Response:

```json
{
  "code": "0正常,其余的会有msg 提示错误，游戏中如需提示需要转当前选择的语言文案提示",
  list: [
    {
      id: 1,
      type: 'gameBalance',
      value: 500
    },
    {
      id: 2,
      type: 'gameBalance',
      value: 1000
    },
    {
      id: 3,
      type: 'gameBalance',
      value: 1500
    },
    {
      id: 4,
      type: 'gameBalance',
      value: 2000
    },
    {
      id: 5,
      type: 'trxBalance',
      value: 10
    },
    {
      id: 6,
      type: 'zfbBalance',
      value: 100
    },
    {
      id: 7,
      type: 'zfbBalance',
      value: 300
    },
    {
      id: 8,
      type: 'zfbBalance',
      value: 500
    }
  ],
  //转盘奖励列表 type 币种类型 value 奖励数量
  "turntableTimes": 1,//剩余次数
}
```


### 转盘抽奖
#### /turntablego
- Method: POST
- Request: 【body】
```json
{
    "token": "/tglogin 返回的token",
    "userid": 12345678
}
```
- Response:
```json
{
    "code": "0正常,其余的会有msg 提示错误，游戏中如需提示需要转当前选择的语言文案提示",
    "id":1,//奖励id
    "gameBalance":123456,//更新 gameBalance余额
    "trxBalance":123456,//更新 trxBalance余额
    "zfbBalance":123456,//更新 zfbBalance余额
    
}
```

### 余额
#### /balance
- Method: POST
- Request: 【body】
```json
{
    "token": "/tglogin 返回的token",
    "userid": 12345678
}
```
- Response:
```json
{
    "code": "0正常,其余的会有msg 提示错误，游戏中如需提示需要转当前选择的语言文案提示",
    "gameBalance":123456,// gameBalance余额
    "trxBalance":123456,// trxBalance余额
    "zfbBalance":123456,// zfbBalance余额
    "availableTRX":123456,// 可转账trx余额
    
}
```


### 转账TRX
#### /transfertrx
- Method: POST
- Request: 【body】
```json
{
    "token": "/tglogin 返回的token",
    "userid": 12345678,
    "trxBalance": 123456,//转账数量
    "toAddress": "TKJFKKDSKHKJFJLDFLKFLKFKLSFLK"//TRX地址
}
```
- Response:
```json
{
    "code": "0正常,其余的会有msg 提示错误，游戏中如需提示需要转当前选择的语言文案提示",
}
```


### TRX记录
#### /trxrecord
- Method: POST
- Request: 【body】
```json
{
    "token": "/tglogin 返回的token",
    "userid": 12345678,
}
```
- Response:
```json
{
    "code": "0正常,其余的会有msg 提示错误，游戏中如需提示需要转当前选择的语言文案提示",
     "data": [
        {
            "id": 1,
            "userid": 123456,
            "amount": 100,
            "type": "0",//0转出 1转入
            "address": "address",
            "txid": "address",
            "time": "时间戳"
        }
     ],
     count: 1,//总数
     start: 0,//第几条开始，默认0
     end: 100,//第几条结束，默认100
  
}
```


### 商店列表
#### /store
- Method: POST
- Request: 【body】
```json
{
    "token": "/tglogin 返回的token",
    "userid": 12345678
}
```
- Response:
```json
{
    "code": "0正常,其余的会有msg 提示错误，游戏中如需提示需要转当前选择的语言文案提示",
    
}
```


### 商店购买物品
#### /buy
- Method: POST
- Request: 【body】
```json
{
    "token": "/tglogin 返回的token",
    "userid": 12345678
}
```
- Response:

```json
{
  code: "0正常,其余的会有msg 提示错误，游戏中如需提示需要转当前选择的语言文案提示",
  gameBalance: 123456, //更新 gameBalance余额 code 非 0 时为空
  coinsCount: 123456, //更新 coinsCount余额  code 非 0 时为空
  teamCount: 123456, //更新 teamCount余额  code 非 0 时为空
  giantCount: 123456, //更新 giantCount余额  code 非 0 时为空
  zFBBalance: 123456, //更新 zFBBalance余额  code 非 0 时为空
  tRXBalance: 123456, //更新 tRXBalance余额  code 非 0 时为空
}
```

### 刷新体力 (推荐每3-5分钟自动请求一次)
#### /refresh
- Method: POST
- Request: 【body】
```json
{
    "token": "/tglogin 返回的token",
    "userid": 12345678
}
```
- Response:
```json
{
    "code": "0正常,其余的会有msg 提示错误，游戏中如需提示需要转当前选择的语言文案提示",
    
}
```

### 刷新邀请列表
#### /invite
- Method: POST
- Request: 【body】
```json
{
    "token": "/tglogin 返回的token",
    "userid": 12345678,
    "start": 0,//第几条开始，默认0,可选参数
    "end": 100 //第几条结束，默认100,可选参数
}
```
- Response:

```json
{
  "code": "0正常,其余的会有msg 提示错误，游戏中如需提示需要转当前选择的语言文案提示",
  "data":[],
  "count": 1,//总数
  "start": 0,//第几条开始，默认0
  "end": 100,//第几条结束，默认100
}
```

### 任务列表
#### /task
- Method: POST
- Request: 【body】
```json
{
    "token": "/tglogin 返回的token",
    "userid": 12345678
}
```
- Response:

```json
{
  "code": "0正常,其余的会有msg 提示错误，游戏中如需提示需要转当前选择的语言文案提示",
  "data": [
    {
      id: 1,
      desc: "任务描述",
      type: "1 邀请 2 进入频道 3消耗 4消耗TRX 5充值TRX 6购买盲盒",
      count: "完成任务数量",
      gameAmount: "奖励游戏币",
      zfbAmount: "奖励自发币",
      trxAmount: "奖励TRX"
    }
  ]
}
```
