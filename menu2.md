# erigon下的项目文件夹
+---accounts
+---cl
+---cmd
+---common
+---consensus
+---core
+---crypto
+---eth
+---ethdb
+---ethstats
+---event
+---hive
+---hooks
+---k8s
+---metrics
+---migrations
+---node
+---p2p
+---params
+---rlp
+---rpc
+---tests
+---turbo
+---visual

部分geth中的目录结构参考：https://blog.csdn.net/lj900911/article/details/83449858

## accounts*
from geth，只包含abi文件夹，先不管
> ABI全称 Application Binary Interface，字面意思是应用程序二进制接口，可以通俗的理解为合约的接口说明，当合约被编译后，它对应的abi也就确定了。
> 在合约的执行中中没有作用
> 在合约编译时生成的json文件(abi)起到接口文档的作用

from: https://blog.csdn.net/weixin_33717117/article/details/88708396

## cl*
from erigon, 不知道是干什么的，好像和SSZ有关（从函数命名和提交可以看出），先不管
> Eth 2.0 - 简单的序列化 Simple Serialize (SSZ) 是一种结构化数据编码和默克尔化的标准，专为 ETH 2.0 设计

## cmd
其中包括了启动客户端、执行合约等一些命令，可以被认为是一个入口，可以从这里详细看evm的代码。
> 除了cmd文件夹会被编译成二进制，其他都是库？

