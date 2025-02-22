## 기본 블록 매개변수 <a id="the-default-block-parameter"></a>

Klaytn 상태 상에서 어떤 행위에 대한 요청이 있을 때 마지막의 기본 블록 매개변수가 블록의 번호를 결정합니다.

`defaultBlock` 매개변수를 통해 설정할 수 있는 사항들은 다음과 같습니다.

- `16진수 문자열` - 블록 번호의 정수 형태입니다.
- `"earliest" 문자열` - 제네시스 블록입니다.
- `"latest" 문자열` - 가장 최근에 채굴된 블록입니다.
- `"pending" 문자열` - 보류 중인 상태/트랜잭션입니다.


## klay_blockNumber <a id="klay_blocknumber"></a>

가장 최근의 블록 번호를 반환합니다.

**파라미터**

없음

**리턴값**

| 타입       | 설명                            |
| -------- | ----------------------------- |
| QUANTITY | 클라이언트가 있는 현재 블록 번호의 정수 형태입니다. |

**예시**

```shell
// Request
curl -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"klay_blockNumber","params":[],"id":83}' https://api.baobab.klaytn.net:8651

// Result
{
  "jsonrpc": "2.0",
  "id":83,
  "result": "0xc94"
}
```


## klay_getHeaderByNumber <a id="klay_getheaderbynumber"></a>

**참고**: 이 API는 Klaytn v1.7.0.부터 지원됩니다.

블록 번호를 기준으로 헤더 정보를 반환합니다. 이 API는 RPC 호출로만 작동하며 자바스크립트 콘솔을 통해서는 작동하지 않습니다.

**파라미터**

| 타입                  | 설명                                                                                                                          |
| ------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| QUANTITY &#124; TAG | 정수 형태의 블록 번호 또는 [기본 블록 매개변수](#the-default-block-parameter)에서와 같이 `"earliest"`, `"latest"`, `"pending"`과 같이 상태를 나타내는 문자열입니다. |

**리턴값**

[klay_getBlockByHash](#klay_getheaderbyhash)를 참고하세요.

**예시**

```shell
// Request
curl -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"klay_getHeaderByNumber","params":["0x1b4"],"id":1}' https://api.baobab.klaytn.net:8651
// Result
{
  "jsonrpc":"2.0",
  "id":1,
  "result":{
    "baseFeePerGas":"0x5d21dba00",
    "blockScore":"0x1",
    "extraData":"0xda83010800846b6c617989676f312e31362e31338664617277696e0000000000f89ed5949712f943b296758aaae79944ec975884188d3a96b841ddfdf7e2cb0a93538f757f87f23a93ee35df703c781c6f15e31e4978ecdfb3501fc00924372b9a01df2bc452f2a924c242d83580183d131c47e49a25b78f625201f843b841b9b6034d5a8c5f5b057274cda4f427614cd1f448ee781f4c4322861d1361d09d47d6030f2b69a26cb426db984f54e71f8c112fbf882930ccd715d595e8d8307500",
    "gasUsed":"0x0",
    "governanceData":"0x",
    "hash":"0xe882d7a16f38126dc0c507f990b3fe18fa2d3a380002538581327abe96ca6edc",
    "logsBloom":"0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
    "number":"0x1e67",
    "parentHash":"0x28b1c054346c3bd083741c757a750dcabf94b6d50c7f87158753544e96e73550",
    "receiptsRoot":"0xc5d2460186f7233c927e7db2dcc703c0e500b653ca82273b7bfad8045d85a470",
    "reward":"0x4b2c736fd05c2e2da3ccbd001a395a444f16a861",
    "stateRoot":"0xdf9885621c9e6e75912ca94d6987bcb1b54fef0e4a99cbec5e68f1ffc7468a78",
    "timestamp":"0x62130beb",
    "timestampFoS":"0x0",
    "transactionsRoot":"0xc5d2460186f7233c927e7db2dcc703c0e500b653ca82273b7bfad8045d85a470"
  }

}
```

## klay_getHeaderByHash <a id="klay_getheaderbyhash"></a>

**참고**: 이 API는 Klaytn v1.7.0.부터 지원됩니다.

블록 해시를 기준으로 헤더의 정보를 반환합니다. 이 API는 RPC 호출로만 작동하며 자바스크립트 콘솔을 통해서는 작동하지 않습니다.

**파라미터**

| 타입            | 설명         |
| ------------- | ---------- |
| 32바이트 크기 DATA | 블록의 해시입니다. |

**리턴값**

`객체` - 헤더 객체, 또는 블록이 없는 경우 `error`를 반환합니다.

| 이름               | 타입             | 설명                                                                                                          |
| ---------------- | -------------- | ----------------------------------------------------------------------------------------------------------- |
| number           | QUANTITY       | 블록 번호입니다. 아직 보류 중인 블록이면 `null`입니다.                                                                          |
| parentHash       | 32바이트 크기 DATA  | The hash of the parent block.                                                                               |
| logsBloom        | 256바이트 크기 DATA | 블록의 로그를 위한 블룸필터입니다. 아직 보류 중인 블록이면 `null`입니다.                                                                |
| transactionsRoot | 32바이트 크기 DATA  | 블록의 트랜잭션 트라이의 루트 해시입니다.                                                                                     |
| stateRoot        | 32바이트 크기 DATA  | 블록의 상태 트라이의 루트 해시입니다.                                                                                       |
| receiptsRoot     | 32바이트 크기 DATA  | 블록의 영수증 트라이의 루트 해시입니다.                                                                                      |
| reward           | 20바이트 크기 DATA  | 블록 보상을 받을 수혜자의 주소입니다.                                                                                       |
| blockScore       | QUANTITY       | 이전 난이도입니다. BFT 합의 엔진에서는 항상 1입니다.                                                                            |
| extraData        | DATA           | 블록의 "추가 데이터"를 위한 필드입니다.                                                                                     |
| gasUsed          | QUANTITY       | 블록에 있는 트랜잭션들에서 사용된 가스양의 총합입니다.                                                                              |
| timestamp        | QUANTITY       | 블록이 생성되었을 때의 Unix 타임스탬프입니다.                                                                                 |
| timestampFoS     | QUANTITY       | 블록이 생성되었을 때의 타임스탬프 중 초 단위 부분입니다.                                                                            |
| governanceData   | DATA           | RLP 인코딩된 거버넌스 설정입니다.                                                                                        |
| voteData         | DATA           | 제안자의 RLP 인코딩된 거버넌스 투표입니다.                                                                                   |
| baseFeePerGas    | QUANTITY       | The base fee per gas. It has a meaningful value when EthTxTypeCompatible and Magma hardforks are activated. |

**예시**

```shell
// Request
curl -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"klay_getHeaderByHash","params":["0xb8deae63002d2b6aa33247c8ef545383ee0fd2282ac9b49dbbb74114389ddb5c"],"id":1}' https://api.baobab.klaytn.net:8651
// Result
{
  "jsonrpc":"2.0",
  "id":1,
  "result":{
    "baseFeePerGas":"0x5d21dba00",
    "blockScore":"0x1",
    "extraData":"0xda83010800846b6c617989676f312e31362e31338664617277696e0000000000f89ed5949712f943b296758aaae79944ec975884188d3a96b841ddfdf7e2cb0a93538f757f87f23a93ee35df703c781c6f15e31e4978ecdfb3501fc00924372b9a01df2bc452f2a924c242d83580183d131c47e49a25b78f625201f843b841b9b6034d5a8c5f5b057274cda4f427614cd1f448ee781f4c4322861d1361d09d47d6030f2b69a26cb426db984f54e71f8c112fbf882930ccd715d595e8d8307500",
    "gasUsed":"0x0",
    "governanceData":"0x",
    "hash":"0xe882d7a16f38126dc0c507f990b3fe18fa2d3a380002538581327abe96ca6edc",
    "logsBloom":"0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
    "number":"0x1e67",
    "parentHash":"0x28b1c054346c3bd083741c757a750dcabf94b6d50c7f87158753544e96e73550",
    "receiptsRoot":"0xc5d2460186f7233c927e7db2dcc703c0e500b653ca82273b7bfad8045d85a470",
    "reward":"0x4b2c736fd05c2e2da3ccbd001a395a444f16a861",
    "stateRoot":"0xdf9885621c9e6e75912ca94d6987bcb1b54fef0e4a99cbec5e68f1ffc7468a78",
    "timestamp":"0x62130beb",
    "timestampFoS":"0x0",
    "transactionsRoot":"0xc5d2460186f7233c927e7db2dcc703c0e500b653ca82273b7bfad8045d85a470"
  }

}
```


## klay_getBlockByNumber <a id="klay_getblockbynumber"></a>

블록 번호로 조회한 블록의 정보를 반환합니다. 이 API는 RPC 호출로만 작동하며 자바스크립트 콘솔을 통해서는 작동하지 않습니다.

**파라미터**

| 타입                  | 설명                                                                                                                          |
| ------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| QUANTITY &#124; TAG | 정수 형태의 블록 번호 또는 [기본 블록 매개변수](#the-default-block-parameter)에서와 같이 `"earliest"`, `"latest"`, `"pending"`과 같이 상태를 나타내는 문자열입니다. |
| Boolean             | `true`이면 트랜잭션 객체 전체를 반환하고, `false`이면 트랜잭션의 해시만을 반환합니다.                                                                      |

{% hint style="success" %}
참고: Klaytn v1.7.0 이전 버전에서는 정수형 블록 번호나 `"earliest"`, `"latest"` 같은 문자열만 사용할 수 있습니다.
{% endhint %}

**리턴값**

See [klay_getBlockByHash](#klay_getblockbyhash)

**예시**

```shell
// Request
curl -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"klay_getBlockByNumber","params":["0x1b4", true],"id":1}' https://api.baobab.klaytn.net:8651

// Result
{
  "jsonrpc":"2.0",
  "id":1,
  "result":{
    "baseFeePerGas":"0x5d21dba00",
    "blockscore":"0x1",
    "extraData":"0xda83010800846b6c617989676f312e31362e31338664617277696e0000000000f89ed5949712f943b296758aaae79944ec975884188d3a96b841ddfdf7e2cb0a93538f757f87f23a93ee35df703c781c6f15e31e4978ecdfb3501fc00924372b9a01df2bc452f2a924c242d83580183d131c47e49a25b78f625201f843b841b9b6034d5a8c5f5b057274cda4f427614cd1f448ee781f4c4322861d1361d09d47d6030f2b69a26cb426db984f54e71f8c112fbf882930ccd715d595e8d8307500",
    "gasUsed":"0x0",
    "governanceData":"0x",
    "hash":"0xe882d7a16f38126dc0c507f990b3fe18fa2d3a380002538581327abe96ca6edc",
    "logsBloom":"0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
    "number":"0x1e67",
    "parentHash":"0x28b1c054346c3bd083741c757a750dcabf94b6d50c7f87158753544e96e73550",
    "receiptsRoot":"0xc5d2460186f7233c927e7db2dcc703c0e500b653ca82273b7bfad8045d85a470",
    "reward":"0x4b2c736fd05c2e2da3ccbd001a395a444f16a861",
    "size":"0x272",
    "stateRoot":"0xdf9885621c9e6e75912ca94d6987bcb1b54fef0e4a99cbec5e68f1ffc7468a78",
    "timestamp":"0x62130beb",
    "timestampFoS":"0x0",
    "totalBlockScore":"0x1e68",
    "transactions":[],
    "transactionsRoot":"0xc5d2460186f7233c927e7db2dcc703c0e500b653ca82273b7bfad8045d85a470",
    "voteData":"0x"
  }
}
```


## klay_getBlockByHash <a id="klay_getblockbyhash"></a>

블록 해시를 기준으로 블록의 정보를 반환합니다. 이 API는 RPC 호출로만 작동하며 자바스크립트 콘솔을 통해서는 작동하지 않습니다.

**파라미터**

| 타입            | 설명                                                     |
| ------------- | ------------------------------------------------------ |
| 32바이트 크기 DATA | 블록의 해시입니다.                                             |
| Boolean       | `true`이면 트랜잭션 객체 전체를 반환하고, `false`이면 트랜잭션의 해시만을 반환합니다. |

**리턴값**

`Object` - A block object, or `error` when no block was found:

| 이름               | 타입             | 설명                                                                                                          |
| ---------------- | -------------- | ----------------------------------------------------------------------------------------------------------- |
| number           | QUANTITY       | 블록 번호입니다. 아직 보류 중인 블록이면 `null`입니다.                                                                          |
| 해시               | 32바이트 크기 DATA  | 블록의 해시입니다. 아직 보류 중인 블록이면 `null`입니다.                                                                         |
| parentHash       | 32바이트 크기 DATA  | 이전 블록의 해시입니다.                                                                                               |
| logsBloom        | 256바이트 크기 DATA | 블록의 로그를 위한 블룸필터입니다. 아직 보류 중인 블록이면 `null`입니다.                                                                |
| transactionsRoot | 32바이트 크기 DATA  | 블록의 트랜잭션 트라이의 루트 해시입니다.                                                                                     |
| stateRoot        | 32바이트 크기 DATA  | 블록의 상태 트라이의 루트 해시입니다.                                                                                       |
| receiptsRoot     | 32바이트 크기 DATA  | 블록의 영수증 트라이의 루트 해시입니다.                                                                                      |
| reward           | 20바이트 크기 DATA  | 블록 보상을 받을 수혜자의 주소입니다.                                                                                       |
| blockScore       | QUANTITY       | 이전 난이도입니다. BFT 합의 엔진에서는 항상 1입니다.                                                                            |
| totalBlockScore  | QUANTITY       | 본 블록까지 체인 내 모든 블록의 blockScore 값의 합입니다.                                                                      |
| extraData        | DATA           | 블록의 "추가 데이터"를 위한 필드입니다.                                                                                     |
| size             | QUANTITY       | 블록의 바이트 크기의 정수 형태입니다.                                                                                       |
| gasUsed          | QUANTITY       | 블록에 있는 트랜잭션들에서 사용된 가스양의 총합입니다.                                                                              |
| timestamp        | QUANTITY       | 블록이 생성되었을 때의 Unix 타임스탬프입니다.                                                                                 |
| timestampFoS     | QUANTITY       | 블록이 생성되었을 때의 타임스탬프 중 초 단위 부분입니다.                                                                            |
| transactions     | Array          | 트랜잭션 객체의 배열이거나 또는 마지막으로 주어진 매개변수에 따라 32바이트 크기의 트랜잭션 해시입니다.                                                  |
| governanceData   | DATA           | RLP 인코딩된 거버넌스 설정입니다.                                                                                        |
| voteData         | DATA           | 제안자의 RLP 인코딩된 거버넌스 투표입니다.                                                                                   |
| baseFeePerGas    | QUANTITY       | The base fee per gas. It has a meaningful value when EthTxTypeCompatible and Magma hardforks are activated. |

**예시**

```shell
// Request
curl -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"klay_getBlockByHash","params":["0xb8deae63002d2b6aa33247c8ef545383ee0fd2282ac9b49dbbb74114389ddb5c", true],"id":1}' https://api.baobab.klaytn.net:8651

// Result
{
  "jsonrpc":"2.0",
  "id":1,
  "result":{
    "baseFeePerGas":"0x0",
    "blockscore":"0x1",
    "extraData":"0xda83010800846b6c617989676f312e31362e31338664617277696e0000000000f89ed5949712f943b296758aaae79944ec975884188d3a96b841ddfdf7e2cb0a93538f757f87f23a93ee35df703c781c6f15e31e4978ecdfb3501fc00924372b9a01df2bc452f2a924c242d83580183d131c47e49a25b78f625201f843b841b9b6034d5a8c5f5b057274cda4f427614cd1f448ee781f4c4322861d1361d09d47d6030f2b69a26cb426db984f54e71f8c112fbf882930ccd715d595e8d8307500",
    "gasUsed":"0x0",
    "governanceData":"0x",
    "hash":"0xe882d7a16f38126dc0c507f990b3fe18fa2d3a380002538581327abe96ca6edc",
    "logsBloom":"0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
    "number":"0x1e67",
    "parentHash":"0x28b1c054346c3bd083741c757a750dcabf94b6d50c7f87158753544e96e73550",
    "receiptsRoot":"0xc5d2460186f7233c927e7db2dcc703c0e500b653ca82273b7bfad8045d85a470",
    "reward":"0x4b2c736fd05c2e2da3ccbd001a395a444f16a861",
    "size":"0x272",
    "stateRoot":"0xdf9885621c9e6e75912ca94d6987bcb1b54fef0e4a99cbec5e68f1ffc7468a78",
    "timestamp":"0x62130beb",
    "timestampFoS":"0x0",
    "totalBlockScore":"0x1e68",
    "transactions":[],
    "transactionsRoot":"0xc5d2460186f7233c927e7db2dcc703c0e500b653ca82273b7bfad8045d85a470",
    "voteData":"0x"
  }
}
```


## klay_getBlockReceipts <a id="klay_getblockreceipts"></a>

블록 해시로 조회한 블록에 포함된 영수증을 반환합니다.

**파라미터**
| 타입            | 설명         |
| ------------- | ---------- |
| 32바이트 크기 DATA | Block hash |

**리턴값**

Receipts included in a block.  If the target block contains no transaction, an empty array `[]` is returned.

**예시**

```shell
// Request
curl -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0", "method":"klay_getBlockReceipts", "params":["0xdc762ed0274496e2a42278e2648d910d82468687b5415bb5eb058a96a0b93c30"],"id":73}' https://api.baobab.klaytn.net:8651

// Result
{
  "jsonrpc":"2.0",
  "id":73,
  "result":[{
    "blockHash":"0xdc762ed0274496e2a42278e2648d910d82468687b5415bb5eb058a96a0b93c30",
    "blockNumber":"0x3ba38",
    "contractAddress":null,
    "effectiveGasPrice":"0x5d21dba00",
    "from":"0x16b11cf9c2186a117b0da38315b42b1eaa03bbe5",
    "gas":"0x30d40",
    "gasPrice":"0xba43b7400",
    "gasUsed":"0x1886c",
    "logs":[],
    "logsBloom":"0x00000000000000000000000000000000008000000000000000000000000000080000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000080000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000004000000000000040000080000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
    "nonce":"0x58e",
    "senderTxHash":"0x234469b3d3222657c98904deaba7ec6613161ea9405275025f4784a4d9918af5",
    "signatures":["0x7f6","0x50b2b0f95b8a6d7018369b1933d6cebb52ef119463d1840a6181d05bf8fc29d8","0x329630f88d9d06c5f1bd7644dbf6bd6b92e4ab0e3d47122972f8294c9289e7bb"],
    "status":"0x1",
    "to":"0xdbb98c72e9818ad2c93a09e35ad43ada0d4223f0",
    "transactionHash":"0x234469b3d3222657c98904deaba7ec6613161ea9405275025f4784a4d9918af5",
    "transactionIndex":"0x0",
    "type":"TxTypeValueTransfer",
    "typeInt":8,
    "value":"0x21e19e0c9bab2400000"
  }
}
```


## klay_getBlockTransactionCountByNumber <a id="klay_getblocktransactioncountbynumber"></a>

블록 번호로 조회한 블록에 담긴 트랜잭션의 개수를 반환합니다.

**파라미터**

| 타입                  | 설명                                                                                                                                                        |
| ------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| QUANTITY &#124; TAG | 정수 형태의 블록 번호 또는  `"earliest"`, `"latest"`, `"pending"`과 같이 상태를 나타내는 문자열입니다. 이 매개변수에 대한 자세한 설명은 [기본 블록 매개변수](block.md#the-default-block-parameter)를 참고하세요. |

{% hint style="success" %}
참고: Klaytn v1.7.0 이전 버전에서는 정수형 블록 번호나 `"earliest"`, `"latest"` 같은 문자열만 사용할 수 있습니다.
{% endhint %}

**리턴값**

| 타입       | 설명                           |
| -------- | ---------------------------- |
| QUANTITY | 이 블록에 담긴 트랜잭션의 개수의 정수 형태입니다. |

**예시**

```shell
// Request
curl -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"klay_getBlockTransactionCountByNumber","params":["0xe8"],"id":1}' https://api.baobab.klaytn.net:8651

// Result
{
  "jsonrpc": "2.0",
  "id":1,
  "result": "0xa" // 10
}
```


## klay_getBlockTransactionCountByHash <a id="klay_getblocktransactioncountbyhash"></a>

블록 해시를 기준으로 조회한 특정 블록에 담긴 트랜잭션의 개수를 반환합니다.

**파라미터**

| 타입            | 설명         |
| ------------- | ---------- |
| 32바이트 크기 DATA | 블록의 해시입니다. |

**리턴값**

| 타입       | 설명                           |
| -------- | ---------------------------- |
| QUANTITY | 이 블록에 담긴 트랜잭션의 개수의 정수 형태입니다. |

**예시**

```shell
// Request
curl -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"klay_getBlockTransactionCountByHash","params":["0x0c11803ab36110db993e7520908b9ba9336cca2f2dcc9b6130c481a3ccdc2621"],"id":1}' https://api.baobab.klaytn.net:8651

// Result
{
  "jsonrpc": "2.0",
  "id":1,
  "result": "0x0"
}
```


## klay_getBlockWithConsensusInfoByNumber <a id="klay_getblockwithconsensusinfobynumber"></a>
Returns a block with consensus information that matches the given block number.

**파라미터**

| 타입                  | 설명                                                                                                                                                       |
| ------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| QUANTITY &#124; TAG | Integer or hexadecimal block number, or the string `"earliest"` or `"latest"` as in the [default block parameter](block.md#the-default-block-parameter). |

{% hint style="success" %}
참고: Klaytn v1.7.0 이전 버전에서는 정수형 블록 번호나 `"earliest"`, `"latest"` 같은 문자열만 사용할 수 있습니다.
{% endhint %}

**리턴값**

See [klay_getBlockWithConsensusInfoByHash](#klay_getblockwithconsensusinfobyhash)

**예시**

```shell
// Request
curl -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0", "method":"klay_getBlockWithConsensusInfoByNumber", "params":["0x6e0431"],"id":73}' https://api.baobab.klaytn.net:8651

// Result
{
  "jsonrpc": "2.0",
  "id": 73,
  "result": {
    "baseFeePerGas":"0x5d21dba00",
    "blockscore": "0x1",
    "committee": ["0xe783fc94fddaeebef7293d6c5864cff280f121e1", "0x8a88a093c05376886754a9b70b0d0a826a5e64be", "0xf113ec8c22765d485309cf1d025d1b975245b9f8", "0xe3d92072d8b9a59a0427485a1b5f459271df457c", "0xa2ba8f7798649a778a1fd66d3035904949fec555", "0x2bdd279522b8a0843831fbb94cfbb24a913597c5", "0x9419fa2e3b9eb1158de31be66c586a52f49c5de7", "0xc032c34cb9fe064fe435199e1078dd8756a166b5", "0x56e8c1463c341abf8b168c3079ea41ce8a387e18", "0x6873352021fe9226884616dc6f189f289aeb0cc5", "0xe93a890fb7ec5e993b1a7fd77b0d13a0763eff3d", "0xbca8ffa45cc8e30bbc0522cdf1a1e0ebf540dfe2", "0x386ca3cb8bb13f48d1a6adc1fb8df09e7bb7f9c8", "0x1782834bf8847e235f21f2c1f13fca4d5dff6621", "0x6f6770f1f67f44fb15b335b49581ad6b935d963a", "0x0b59cae1f03534209fdb9ddf5ea65b310cd7060c", "0xb9456fd65a6810b19df24832c50b2e61a41867f8", "0x16c192585a0ab24b552783b4bf7d8dc9f6855c35", "0xec6c1cede510be308f0fdbbc8dbdf238829bdb34", "0xf8c9c61c5e7f2b6219d1c28b94e5cb3cdc802594", "0x5e59db28cef098d5a2e877f84127aed10d7378f2", "0x52d41ca72af615a1ac3301b0a93efa222ecc7541"],
    "extraData": "0xd883010101846b6c617988676f312e31322e35856c696e757800000000000000f90604f901ce9452d41ca72af615a1ac3301b0a93efa222ecc7541948a88a093c05376886754a9b70b0d0a826a5e64be94f113ec8c22765d485309cf1d025d1b975245b9f894e3d92072d8b9a59a0427485a1b5f459271df457c94a2ba8f7798649a778a1fd66d3035904949fec555942bdd279522b8a0843831fbb94cfbb24a913597c594bca8ffa45cc8e30bbc0522cdf1a1e0ebf540dfe294c032c34cb9fe064fe435199e1078dd8756a166b59456e3a565e31f8fb0ba0b12c03355518c64372120946f6770f1f67f44fb15b335b49581ad6b935d963a94e93a890fb7ec5e993b1a7fd77b0d13a0763eff3d94e783fc94fddaeebef7293d6c5864cff280f121e194386ca3cb8bb13f48d1a6adc1fb8df09e7bb7f9c8941782834bf8847e235f21f2c1f13fca4d5dff6621949419fa2e3b9eb1158de31be66c586a52f49c5de7940b59cae1f03534209fdb9ddf5ea65b310cd7060c94b9456fd65a6810b19df24832c50b2e61a41867f89416c192585a0ab24b552783b4bf7d8dc9f6855c3594ec6c1cede510be308f0fdbbc8dbdf238829bdb3494f8c9c61c5e7f2b6219d1c28b94e5cb3cdc802594946873352021fe9226884616dc6f189f289aeb0cc59456e8c1463c341abf8b168c3079ea41ce8a387e18b8418890007a341ee171ba8d5e3cb546d1d927c8202f0df3c3f381c8173eb36db41305227c289fb528a4614b1a2c04a7ec5a1b5d76f62b829496aa36979e88a9610c01f903edb841f0ba93ac8e28a021e582e50abbaa24fa5174674b3b0873dc568f6c9ebaf830bb4d03b857416304f97b4314e310f66f6c8043e716e70751bc9663dd6f9e5d6a9100b84174717204aa9d9f2dcb1269c89141ec2ee9d447e1981e8a704caa5a6ce376b0901f3e0ddf0ebe08542af86b23637df2f962b0f7ced5469cea310cb71c2358357300b841aa3aa8b450a6f4d883dcf2eda0f964ff4d35a250996b34aa91279c9c7f4383a22c879e2f21c9fddf8c3b1a6cbc59b273b4a0daf4b15aaf18f5e33e70c9277e6f00b8414adbeaaf82da005a33f00e7f74a3eeecb989698968b3694ea9e74018a0836184188eca727900280734ead256af02e72679addcddbf5ebd82c04c030c2bd85f4a01b841610b61422badd11afa2a617502f81c0c8aa1f11951d80893976a391026a3859c1f5e6c6d28e8b2ca8c4281c699b7b8ec30625801d4a6637291f9a8d1a2d8244f00b8417590e3d92063d4162f49493848ef0557daba3c2d82b9498eda09d5d08837296937a69e7b852579eeadf1c077d3b80d232ece03a12f4c45896e518cbb0771c52700b8415a2a40f416154793535cfe133040236ecc8b1f276df39e0a3713992fad06e38a42a455a636add93bff218544a4c53b852b8c4e461d3ae0663fdefe8fe7e327cc00b841e0c64cc8a30d84196d57639a42c5da941164b0700476d1b91d18f7c8f58d12f932ad1362270ec968294257f9c5cb60c40a7d4a5932a8f4d537be4db51f7dcf2500b841f61b6f014628ab751d79f095b1e739bc2b31fa8b6b847878e13b000a6dd53fa8467903119a72c7445f8490cf4932a42f4a418b89436b70d100c56c083399579500b841e6fe4f7c4bdcb4a81125bd282d0b9fedf1f51636c69bd4684d3131d685a7aed34face3d943d02b6ad632bb337f89fd6b0fb08e163ef84bb87fe556f4bafa0d3401b8412c6666136414f88327e07a6e8a2b04d105d6cf64daee239cea647a25f93ce0e6542f59f4363e3522bc838841e6db1940e569938b9458fb674fd543646a6b669b00b84134f967c4060d85a7c2f65d00695f3308d2ab78033e895775e0ab6f70cc6e71081c030bd997773191b3d2d7e5425e542c3b98fc127031784a858cf497c0e1532100b841d81aedf218d33e12087fb6c71b1d76e69dde542659c85661909b8c99793c7f1535afdc8addaefc5bcf6a3f99fd34518a1e9ab4a73ec9921e9865c1bd8543fd4c01b84199ec6f0fca02e48db37f0e4ae1b2fdf643abf610a9f1d7c0b490250aa7f1393d3069d1b4cec74ee99b0e18081bbf5e03d7b918d46499d579459cf0114ff76e9301b841d81a55eb96767edc5305dac78b904f70d2f44bd845fcd2bd581778669e5b8446220143680619986b9975ea528aacec0976406424588760f4fe086f16abaaaf4600",
    "gasUsed": "0x1d065",
    "governanceData": "0x",
    "hash": "0x7d68d09a7a571cdf8a3b6a5ef6e037265b3e3093cf145b0954d22bde5c1d4f61",
    "logsBloom": "0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
    "number": "0x6e0431",
    "parentHash": "0xa76ef625874a4d2126eb3fd1ebb5c1a8d0deb360a12b4f8edf30fb417d82b5a1",
    "proposer": "0xe783fc94fddaeebef7293d6c5864cff280f121e1",
    "receiptsRoot": "0x56734b337c3daab6766104bb51bd2ca408cf4537f5528ab3362536c57e65ba67",
    "reward": "0x79f83dbb81f6f706be3e8491b14790c30d03e659",
    "size": "0x947",
    "stateRoot": "0xf685dce2cbef004cb041cf23959aea65e8aa86911fac55739ae1971f7d1dacd4",
    "timestamp": "0x5d801768",
    "timestampFoS": "0x4",
    "totalBlockScore": "0x6e0432",
    "transactions": [
      {
        "blockHash": "0x7d68d09a7a571cdf8a3b6a5ef6e037265b3e3093cf145b0954d22bde5c1d4f61",
        "blockNumber": "0x6e0431",
        "contractAddress": null,
        "feePayer": "0x08260736c18bd8612bee2b21beedf4e97c0bc6b9",
        "feePayerSignatures": [
          {
            "V": "0x4055",
            "R": "0xd3fdd58e18e5a96d1f9af3d1aff31601d8e543a8085c78edfc8602db4c91b3c6",
            "S": "0x19d937e315472a188f11a6bb87f47e66a30b44ba907b5f01fcd47dab8d99f3f0"
          }
        ],
        "from": "0x84b605b268e89ccdf591974db82deaa48bce59dc",
        "gas": "0x419ce0",
        "gasPrice": "0x5d21dba00",
        "gasUsed": "0x1d065",
        "input": "0x50716652000000000000000000000000000000000000000000000000000000000000000100000000000000000000000000000000000000000000000000000000013416c50000000000000000000000000000000000000000000000000000000000001f3f000000000000000000000000000000000000000000000000000000003b9af23c",
        "logs": [],
        "logsBloom": "0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
        "nonce": "0x8",
        "senderTxHash": "0x5fe7485db56c0c2b0eb54dd46e584a413193ad66b40e69281f44dadfa7409b2e",
        "signatures": [
          {
            "V": "0x4056",
            "R": "0xca32239c38e1080f3a394504e2a0bb9811cda0a87d25b750cbbab265d581074d",
            "S": "0x584ab136a483e755d9d458f9965ca0d514724c7b45f6123d19323f6fa7ccdb5f"
          }
        ],
        "status": "0x1",
        "to": "0x1db1b93447328dd904152f798ead97987844f7b7",
        "transactionHash": "0x020a2156bb4b29dc84f26887efae79e07a3d738b2856a66bbaab8aee18d507b5",
        "transactionIndex": "0x0",
        "type": "TxTypeFeeDelegatedSmartContractExecution",
        "typeInt": 49,
        "value": "0x0"
      }
    ],
    "transactionsRoot": "0x020a2156bb4b29dc84f26887efae79e07a3d738b2856a66bbaab8aee18d507b5",
    "voteData": "0x"
  }
}
```


## klay_getBlockWithConsensusInfoByHash <a id="klay_getblockwithconsensusinfobyhash"></a>

Returns a block with consensus information that matches the given hash.

**파라미터**

| 타입            | 설명         |
| ------------- | ---------- |
| 32바이트 크기 DATA | 블록의 해시입니다. |

**리턴값**

`Object` - A block object with consensus information (a proposer and a list of committee members), or `error` when no block was found:

| 이름               | 타입            | 설명                                                                                                          |
| ---------------- | ------------- | ----------------------------------------------------------------------------------------------------------- |
| blockScore       | QUANTITY      | 이전 난이도입니다. BFT 합의 엔진에서는 항상 1입니다.                                                                            |
| totalBlockScore  | QUANTITY      | 본 블록까지 체인 내 모든 블록의 blockScore 값의 합입니다.                                                                      |
| committee        | Array         | 블록 생성에 관여한 위원회 멤버들의 주소의 배열입니다. 위원회란 블록 생성을 위한 합의 프로토콜에 참여한 검증자들 중 일부입니다.                                    |
| gasUsed          | QUANTITY      | 블록에 있는 트랜잭션들에서 사용된 가스양의 총합입니다.                                                                              |
| 해시               | 32바이트 크기 DATA | 블록의 해시입니다. 아직 보류 중인 블록이면 `null`입니다.                                                                         |
| number           | QUANTITY      | 블록 번호입니다. 아직 보류 중인 블록이면 `null`입니다.                                                                          |
| parentHash       | 32바이트 크기 DATA | 이전 블록의 해시입니다.                                                                                               |
| proposer         | 20바이트 크기 DATA | 블록 제안자의 주소입니다.                                                                                              |
| receiptsRoot     | 32바이트 크기 DATA | 블록의 영수증 트라이의 루트 해시입니다.                                                                                      |
| size             | QUANTITY      | 블록의 바이트 크기의 정수 형태입니다.                                                                                       |
| stateRoot        | 32바이트 크기 DATA | 블록의 상태 트라이의 루트 해시입니다.                                                                                       |
| timestamp        | QUANTITY      | 블록이 생성되었을 때의 Unix 타임스탬프입니다.                                                                                 |
| timestampFoS     | QUANTITY      | 블록이 생성되었을 때의 타임스탬프 중 초 단위 부분입니다.                                                                            |
| transactions     | Array         | 트랜잭션 객체의 배열입니다.                                                                                             |
| transactionsRoot | 32바이트 크기 DATA | 블록의 트랜잭션 트라이의 루트 해시입니다.                                                                                     |
| baseFeePerGas    | QUANTITY      | The base fee per gas. It has a meaningful value when EthTxTypeCompatible and Magma hardforks are activated. |

**예시**

```shell
// Request
curl -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0", "method":"klay_getBlockWithConsensusInfoByHash", "params":["0x7d68d09a7a571cdf8a3b6a5ef6e037265b3e3093cf145b0954d22bde5c1d4f61"],"id":73}' https://api.baobab.klaytn.net:8651

// Result
{
  "jsonrpc": "2.0",
  "id": 73,
  "result": {
    "baseFeePerGas":"0x5d21dba00",
    "blockscore": "0x1",
    "committee": ["0xe783fc94fddaeebef7293d6c5864cff280f121e1", "0x8a88a093c05376886754a9b70b0d0a826a5e64be", "0xf113ec8c22765d485309cf1d025d1b975245b9f8", "0xe3d92072d8b9a59a0427485a1b5f459271df457c", "0xa2ba8f7798649a778a1fd66d3035904949fec555", "0x2bdd279522b8a0843831fbb94cfbb24a913597c5", "0x9419fa2e3b9eb1158de31be66c586a52f49c5de7", "0xc032c34cb9fe064fe435199e1078dd8756a166b5", "0x56e8c1463c341abf8b168c3079ea41ce8a387e18", "0x6873352021fe9226884616dc6f189f289aeb0cc5", "0xe93a890fb7ec5e993b1a7fd77b0d13a0763eff3d", "0xbca8ffa45cc8e30bbc0522cdf1a1e0ebf540dfe2", "0x386ca3cb8bb13f48d1a6adc1fb8df09e7bb7f9c8", "0x1782834bf8847e235f21f2c1f13fca4d5dff6621", "0x6f6770f1f67f44fb15b335b49581ad6b935d963a", "0x0b59cae1f03534209fdb9ddf5ea65b310cd7060c", "0xb9456fd65a6810b19df24832c50b2e61a41867f8", "0x16c192585a0ab24b552783b4bf7d8dc9f6855c35", "0xec6c1cede510be308f0fdbbc8dbdf238829bdb34", "0xf8c9c61c5e7f2b6219d1c28b94e5cb3cdc802594", "0x5e59db28cef098d5a2e877f84127aed10d7378f2", "0x52d41ca72af615a1ac3301b0a93efa222ecc7541"],
    "extraData": "0xd883010101846b6c617988676f312e31322e35856c696e757800000000000000f90604f901ce9452d41ca72af615a1ac3301b0a93efa222ecc7541948a88a093c05376886754a9b70b0d0a826a5e64be94f113ec8c22765d485309cf1d025d1b975245b9f894e3d92072d8b9a59a0427485a1b5f459271df457c94a2ba8f7798649a778a1fd66d3035904949fec555942bdd279522b8a0843831fbb94cfbb24a913597c594bca8ffa45cc8e30bbc0522cdf1a1e0ebf540dfe294c032c34cb9fe064fe435199e1078dd8756a166b59456e3a565e31f8fb0ba0b12c03355518c64372120946f6770f1f67f44fb15b335b49581ad6b935d963a94e93a890fb7ec5e993b1a7fd77b0d13a0763eff3d94e783fc94fddaeebef7293d6c5864cff280f121e194386ca3cb8bb13f48d1a6adc1fb8df09e7bb7f9c8941782834bf8847e235f21f2c1f13fca4d5dff6621949419fa2e3b9eb1158de31be66c586a52f49c5de7940b59cae1f03534209fdb9ddf5ea65b310cd7060c94b9456fd65a6810b19df24832c50b2e61a41867f89416c192585a0ab24b552783b4bf7d8dc9f6855c3594ec6c1cede510be308f0fdbbc8dbdf238829bdb3494f8c9c61c5e7f2b6219d1c28b94e5cb3cdc802594946873352021fe9226884616dc6f189f289aeb0cc59456e8c1463c341abf8b168c3079ea41ce8a387e18b8418890007a341ee171ba8d5e3cb546d1d927c8202f0df3c3f381c8173eb36db41305227c289fb528a4614b1a2c04a7ec5a1b5d76f62b829496aa36979e88a9610c01f903edb841f0ba93ac8e28a021e582e50abbaa24fa5174674b3b0873dc568f6c9ebaf830bb4d03b857416304f97b4314e310f66f6c8043e716e70751bc9663dd6f9e5d6a9100b84174717204aa9d9f2dcb1269c89141ec2ee9d447e1981e8a704caa5a6ce376b0901f3e0ddf0ebe08542af86b23637df2f962b0f7ced5469cea310cb71c2358357300b841aa3aa8b450a6f4d883dcf2eda0f964ff4d35a250996b34aa91279c9c7f4383a22c879e2f21c9fddf8c3b1a6cbc59b273b4a0daf4b15aaf18f5e33e70c9277e6f00b8414adbeaaf82da005a33f00e7f74a3eeecb989698968b3694ea9e74018a0836184188eca727900280734ead256af02e72679addcddbf5ebd82c04c030c2bd85f4a01b841610b61422badd11afa2a617502f81c0c8aa1f11951d80893976a391026a3859c1f5e6c6d28e8b2ca8c4281c699b7b8ec30625801d4a6637291f9a8d1a2d8244f00b8417590e3d92063d4162f49493848ef0557daba3c2d82b9498eda09d5d08837296937a69e7b852579eeadf1c077d3b80d232ece03a12f4c45896e518cbb0771c52700b8415a2a40f416154793535cfe133040236ecc8b1f276df39e0a3713992fad06e38a42a455a636add93bff218544a4c53b852b8c4e461d3ae0663fdefe8fe7e327cc00b841e0c64cc8a30d84196d57639a42c5da941164b0700476d1b91d18f7c8f58d12f932ad1362270ec968294257f9c5cb60c40a7d4a5932a8f4d537be4db51f7dcf2500b841f61b6f014628ab751d79f095b1e739bc2b31fa8b6b847878e13b000a6dd53fa8467903119a72c7445f8490cf4932a42f4a418b89436b70d100c56c083399579500b841e6fe4f7c4bdcb4a81125bd282d0b9fedf1f51636c69bd4684d3131d685a7aed34face3d943d02b6ad632bb337f89fd6b0fb08e163ef84bb87fe556f4bafa0d3401b8412c6666136414f88327e07a6e8a2b04d105d6cf64daee239cea647a25f93ce0e6542f59f4363e3522bc838841e6db1940e569938b9458fb674fd543646a6b669b00b84134f967c4060d85a7c2f65d00695f3308d2ab78033e895775e0ab6f70cc6e71081c030bd997773191b3d2d7e5425e542c3b98fc127031784a858cf497c0e1532100b841d81aedf218d33e12087fb6c71b1d76e69dde542659c85661909b8c99793c7f1535afdc8addaefc5bcf6a3f99fd34518a1e9ab4a73ec9921e9865c1bd8543fd4c01b84199ec6f0fca02e48db37f0e4ae1b2fdf643abf610a9f1d7c0b490250aa7f1393d3069d1b4cec74ee99b0e18081bbf5e03d7b918d46499d579459cf0114ff76e9301b841d81a55eb96767edc5305dac78b904f70d2f44bd845fcd2bd581778669e5b8446220143680619986b9975ea528aacec0976406424588760f4fe086f16abaaaf4600",
    "gasUsed": "0x1d065",
    "governanceData": "0x",
    "hash": "0x7d68d09a7a571cdf8a3b6a5ef6e037265b3e3093cf145b0954d22bde5c1d4f61",
    "logsBloom": "0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
    "number": "0x6e0431",
    "parentHash": "0xa76ef625874a4d2126eb3fd1ebb5c1a8d0deb360a12b4f8edf30fb417d82b5a1",
    "proposer": "0xe783fc94fddaeebef7293d6c5864cff280f121e1",
    "receiptsRoot": "0x56734b337c3daab6766104bb51bd2ca408cf4537f5528ab3362536c57e65ba67",
    "reward": "0x79f83dbb81f6f706be3e8491b14790c30d03e659",
    "size": "0x947",
    "stateRoot": "0xf685dce2cbef004cb041cf23959aea65e8aa86911fac55739ae1971f7d1dacd4",
    "timestamp": "0x5d801768",
    "timestampFoS": "0x4",
    "totalBlockScore": "0x6e0432",
    "transactions": [
      {
        "blockHash": "0x7d68d09a7a571cdf8a3b6a5ef6e037265b3e3093cf145b0954d22bde5c1d4f61",
        "blockNumber": "0x6e0431",
        "contractAddress": null,
        "feePayer": "0x08260736c18bd8612bee2b21beedf4e97c0bc6b9",
        "feePayerSignatures": [
          {
            "V": "0x4055",
            "R": "0xd3fdd58e18e5a96d1f9af3d1aff31601d8e543a8085c78edfc8602db4c91b3c6",
            "S": "0x19d937e315472a188f11a6bb87f47e66a30b44ba907b5f01fcd47dab8d99f3f0"
          }
        ],
        "from": "0x84b605b268e89ccdf591974db82deaa48bce59dc",
        "gas": "0x419ce0",
        "gasPrice": "0x5d21dba00",
        "gasUsed": "0x1d065",
        "input": "0x50716652000000000000000000000000000000000000000000000000000000000000000100000000000000000000000000000000000000000000000000000000013416c50000000000000000000000000000000000000000000000000000000000001f3f000000000000000000000000000000000000000000000000000000003b9af23c",
        "logs": [],
        "logsBloom": "0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
        "nonce": "0x8",
        "senderTxHash": "0x5fe7485db56c0c2b0eb54dd46e584a413193ad66b40e69281f44dadfa7409b2e",
        "signatures": [
          {
            "V": "0x4056",
            "R": "0xca32239c38e1080f3a394504e2a0bb9811cda0a87d25b750cbbab265d581074d",
            "S": "0x584ab136a483e755d9d458f9965ca0d514724c7b45f6123d19323f6fa7ccdb5f"
          }
        ],
        "status": "0x1",
        "to": "0x1db1b93447328dd904152f798ead97987844f7b7",
        "transactionHash": "0x020a2156bb4b29dc84f26887efae79e07a3d738b2856a66bbaab8aee18d507b5",
        "transactionIndex": "0x0",
        "type": "TxTypeFeeDelegatedSmartContractExecution",
        "typeInt": 49,
        "value": "0x0"
      }
    ],
    "transactionsRoot": "0x020a2156bb4b29dc84f26887efae79e07a3d738b2856a66bbaab8aee18d507b5",
    "voteData": "0x"
  }
}
```


## klay_getCommittee <a id="klay_getcommittee"></a>
어떤 블록 시간에서 위원회에 속한 검증자 목록을 반환합니다. 매개변수를 설정하지 않으면 최신 블록에서 위원회에 속한 검증자 목록을 반환합니다.

**파라미터**

| 이름                   | 타입    | 설명                                                                                                                                                                  |
| -------------------- | ----- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| QUANTITY  &#124; TAG | 블록 번호 | (optional) Integer or hexadecimal block number, or the string `"earliest"` or `"latest"` as in the [default block parameter](block.md#the-default-block-parameter). |

{% hint style="success" %}
참고: Klaytn v1.7.0 이전 버전에서는 정수형 블록 번호나 `"earliest"`, `"latest"` 같은 문자열만 사용할 수 있습니다.
{% endhint %}

**리턴값**

`Array` - Array of addresses of all validators in the committee, or `null` when no committee was found:

| 타입                  | 설명                                            |
| ------------------- | --------------------------------------------- |
| 20바이트 크기 DATA array | Addresses of all validators in the committee. |

**예시**

```shell
// Request
curl -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0", "method":"klay_getCommittee", "params":["0x1b4"],"id":73}' https://api.baobab.klaytn.net:8651
// Result
{
    "jsonrpc":"2.0",
    "id":73,
    "result":[
        "0x207e38864b45a538733741dc1ff92eff9d1a6159",
        "0x6d64bc82b93368a7f963d6c34483ca3893f405f6",
        "0xbc9c19f91878369776812039e4ebcdfa3c646716",
        "0xe3ed6fa287752b992f936b42360770c59731d9eb"
    ]
}
```

## klay_getCommitteeSize <a id="klay_getcommitteesize"></a>
어떤 블록 시간에서 위원회의 구성원 수를 반환합니다. 매개변수를 설정하지 않으면 최신 블록에서의 위원회 구성원 수를 반환합니다.

**파라미터**

| 이름                   | 타입    | 설명                                                                                                                                                                  |
| -------------------- | ----- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| QUANTITY  &#124; TAG | 블록 번호 | (optional) Integer or hexadecimal block number, or the string `"earliest"` or `"latest"` as in the [default block parameter](block.md#the-default-block-parameter). |

{% hint style="success" %}
참고: Klaytn v1.7.0 이전 버전에서는 정수형 블록 번호나 `"earliest"`, `"latest"` 같은 문자열만 사용할 수 있습니다.
{% endhint %}

**리턴값**

`Integer` - The size of the committee, or `-1` when no committee was found:

| 타입       | 설명                      |
| -------- | ----------------------- |
| QUANTITY | The size of the council |

**예시**

```shell
// Request
curl -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0", "method":"klay_getCommitteeSize", "params":["0x1b4"],"id":73}' https://api.baobab.klaytn.net:8651
// Result
{
    "jsonrpc":"2.0",
    "id":73,
    "result":4
}
```


## klay_getCouncil <a id="klay_getcouncil"></a>
어떤 블록 시간에서 council에 속한 검증자 목록을 반환합니다. 매개변수를 설정하지 않으면 최신 블록에서 council에 속한 검증자 목록을 반환합니다.

**NOTE**: `klay_getValidators` is replaced with this method and is not supported anymore.

**파라미터**

| 이름                   | 타입    | 설명                                                                                                                                                                  |
| -------------------- | ----- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| QUANTITY  &#124; TAG | 블록 번호 | (optional) Integer or hexadecimal block number, or the string `"earliest"` or `"latest"` as in the [default block parameter](block.md#the-default-block-parameter). |

{% hint style="success" %}
참고: Klaytn v1.7.0 이전 버전에서는 정수형 블록 번호나 `"earliest"`, `"latest"` 같은 문자열만 사용할 수 있습니다.
{% endhint %}

**리턴값**

`Array` - Array of validator addresses of the council, or `null` when no council was found:

| 타입                  | 설명                                          |
| ------------------- | ------------------------------------------- |
| 20바이트 크기 DATA array | Addresses of all validators of the council. |

**예시**

```shell
// Request
curl -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0", "method":"klay_getCouncil", "params":["0x1b4"],"id":73}' https://api.baobab.klaytn.net:8651
// Result
{
    "jsonrpc":"2.0",
    "id":73,
    "result":[
        "0x207e38864b45a538733741dc1ff92eff9d1a6159",
        "0x6d64bc82b93368a7f963d6c34483ca3893f405f6",
        "0xbc9c19f91878369776812039e4ebcdfa3c646716",
        "0xe3ed6fa287752b992f936b42360770c59731d9eb"
    ]
}
```

## klay_getCouncilSize <a id="klay_getcouncilsize"></a>
어떤 블록 시간에서 council의 구성원 수를 반환합니다. 매개변수를 설정하지 않으면 최신 블록에서의 council 구성원 수를 반환합니다.

**파라미터**

| 이름                   | 타입    | 설명                                                                                                                                                                  |
| -------------------- | ----- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| QUANTITY  &#124; TAG | 블록 번호 | (optional) Integer or hexadecimal block number, or the string `"earliest"` or `"latest"` as in the [default block parameter](block.md#the-default-block-parameter). |

{% hint style="success" %}
참고: Klaytn v1.7.0 이전 버전에서는 정수형 블록 번호나 `"earliest"`, `"latest"` 같은 문자열만 사용할 수 있습니다.
{% endhint %}

**리턴값**

`Integer` - The size of the council, or `-1` when no council was found:

| 타입       | 설명                      |
| -------- | ----------------------- |
| QUANTITY | The size of the council |

**예시**

```shell
// Request
curl -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0", "method":"klay_getCouncilSize", "params":["0x1b4"],"id":73}' https://api.baobab.klaytn.net:8651
// Result
{
    "jsonrpc":"2.0",
    "id":73,
    "result": 4
}
```


## klay_getStorageAt <a id="klay_getstorageat"></a>

입력으로 받은 주소의 스토리지 위치에서 값을 반환합니다.

**파라미터**

| 타입                              | 설명                                                                                                                                                                                   |
| ------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 20바이트 크기 DATA                   | 스토리지의 주소입니다.                                                                                                                                                                         |
| QUANTITY                        | 스토리지 내 위치의 정수 형태입니다.                                                                                                                                                                 |
| QUANTITY &#124; TAG &#124; HASH | Integer or hexadecimal block number, or the string `"earliest"`, `"latest"` or `"pending"` as in the [default block parameter](block.md#the-default-block-parameter), or block hash. |

{% hint style="success" %}
참고: Klaytn v1.7.0 이전 버전에서는 정수형 블록 번호나 `"earliest"`, `"latest"` 같은 문자열만 사용할 수 있습니다.
{% endhint %}

 **리턴값**

| 타입   | 설명                         |
| ---- | -------------------------- |
| DATA | 입력으로 받은 스토리지 위치의 값을 반환합니다. |

**예시**

올바른 위치를 계산하는 것은 탐색할 스토리지에 따라 차이가 있습니다. Consider the following contract deployed at `0x295a70b2de5e3953354a6a8344e616ed314d7251` by address `0x391694e7e0b0cce554cb130d723a9d27458f9298`.

```
contract Storage {
    uint pos0;
    mapping(address => uint) pos1;

    function Storage() {
        pos0 = 1234;
        pos1[msg.sender] = 5678;
    }
}
```

`pos0`의 값은 다음과 같이 쉽게 찾을 수 있습니다.

```shell
curl -H "Content-Type: application/json" --data '{"jsonrpc":"2.0", "method": "klay_getStorageAt", "params": ["0x295a70b2de5e3953354a6a8344e616ed314d7251", "0x0", "latest"], "id": 1}' https://api.baobab.klaytn.net:8651

{"jsonrpc":"2.0","id":1,"result":"0x00000000000000000000000000000000000000000000000000000000000004d2"}
```

맵핑의 요소를 찾는 것은 더 어렵습니다. 맵핑의 요소의 위치는 다음과 같이 계산됩니다.
```javascript
keccak(LeftPad32(key, 0), LeftPad32(map position, 0))
```

즉 `pos1["0x391694e7e0b0cce554cb130d723a9d27458f9298"]`의 스토리지를 탐색하려면 아래와 같이 그 위치를 계산해야 합니다.
```javascript
keccak(decodeHex("000000000000000000000000391694e7e0b0cce554cb130d723a9d27458f9298" + "0000000000000000000000000000000000000000000000000000000000000001"))
```
이는 `klay` 라이브러리와 함께 제공되는 Klaytn 콘솔을 사용하여 계산할 수 있습니다.
```javascript
> var key = "000000000000000000000000391694e7e0b0cce554cb130d723a9d27458f9298" + "0000000000000000000000000000000000000000000000000000000000000001"
undefined
> klay.sha3(key, {"encoding": "hex"})
"0x6661e9d6d8b923d5bbaab1b96e1dd51ff6ea2a93520fdc9eb75d059238b8c5e9"
```
이제 스토리지 값을 가져오려면 다음과 같이 입력합니다.
```shell
curl -H "Content-Type: application/json" --data '{"jsonrpc":"2.0", "method": "klay_getStorageAt", "params": ["0x295a70b2de5e3953354a6a8344e616ed314d7251", "0x6661e9d6d8b923d5bbaab1b96e1dd51ff6ea2a93520fdc9eb75d059238b8c5e9", "latest"], "id": 1}' https://api.baobab.klaytn.net:8651

{"jsonrpc":"2.0","id":1,"result":"0x000000000000000000000000000000000000000000000000000000000000162e"}
```


## klay_syncing <a id="klay_syncing"></a>

동기화 상태에 대한 데이터가 있는 객체를 반환하거나 `false`를 반환합니다.

**파라미터**

없음

**리턴값**

`Object|Boolean`, 동기화 상태에 대한 데이터 객체를 반환하거나 또는 동기화하고 있지 않으면 `false` 를 반환합니다.

| 이름            | 타입       | 설명                                                       |
| ------------- | -------- | -------------------------------------------------------- |
| startingBlock | QUANTITY | 가져오기 시작하는 블록입니다(동기화가 완료되면 재설정됩니다).                       |
| currentBlock  | QUANTITY | The current block, same as `klay_blockNumber`.           |
| highestBlock  | QUANTITY | 예상되는 최신 블록 번호입니다.                                        |
| pulledStates  | QUANTITY | 지금까지 처리된 상태 항목의 개수입니다.  동기화 모드가 "fast"가 아니면 0이 반환됩니다.    |
| knownStates   | QUANTITY | 가져와야 하는 알려진 상태 항목의 개수입니다.  동기화 모드가 "fast"가 아니면 0이 반환됩니다. |

**예시**

```shell
// Request
curl -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"klay_syncing","params":[],"id":1}' https://api.baobab.klaytn.net:8651

// Result
{
  "jsonrpc": "2.0",
  "id":1,
  "result": {
    "currentBlock":"0x3e31e",
    "highestBlock":"0x827eef",
    "knownStates":"0x0",
    "pulledStates":"0x0",
    "startingBlock":"0x0"
  }
}
// Or when not syncing
{
  "jsonrpc": "2.0",
  "id":1,
  "result": false
}
```
