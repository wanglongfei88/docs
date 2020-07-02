# 智能合约框架

NEO 智能合约框架是对智能合约开发中使用的 API 的封装，使C#智能合约开发者可以直接使用 Neo核心模块开发给智能合约使用的类、方法、属性来方便地与Neo区块链交互，进而获得区块链账本数据、操作持久化存储区和NeoVM的执行状况等信息。

Neo.SmartContract.Framework 提供了以下几种比较重要的API方法集：

+ 互操作服务的方法
+ 常用方法

## 互操作服务层的方法

互操作服务层提供的API包含在以下命名空间：

+ **Neo.SmartContract.Framework.Services.NEO** 

  Neo 命名空间是 Neo 区块链所提供的 API，提供了访问区块链账本数据的和操作持久化存储区的方法。

  | 类                                                    | 说明                                       |
  | ----------------------------------------------------- | ------------------------------------------ |
  | [Account](neo/Account.md)                             | 表示账户的类，提供了查询余额的方法         |
  | [Asset](neo/Asset.md)                                 | 用来表示资产的数据结构                     |
  | [Block](neo/Block.md)                                 | 表示区块的类，提供了查询区块中交易的方法   |
  | [Blockchain](neo/Blockchain.md)                       | 该类提供了访问区块链数据的一系列方法       |
  | [Contract](neo/Contract.md)                           | 表示合约的类                               |
  | [Header](neo/Header.md)                               | 用来表示区块头的数据结构                   |
  | [InvocationTransaction](neo/InvocationTransaction.md) | 用来表示调用合约交易的类                   |
  | [Iterator](neo/Iterator.md)                           | 用来表示枚举器的类                         |
  | [Runtime](neo/Runtime.md)                             | 提供智能合约运行时的一些方法               |
  | [Storage](neo/Storage.md)                             | 提供了持久化存储区的插入、查询、删除的方法 |
  | [StorageContext](neo/StorageContext.md)               | 用来表示私有存储区存储上下文的类           |
  | [StorageMap](neo/StorageMap.md)                       | 用来表示 Map 数据结构的类                  |
  | [Transaction](neo/Transaction.md)                     | 用来表示交易的基类                         |
  | [TransactionAttribute](neo/TransactionAttribute.md)   | 用来表示交易特性的数据结构                 |
  | [TransactionInput](neo/TransactionInput.md)           | 用来表示交易输入的数据结构                 |
  | [TransactionOutput](neo/TransactionOutput.md)         | 用来表示交易输出的数据结构                 |

  | **枚举**                                              | **说明**                       |
  | ----------------------------------------------------- | ------------------------------ |
  | [ContractPropertyState](neo/ContractPropertyState.md) | 用来表示智能合约属性状态的枚举 |
  | [TriggerType](neo/TriggerType.md)                     | 用来表示智能合约触发条件的枚举 |

+ **Neo.SmartContract.Framework.Services.System** 

  System 命名空间是智能合约执行引擎（NeoVM）提供的 API，提供了访问访问该智能合约的执行环境的方法。

  | 类                                           | 说明                                                 |
  | -------------------------------------------- | ---------------------------------------------------- |
  | [ExecutionEngine](System/ExecutionEngine.md) | 虚拟机的执行引擎，可以获取当前合约的调用者和执行容器 |

## Neo提供的常用方法

在智能合约中除了可以调用互操作服务层中的方法，还可以调用智能合约框架本身提供的常用方法。这些方法直接归属于 Neo.SmartContract.Framework 命名空间，可以在智能合约中可以直接使用这些方法。

#### SmartContract类提供的方法

SmartContract 类提供了一些散列算法以及验签方法，通过继承SmartContract类来使用这类方法。

| 名称                                                         | 说明                                                        |
| ------------------------------------------------------------ | ----------------------------------------------------------- |
| Sha1(byte[])                                                 | 对传入的 byte 数组进行 Sha1 运算                            |
| Sha256(byte[])                                               | 对传入的 byte 数组进行 Sha256 运算                          |
| Hash160(byte[])                                              | 对传入的 byte 数组进行 Sha256 运算后，再进行 Ripemd160 运算 |
| Hash256(byte[])                                              | 对传入的 byte 数组进行两次 Sha256 运算                      |
| VerifySignature(byte[] signature, byte[] pubkey)             | 通过公钥和已签名的数据来验证验证是否通过                    |
| VerifySignature(byte[] message, byte[] signature, byte[] pubkey); | 验证签名                                                    |
| VerifySignatures(byte[][] signature, byte[][] pubkey);       | 验证多签                                                    |

>  [!Note]
>
> 以下方法通过继承SmartContract类获得。如果找不到这些方法，请检查你的类是否继承自 SmartContract 类。

### Helper扩展方法

下面的这些方法是智能合约框架中的 Helper 类提供的一些 ` 扩展方法 `。

| 名称                                   | **说明**                                                     |
| -------------------------------------- | ------------------------------------------------------------ |
| **不同数据类型的转换**                 |                                                              |
| byte[] AsByteArray(source)             | 源数据 => byte[]，支持：<br />byte, byte[], sbyte, sbyte[], BigInteger, string, |
| byte[] HexToBytes(string hex)          | Hex字符串 => byte[]                                          |
| BigInteger AsBigInteger(byte[] source) | byte[] => BigInteger                                         |
| BigInteger ToBigInteger( source)       | byte[] => BigInteger<br />string => BigInteger               |
| string AsString(byte[] source)         | byte[] => string                                             |
| byte ToByte(source)                    | BigInteger => byte<br />int => byte                          |
| byte[] ToScriptHash(string address)    | 钱包地址 => ScriptHash                                       |
|                                        |                                                              |
| **Byte数组相关**                       |                                                              |
| Concat(byte[], byte[])                 | 连接两个 byte 数组                                           |
| Range(byte[], int, int)                | 截取 byte 数组，参数为：index, count                         |
| Take(byte[], int)                      | 从 byte 数组中取左侧固定长度的 byte 数组，参数为：count      |
| byte[] Last(byte[] source, int count)  | 获取字节数组的最后一个元素                                   |
| byte[] Reverse(byte[] source)          | 逆转字节数组                                                 |
|                                        |                                                              |
| **系列化**                             |                                                              |
| byte[] Serialize(object source)        | 系列化对象为字节数组                                         |
| object Deserialize(byte[] source)      | 反系列化字节数组为对象                                       |