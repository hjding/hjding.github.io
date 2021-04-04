# SNMP/UDP端口




![2_SNMP流程](D:\Hugo\my_website\content\images\2_SNMP流程.png)

## 公有mib

snmp udp端口161/162

## 私有mib

snmp管理请求（src随机x/dst161） 
snmp代理回复（src161/dst随机x）



### 从snmp管理的角度看

随机端口x收发请求+162收trap
使用随机端口x应该是为了减轻snmp管理请求的io压力，使用162专门获取trap

### 从snmp代理的角度看

161收发请求+161发trap

使用src161发送消息，不管是snmp管理的请求，还是snmp代理主动上报的trap，因为snmp代理相当于管理的一个node，io压力相对来说不是很大

## trap

snmp代理主动上报（src161/dst162）
