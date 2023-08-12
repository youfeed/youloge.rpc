# Youloge.RPC 规范 
创建时间：2023-08-13 02:29:24 
更新时间：2023-08-13 02:29:31 
作者：Micateam

# 概述
Youloge.RPC 是一个有状态，需要路由匹配的，轻量级远程调用协议。它非常适合用在前端-后端，后端-后端，代理-节点等方面使用。

# 约定
- 主域名 `https://api.youloge.com` `https://vip.youloge.com`
- 请求路径 `path`
- 请求方式 `POST`
- 请求头 `Ukey` | 'Signer'
- 请求体 `{"method":"","params":{}[]}`

## 简单请求
``` 
--> login
{"method":"profile","params":{"uuid":"userID"}}
<-- login
{"err":200,"msg":"success","data":{"uuid":"userID","name":"name"...}}
```
* 完整请求URL为 `https://api.youloge.com/login`

## 批量调用
``` 
--> login
{"method":"profile","params":[{"uuid":"userID001"},{"uuid":"userID002"}...]}
<-- login
{"err":200,"msg":"success","data":[{"uuid":"userID001","name":"name001"...},{"uuid":"userID002","name":"name002"...}]}
```
* 完整请求URL为 `https://api.youloge.com/login`

## 开放接口调用
``` 
--> login
{"method":"verify","params":{"sign":"sign"}}
<-- login
{"err":200,"msg":"success","data":{"uuid":"userID","verify":"verifys"...}}
{"err":401,"msg":"Ukey No Found"}
```
* 完整请求URL为 `https://api.youloge.com/login` 请求头加入`Ukey:*************************`

## 私有接口调用
``` 
--> payment
{"method":"verify","params":{"sign":"sign"}}
<-- login
{"err":200,"msg":"success","data":{"uuid":"userID","verify":"verifys"...}}
{"err":402,"msg":"Signer bind IP"}
{"err":403,"msg":"Signer is Expired"}
```
* 完整请求URL为 `https://vip.youloge.com/payment` 请求头加入`Signer:*************************`







