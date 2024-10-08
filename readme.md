# API 说明文档

## 目录
1. [登录](#登录)
2. [背包](#背包)
3. [切换武器](#切换武器)
4. [开始游戏](#开始游戏)
5. [拾取奖励](#拾取奖励)
6. [游戏结束](#游戏结束)
7. [签到界面初始化](#签到界面初始化)
8. [签到动作](#签到动作)
9. [转盘初始化](#转盘初始化)
10. [转盘抽奖](#转盘抽奖)
11. [余额查询](#余额查询)
12. [转账TRX](#转账trx)
13. [TRX记录查询](#trx记录查询)
14. [商店列表](#商店列表)
15. [购买物品](#购买物品)
16. [刷新体力](#刷新体力)
17. [刷新已存在的邀请列表](#刷新已存在的邀请列表)
18. [任务列表](#任务列表)
19. [关卡数据](#关卡数据)
20. [错误码](#错误码)

## 根部API https://api1.vvk3.com （未来需要动态获取）

#### [Postman DEMO](https://github.com/Andyok2022/descapi/blob/main/Test.postman_collection.json)
##### 注：所有token 通过 Heade参数添加 :"Authorization"："token" 传递过来

## 登录
##### 前提条件要访问机器人 START 后 才会注册用户
### `/tglogin`
##### 该api无需传token 其余都需要
- **Method**: POST
  - **Request**:
      ```json
      {
          "initData": "Telegram.WebApp.initData", //Telegram 用户数据
          "fingerprint": "详情 ： https://demo.fingerprint.com/" //指纹 每个手机唯一值 用于确保同手机多tg登录互相邀请刷  TRX 行为
      }
      ```
- **Response**:
    ```json
    {
        "token": "xxxxxx",
        "code": "0正常,其余的会有msg 提示错误，游戏中如需提示需要转当前选择的语言文案提示"
        "inviteUrl": "邀请链接",
        "inviteDesc": "邀请英文文案",
        "groupURL":groupURL,//加入群组id
        "userInfo": UserObject,
    }
    ```
  ```json
  UserObject
  {
      "userid": "userid",
      "first_name": "用户昵称 1",
      "last_name": "用户昵称 2",
      "username": "用户搜索名@xxx",
      "headpic": "用户头像",
      "superiorID": "上级id",
      "physicalPower": "体力 每分钟恢复 1体力，邀请2个好友后增加100% ，一局扣10点",
      "physicalPowerTime": "刷新时间",
      "physicalPowerMax": "体力上限",
      "resurrection": "复活次数",
      "levels": "当前关卡",
      "gameBalance": "游戏余额",
      "tRXBalance": "TRX余额",
      "zFBBalance": "未来发的币",
      "consumption": "消耗TRX余额总数",
      "teamCount": "兵数量",
      "coinsCount": "金币加成",
      "giantCount": "防爆兵数量",
      "currentWeapons": "当前武器",
      "turntableTimes": "转盘剩余次数",
      "vipExperience": "VIP经验",
      "addressTRXBalance": "地址TRX金额",
      "addressUSDTBalance": "地址USDT余额",
      "address": "用户地址",
      "lastOnlineTime": "最后一次在线时间",
      "maximumGameingTRX": "游戏过程可获得最大trx",
      "addGroupTime": "加群时间",
      "groupID": "所属群组id",
      "premium": "是否是优质的",
      "airdropgameBalance": "已经空投了多少游戏币，邀请奖励",
      "airdropzFBBalance": "已经空投了多少ZFB，邀请奖励",
      "airdropBalanceTRX": "已经空投了多少TRX，邀请奖励",
      "singninTime": "最后一次签到时间",
      "lastLoginTime": "最后登录时间",
      "language_code": "telegram语言版本",
      "isquit": "0 是 默认 ， 时间戳 是 退群时间，1 是回归用户",
      "ismute": "是否禁言",
      "token": "token",
      "tokenLife": "token生命周期",
      "inviteUrl": "邀请链接",
      "fingerprint": "指纹"
    }
  ```
## 背包
### `/backpack`
- **Method**: POST
- **Request**:
    ```json
    {
        "userid": 12345678
    }
    ```
- **Response**:
    ```json
    {
        "code": "0正常,其余的会有msg 提示错误，游戏中如需提示需要转当前选择的语言文案提示",
        "data": [
            {
                "id": 1,
                "goodsID": "101",
                "time": 1623871713132 //时间戳
            }
        ]
    }
    ```

## 切换武器
### `/weapons`
- **Method**: POST
- **Request**:
    ```json
    {
        "userid": 12345678,
        "goodsID": 101 //武器ID
    }
    ```
- **Response**:
    ```json
    {
        "code": "0正常,其余的会有msg 提示错误，游戏中如需提示需要转当前选择的语言文案提示"
    }
    ```

## 开始游戏
### `/startgame`
- **Method**: POST
- **Request**:
    ```json
    {
        "userid": 12345678
    }
    ```
- **Response**:
    ```json
    {
        "code": "0正常,其余的会有msg 提示错误，游戏中如需提示需要转当前选择的语言文案提示",
        "tRXBalance": 1, //可得到的TRX数量 ，部分游戏过程 部分结束抽奖 随机 根据场景使用 /pickup 接口获得
        "gameBalance": 1, //结束后可得到的游戏币数量，部分游戏过程 部分结束抽奖 随机 根据场景使用 /pickup 接口获得
        "zFBBalance": 1, //结束后可得到的自发币数量，部分游戏过程 部分结束抽奖 随机 根据场景使用 /pickup 接口获得
        "trxPoint": 1, //可得到的TRX 地点数量，部分游戏过程 部分结束抽奖 随机 根据场景使用 /pickup 接口获得
        "inviteCount": 1, //线下已经邀请的成员，游戏结束后翻牌数量
        
    }
    ```

## 拾取奖励
### `/pickup`
- **Method**: POST
- **Request**:
    ```json
    {
        "userid": 12345678,
        "type": 0 //币种类型 0 游戏币，1自发币，2 TRX
        "amount": 10 //币数量
    }
    ```
- **Response**:
    ```json
    {
        "code": "0正常,其余的会有msg 提示错误，游戏中如需提示需要转当前选择的语言文案提示"
    }
    ```

## 游戏结束
### `/gameover`
- **Method**: POST
- **Request**:
    ```json
    {
        "userid": 12345678,
        "result": 1 //1终点结束, 2中途死亡
    }
    ```
- **Response**:
    ```json
    {
        "code": "0正常,其余的会有msg 提示错误，游戏中如需提示需要转当前选择的语言文案提示"
    }
    ```

## 签到界面初始化
### `/sign`
- **Method**: POST
- **Request**:
    ```json
    {
        "userid": 12345678
    }
    ```
- **Response**:
    ```json
    {
        "code": "0正常,其余的会有msg 提示错误，游戏中如需提示需要转当前选择的语言文案提示",
        "data": {
            "list": [], //签到列表奖励内容 展示
            "count": 1 //当前签到次数，如果是0 从未签到过，以此类推 如果是7则所有签到完成
        },
        "todayIsAvailable": 1 //今天是否可以签到 0 不可以 1 可以
    }
    ```

## 签到动作
### `/singnin`
- **Method**: POST
- **Request**:
    ```json
    {
        "userid": 12345678
    }
    ```
- **Response**:
    ```json
    {
        "code": "0正常,其余的会有msg 提示错误，游戏中如需提示需要转当前选择的语言文案提示"
        "gameBalance": 123456, //更新 gameBalance余额
    }
    ```

## 转盘初始化
### `/turntable`
- **Method**: POST
- **Request**:
    ```json
    {
        "userid": 12345678
    }
    ```
- **Response**:
    ```json
    {
        "code": "0正常,其余的会有msg 提示错误，游戏中如需提示需要转当前选择的语言文案提示",
        "list": [
            {"id": 1, "type": "gameBalance", "value": 500},
            {"id": 2, "type": "gameBalance", "value": 1000},
            {"id": 3, "type": "gameBalance", "value": 1500},
            {"id": 4, "type": "gameBalance", "value": 2000},
            {"id": 5, "type": "trxBalance", "value": 10},
            {"id": 6, "type": "zfbBalance", "value": 100},
            {"id": 7, "type": "zfbBalance", "value": 300},
            {"id": 8, "type": "zfbBalance", "value": 500}
        ],
        "turntableTimes": 1 //剩余次数
    }
    ```

## 转盘抽奖
### `/turntablego`
- **Method**: POST
- **Request**:
    ```json
    {
        "userid": 12345678
    }
    ```
- **Response**:
    ```json
    {
        "code": "0正常,其余的会有msg 提示错误，游戏中如需提示需要转当前选择的语言文案提示",
        "id": 1, //奖励id
        "turntableTimes": 1, //剩余次数
        "gameBalance": 123456, //更新 gameBalance余额
        "trxBalance": 123456, //更新 trxBalance余额
        "zfbBalance": 123456 //更新 zfbBalance余额
    }
    ```

## 余额查询
### `/balance`
- **Method**: POST
- **Request**:
    ```json
    {
        "userid": 12345678
    }
    ```
- **Response**:
    ```json
    {
        "code": "0正常,其余的会有msg 提示错误，游戏中如需提示需要转当前选择的语言文案提示",
        "gameBalance": 123456, // gameBalance余额
        "trxBalance": 123456, // trxBalance余额
        "zfbBalance": 123456, // zfbBalance余额
        "availableTRX": 123456 // 可转账trx余额
    }
    ```

## 转账TRX
### `/transfertrx`
- **Method**: POST
- **Request**:
    ```json
    {
        "userid": 12345678,
        "trxBalance": 123456, //转账数量
        "toAddress": "TKJFKKDSKHKJFJLDFLKFLKFKLSFLK" //TRX地址
    }
    ```
- **Response**:
    ```json
    {
        "code": "0正常,其余的会有msg 提示错误，游戏中如需提示需要转当前选择的语言文案提示"
        "tRXBalance": 123456 //当前TRX金额
    }
    ```

## TRX记录查询
### `/trxrecord`
- **Method**: POST
- **Request**:
    ```json
    {
        "userid": 1p2345678
    }
    ```
- **Response**:
    ```json
    {
        "code": "0正常,其余的会有msg 提示错误，游戏中如需提示需要转当前选择的语言文案提示",
        "data": [
            {
                "id": 1,
                "userid": 123456,
                "amount": 100,
                "type": "0", //0转出 1转入
                "address": "address",
                "txid": "txid",
                "time": "时间戳"
            }
        ],
        "count": 1, //总数
        "start": 0, //第几条开始，默认0
        "end": 100 //第几条结束，默认100
    }
    ```

## 商店列表
### `/store`
- **Method**: POST
- **Request**:
    ```json
    {
        "userid": 12345678
    }
    ```
  - **Response**:
      ```json
      {
          "code": "0正常,其余的会有msg 提示错误，游戏中如需提示需要转当前选择的语言文案提示"
      }
      ```
      ```json
          {
          "id": "商店列表",
          "type": "0 武器装备，1 体力，2金币，3加成，4小小兵, 5防爆兵,6盲盒,7转账（提现）",
          "buyFeeType": "币种类型 0 游戏币，1自发币，2 TRX",
          "goodsID": "武器装备 id",
          "basePrice": "基础费用",
          "priceX": "级别乘积",
          "threshold": "购买门槛，邀请人数量，默认0",
          "level": "级别",
          "maxLevel": "最高级",
          "desc": "描述",
          "isShowStore": "是否展示到商店 1展示 0不展示"
          }
      ```

## 购买物品
### `/buy`
- **Method**: POST
- **Request**:
    ```json
    {
        "userid": 12345678,
        "goodsID": 101, //物品ID
    }
    ```
- **Response**:
    ```json
    {
        "code": "0正常,其余的会有msg 提示错误，游戏中如需提示需要转当前选择的语言文案提示",
        "goodsID":0,//0 为购买盲盒获得trx 其余的就是随机goodsID
        "getAmount":110,//购买盲盒获得的trx数量
        "goodsTimes":1,//购买盲盒中奖 goodsID为 301 - 303 的 数量
        "gameBalance": 123456, //更新 gameBalance余额
        "coinsCount": 123456, //更新 coinsCount余额
        "teamCount": 123456, //更新 teamCount余额
        "giantCount": 123456, //更新 giantCount余额
        "zFBBalance": 123456, //更新 zFBBalance余额
        "tRXBalance": 123456 //更新 tRXBalance余额
    }
    ```

## 刷新体力
### `/refresh`
- **Method**: POST
- **Request**:
    ```json
    {
        "userid": 12345678
    }
    ```
- **Response**:
    ```json
    {
        "code": "0正常,其余的会有msg 提示错误，游戏中如需提示需要转当前选择的语言文案提示"
    }
    ```

## 刷新已存在的邀请列表
### `/invite`
- **Method**: POST
- **Request**:
    ```json
    {
        "userid": 12345678,
        "start": 0, //第几条开始，默认0,可选参数
        "end": 100 //第几条结束，默认100,可选参数
    }
    ```
- **Response**:
    ```json
    {
        "code": "0正常,其余的会有msg 提示错误，游戏中如需提示需要转当前选择的语言文案提示",
        "data": [{first_name,last_name,username,userid,headpic,ismute}],//邀请的用户集
        "count": 1, //总数
        "start": 0, //第几条开始，默认0
        "end": 100 //第几条结束，默认100
        "inviteRecordList": [
            {
                "userid": 123456789, //用户id
                "type":1,//1 邀请 2 进入频道 3消耗 4消耗TRX 5充值TRX 6购买盲盒 7转账（提现）
                "amount":10,//trx 数量
                "zFBBalance": 123456,//送自发币金额
                "physicalPower": 123456,//送体力数量
                "time": "时间戳"
            }
        ]
    }
    ```

## 任务列表
### `/task`
- **Method**: POST
- **Request**:
    ```json
    {
        "userid": 12345678
    }
    ```
- **Response**:
    ```json
    {
        "code": "0正常,其余的会有msg 提示错误，游戏中如需提示需要转当前选择的语言文案提示",
        "data": [
            {
                "id": 1,
                "desc": "任务描述",
                "type": "1 邀请 2 进入频道 3消耗 4消耗TRX 5充值TRX 6购买盲盒",
                "count": "完成任务数量",
                "gameAmount": "奖励游戏币",
                "zfbAmount": "奖励自发币",
                "trxAmount": "奖励TRX 最小",
                "trxAmountMAX": "奖励TRX 最多"
            }
        ]
    }
    ```
    ```json
    {
        "id": "任务列表",
        "desc": "任务描述",
        "type": "1 邀请 2 进入频道 3消耗 4消耗TRX 5充值TRX 6购买盲盒",
        "count": "完成任务数量",
        "gameAmount": "奖励游戏币",
        "zfbAmount": "奖励自发币",
        "trxAmount": "奖励TRX"
    }
    ```
  
## 关卡数据
### ·`/levelsData`
- **Method**: POST
- **Request**:
    ```json
    {
        "userid": 12345678
    }
    ```
- **Response**:
    ```json
    {
        "code": "0正常,其余的会有msg 提示错误，游戏中如需提示需要转当前选择的语言文案提示",
        "Enemy": Enemy, //敌方属性
        "WeaponCfg": WeaponCfg, //武器配置
        "TrapCfg": TrapCfg, //陷阱配置
        "levelConfig": levelConfig //关卡数据
    }
    ```

  * **Enemy** : 敌方属性
      ```json
      {
          //普通兵
          "0": {
              "spd": 7.2,
              "atk": 2,
              "hp": 4,
              "scale": 1.2
          },
          //炸弹
          "1": {
              "spd": 8.2,
              "atk": 2,
              "hp": 8,
              "scale": 1.2,
              "boomRadius": 2.5, //爆炸半径
              "boomAtk": 2
          },
          //刺客
          "2": {
              "spd": 15,
              "atk": 1,
              "hp": 5,
              "scale": 1.5
          },
          //巨人
          "3": {
              "spd": 7.8,
              "atk": 1,
              "hp": 15,
              "scale": 3
          },
          //Boss
          "4": {
              "spd": 8.2,
              "atk": 3,
              "hp": 32,
              "scale": 2.4
          }
      }
      ```
  * **WeaponCfg** : 武器配置: 类型顺序与 `weaponType` 一致
      ```json
      {
          //手枪
          "0": {
              "atk": 1,
              "atkSpd": 2,
              "perfab": "Pistol",
              "bullet": "mergePistolBullet",
              "bulletSpd": 20,
              "propScale": 5 //作为道具显示的缩放
          },
          //短枪
          "1": {
              "atk": 1.5,
              "atkSpd": 1,
              "perfab": "Shotgun",
              "bullet": "mergeShotgunBullet",
              "bulletSpd": 20,
              "propScale": 3 //作为道具显示的缩放
          },
          //喷火枪
          "2": {
              "atk": 4,
              "atkSpd": 1,
              "perfab": "FireGun",
              "bullet": "mergeFireGunBullet",
              "bulletSpd": 20,
              "propScale": 2 //作为道具显示的缩放
          },
          //机关枪
          "3": {
              "atk": 2,
              "atkSpd": 3,
              "perfab": "MachineGun",
              "bullet": "mergeMachineGunBullet",
              "bulletSpd?": 30,
              "propScale": 2 //作为道具显示的缩放
          },
          //手榴弹
          "4": {
              "atk": 1,
              "atkSpd": 1,
              "perfab": "Grenades",
              "bullet": " ", //todo
              "bulletSpd": 5,
              "propScale": 2, //作为道具显示的缩放
              "boomRadius": 3 //爆炸范围
          },
          //无人机
          "5": {
              "atk": 1.5,
              "atkSpd": 8,
              "perfab": "Drone",
              "bullet": "mergeDroneBullet",
              "bulletSpd": 20,
              "propScale": 2, //作为道具显示的缩放
              "droneheight": 7
          }
      }
      ```
  * **TrapCfg** : 陷阱配置: 类型顺序与 `weaponType` 一致
      ```json
      {
          //圆形电锯
          "0": {
              "atk": 15, //攻击力
              "perfab": "ElectricSaw",
              "isMuilty": false
          },
          //地刺
          "1": {
              "atk": 15,
              "perfab": "Spininess",
              "isMuilty": false
          },
          //锤子
          "2": {
              "atk": 15,
              "perfab": "Hammer",
              "isMuilty": false
          },
          //导弹
          "3": {
              "atk": 15,
              "perfab": "Rocket",
              "isMuilty": true
          },
          //炮台
          "4": {
              "atk": 15,
              "atkSpd": 10,
              "bulletType": "mergeFortBarbetteBullet",
              "perfab": "FortBarbette",
              "isMuilty": true
          },
          //高空钉
          "5": {
              "atk": 15,
              "perfab": "UpperAirNail",
              "isMuilty": false
          },
          //地雷
          "6": {
              "atk": 15,
              "perfab": "LandMine",
              "isMuilty": true
          }
      }
      ```
  * **levelConfig** : 关卡数据
      ```json
      {
          "lv": 1,
          //路段配置
          "path": ["P000", "P001", "P001", "P001", "P001", "P001", "P001", "P999"],
          //敌人
          // ['触发点Id, 敌人类型id, 最小数量, 最大数量 ']
          "enemy": [
              ["0,0,35,35"],
              ["0,0,20,20"],
              ["0,0,20,30"],
              ["0,0,20,25"],
              ["0,0,30,45"],
              ["0,0,45,45"],
              ["0,0,40,45"],
              null
          ],
          /** 道具类型:(0-武器,1-陷阱,2-人数),   道具具体分类,  道具数量 , 道具配置参数*/
          "prop": [
              null,
              null,
              [2, "x5", "+10", 0],
              [1, 0, 1, 0],
              [0, 0, 0, "3"],
              [2, "x3", "+20", 0],
              [1, 2, 1, 2],
              null
          ]
      }
      ```


## 错误码
```json
{code: 9999, msg: "维护中，请稍后再试！"}
{code: 8888, msg: "参数有误!"}
{code: 7777, msg: "服务器繁忙!"}
{code: 1001, msg: "用户或密码不对"}
{code: 1002, msg: "设置失败"}
{code: 1003, msg: "用户名或密码不能为空"}
{code: 1004, msg: "添加失败"}
{code: 1005, msg: "删除管理员失败"}
{code: 1006, msg: "修改失败"}
{code: 1007, msg: "非法请求！"}
{code: 1008, msg: "用户不存在，先到机器人@vkvGame_bot 点击 start 完成注册后继续！"}
{code: 1009, msg: '登录失败,请重试'}
{code: 2001, msg: '开始游戏失败,请重试'}
{code: 2002, msg: '拾取失败,没有邀请好友'}
{code: 2003, msg: '拾取失败,没有邀请好友'}
{code: 2004, msg: '拾取失败,超出限制'}
{code: 2005, msg: '拾取失败,请重试'}
{code: 2006, msg: '签到已经结束'}
{code: 2007, msg: '今天已经签到'}
{code: 2008, msg: '服务器繁忙,请稍后再试'}
{code: 2009, msg: '抽奖次数不足'}
{code: 3001, msg: '服务器繁忙,请稍后再试'}
{code: 3002, msg: '复活次数不足'}
{code: 4001, msg: '用户不存在'}
{code: 4002, msg: 'TRX余额不足'}
{code: 4003, msg: '转账失败，服务器繁忙'}
{code: 5001, msg: '商品不存在'}
{code: 5002, msg: '余额不足'}
```
