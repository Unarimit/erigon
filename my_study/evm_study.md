# 如何进行一个完整的交易流程

1. 读取block
2. 从block读取交易 / 从tx pool中读取交易
3. 执行交易
4. 改变RootState (MPT or KZG?)
5. *出块

> 注意context在每个步骤的改变

## files
1. 读取交易（入口）

`eth/stagedsync/stage_execute.go` 读取区块，处理区块信息

`core/blockchain.go` 遍历区块中的交易 //ibs IntraBlockState起什么作用，ExecuteBlockEphemerally 为什么Ephemerally(短暂的)

2. 执行交易

`core/state_processor.go` 准备EVM Context(`func ApplyTransaction`)，处理交易(`func applyTransaction`)

调用函数传入tx的`AsMessage`方法完成交易的执行 // 函数内部只能索引到接口

> `core/vm/instructions.go` 存储了每个opcode对应的操作

3. 改变State / 验证State

在执行交易`core/state_processor.go`的后半段

4. 出块