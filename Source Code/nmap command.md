---
title: nmap 命令
tag: 信息安全
date: 2021/04/08
---
# nmap 命令
## 主机扫描
```bash
-sL List
-sn Ping 禁用端口扫描
-P0  ip协议
-PS/PA/PU SYN/ACK/UDP
-n 不做DNS解析
```
## 扫描技巧
```bash
-sS 快速扫描 SYN
-sT tcp connect()扫描
-sA ACK
-b FTP 弹跳扫描
```
## 端口规格和扫描顺序
```bash
-p 扫描端口
-F 快速模式
-r 端口连续扫描
```
## 服务版本探测
```bash
-sV 扫描版本
--version-intensity <0-9> 指定扫描强度，默认7
--version-light: 轻度 (intensity 2)
--version-all: 强烈 (intensity 9)
```
## 系统探测
```bash
-O 打开系统探测
--osscan-limit 扫描有希望探测到系统的主机
--osscan-guess 加大力度！
```
## 防火墙绕过
```bash
-f 数据包分片发给主机
-D Cloak a scan with decoys(看起来有多个系统同时扫描)
--data-length <num> 增加随机数据到包里
```

## nmap扫描状态
- open
- close
- filtered 
- unfiltered
- unknown
- closed