# 如何进行一个完整的交易流程
1. 读取block
2. 从block读取交易 / 从tx pool中读取交易 
3. 执行交易
4. 改变RootState (MPT or KZG?)
5. *出块

> 1步骤跟geth差别还挺大的，会做相应的记录

> 注意context在每个步骤的改变

## 需要关注的部分
1. 重要的结构体（block的结构、tx的结构、msg的结构）
2. 对数据库的访问（改变state需要的数据有哪些、处理和验证交易需要哪些数据支撑，在哪一步对数据库读取）
3. 数据流的变化（block -> transaction-> contract or tx -> state change info）


## files
1. 读取交易（入口）
- geth

    `miner/woker.go`：传递交易池、挖矿时的交易

    `core/state_processor.go` 中的 `func Process`：传递区块中的交易

- erigon

    `eth/stagedsync/stage_execute.go` 中的 `func SpawnExecuteBlocksStage`、`func executeBlock`：读取区块，处理区块信息
    
    > 这个方法是并行的

    `core/blockchain.go`的`func ExecuteBlockEphemerally`系列：遍历区块中的交易，传递交易 //ibs IntraBlockState起什么作用，ExecuteBlockEphemerally 为什么Ephemerally？(短暂的)


2. 执行交易

    `core/state_processor.go` 准备EVM Context(`func ApplyTransaction`)，处理交易(`func applyTransaction`)

    调用函数传入tx的`AsMessage`方法完成交易的执行 // 函数内部只能索引到接口

    > `core/vm/instructions.go` 存储了每个opcode对应的操作

3. 改变State / 验证State

    在执行交易`core/state_processor.go`的后半段

4. 出块