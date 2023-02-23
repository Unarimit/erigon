# 学习zksync中的智能合约

## 从Verifier.sol开始
1. 关键验证合约，代码中verify_serialized_proof_with_recursion的内容 
    - Verifier继承KeysWithPlonkVerifier //Verifier.sol
    - KeysWithPlonkVerifier继承VerifierWithDeserialize //该合约不在zksync仓库中，https://github.com/matter-labs/recursive_aggregation_circuit/blob/master/contract/KeysWithPlonkVerifier.sol
    - VerifierWithDeserialize继承Plonk4VerifierWithAccessToDNext //PlonkCore.sol
    - verify_serialized_proof_with_recursion调用verify_recursive函数 //PlonkCore.sol
    - Plonk4VerifierWithAccessToDNext中有verify_recursive函数 //PlonkCore.sol
2. 很难从合约代码(验证过程)中看出什么东西。最多是对输入数据做了一系列处理，然后使用plonk库中的pair方法校验。
    - 还是需要从输入内容出发，看函数究竟对什么东西进行验证
3. https://github.com/matter-labs/recursive_aggregation_circuit 应该包含证明的生成部分。但验证部分不知道，rust代码不好看。