# caver.rpc <a id="caver-rpc"></a>

`caver.rpc`는 Klaytn 노드에 RPC 호출을 하는 기능을 제공하는 패키지입니다.

## Class <a id="class"></a>

### RPC <a id="rpc"></a>

```javascript
caver.rpc
```

`RPC` is a class that contains [Klay][], [Net][] and [Governance][] inside.

**속성**

| 이름   | 타입       | 설명                                                                           |
| ---- | -------- | ---------------------------------------------------------------------------- |
| klay | [Klay][] | The [Klay][] providing JSON-RPC call with  the`klay` name space.             |
| net  | [Net][]  | The [Net][] providing JSON-RPC call with the `net` name space.               |
| 거버넌스 | [거버넌스][] | The [Governance][] providing JSON-RPC call with the `governance` name space. |

## JSON-RPC calls <a id="json-rpc-calls"></a>

`caver.rpc.klay`를 사용하면 Klaytn 노드와 상호작용할 수 있습니다. 아래 목록은 `caver-js`에서 현재 지원되는 API의 기능을 열거합니다.

### [계정(Account)](./klay.md#caver-rpc-klay-accountcreated) <a id="account"></a>
- [accountCreated](./klay.md#caver-rpc-klay-accountcreated)
- [getAccount](./klay.md#caver-rpc-klay-getaccount)
- [getAccountKey](./klay.md#caver-rpc-klay-getaccountkey)
- [encodeAccountKey](./klay.md#caver-rpc-klay-encodeaccountkey)
- [decodeAccountKey](./klay.md#caver-rpc-klay-decodeaccountkey)
- [getBalance](./klay.md#caver-rpc-klay-getbalance)
- [getCode](./klay.md#caver-rpc-klay-getcode)
- [getTransactionCount](./klay.md#caver-rpc-klay-gettransactioncount)
- [isContractAccount](./klay.md#caver-rpc-klay-iscontractaccount)
- [서명](./klay.md#caver-rpc-klay-sign)
- [getAccounts](./klay.md#caver-rpc-klay-getaccounts)

### [블록(Block)](./klay.md#caver-rpc-klay-getblocknumber) <a id="block"></a>
- [getBlockNumber](./klay.md#caver-rpc-klay-getblocknumber)
- [getBlockByNumber](./klay.md#caver-rpc-klay-getblockbynumber)
- [getBlockByHash](./klay.md#caver-rpc-klay-getblockbyhash)
- [getBlockReceipts](./klay.md#caver-rpc-klay-getblockreceipts)
- [getBlockTransactionCountByNumber](./klay.md#caver-rpc-klay-getblocktransactioncountbynumber)
- [getBlockTransactionCountByHash](./klay.md#caver-rpc-klay-getblocktransactionCountbyhash)
- [getBlockWithConsensusInfoByNumber](./klay.md#caver-rpc-klay-getblockwithconsensusinfobynumber)
- [getBlockWithConsensusInfoByHash](./klay.md#caver-rpc-klay-getblockwithconsensusinfobyhash)
- [getCommittee](./klay.md#caver-rpc-klay-getcommittee)
- [getCommitteeSize](./klay.md#caver-rpc-klay-getcommitteesize)
- [getCouncil](./klay.md#caver-rpc-klay-getcouncil)
- [getCouncilSize](./klay.md#caver-rpc-klay-getcouncilsize)
- [getStorageAt](./klay.md#caver-rpc-klay-getstorageat)
- [isSyncing](./klay.md#caver-rpc-klay-issyncing)

### [트랜잭션(Transaction)](./klay.md#caver-rpc-klay-call) <a id="transaction"></a>
- [call](./klay.md#caver-rpc-klay-call)
- [estimateGas](./klay.md#caver-rpc-klay-estimategas)
- [estimateComputationCost](./klay.md#caver-rpc-klay-estimatecomputationcost)
- [getTransactionByBlockHashAndIndex](./klay.md#caver-rpc-klay-gettransactionbyblockhashandindex)
- [getTransactionByBlockNumberAndIndex](./klay.md#caver-rpc-klay-gettransactionbyblocknumberandindex)
- [getTransactionByHash](./klay.md#caver-rpc-klay-gettransactionbyhash)
- [getTransactionBySenderTxHash](./klay.md#caver-rpc-klay-gettransactionbysendertxhash)
- [getTransactionReceipt](./klay.md#caver-rpc-klay-gettransactionreceipt)
- [getTransactionReceiptBySenderTxHash](./klay.md#caver-rpc-klay-gettransactionreceiptbysendertxhash)
- [sendRawTransaction](./klay.md#caver-rpc-klay-sendrawtransaction)
- [sendTransaction](./klay.md#caver-rpc-klay-sendtransaction)
- [sendTransactionAsFeePayer](./klay.md#caver-rpc-klay-sendtransactionasfeepayer)
- [signTransaction](./klay.md#caver-rpc-klay-signtransaction)
- [signTransactionAsFeePayer](./klay.md#caver-rpc-klay-signtransactionasfeepayer)
- [getDecodedAnchoringTransactionByHash](./klay.md#caver-rpc-klay-getdecodedanchoringtransactionbyhash)

### [환경설정(Configuration)](./klay.md#caver-rpc-klay-getclientversion) <a id="configuration"></a>
- [getChainId](./klay.md#caver-rpc-klay-getchainid)
- [getClientVersion](./klay.md#caver-rpc-klay-getclientversion)
- [getGasPrice](./klay.md#caver-rpc-klay-getgasprice)
- [getGasPriceAt](./klay.md#caver-rpc-klay-getgaspriceat)
- [isParallelDBWrite](./klay.md#caver-rpc-klay-isparalleldbwrite)
- [isSenderTxHashIndexingEnabled](./klay.md#caver-rpc-klay-issendertxhashindexingenabled)
- [getProtocolVersion](./klay.md#caver-rpc-klay-getprotocolversion)
- [getRewardbase](./klay.md#caver-rpc-klay-getrewardbase)

### [필터(Filter)](./klay.md#caver-rpc-klay-getfilterchanges) <a id="filter"></a>
- [getFilterChanges](./klay.md#caver-rpc-klay-getfilterchanges)
- [getFilterLogs](./klay.md#caver-rpc-klay-getfilterlogs)
- [getLogs](./klay.md#caver-rpc-klay-getlogs)
- [newBlockFilter](./klay.md#caver-rpc-klay-newblockfilter)
- [newFilter](./klay.md#caver-rpc-klay-newfilter)
- [newPendingTransactionFilter](./klay.md#caver-rpc-klay-newpendingtransactionfilter)
- [uninstallFilter](./klay.md#caver-rpc-klay-uninstallfilter)

### [네트워크(Network)](./net.md) <a id="network"></a>
- [getNetworkId](./net.md#caver-rpc-net-getnetworkid)
- [isListening](./net.md#caver-rpc-net-islistening)
- [getPeerCount](./net.md#caver-rpc-net-getpeercount)
- [getPeerCountByType](./net.md#caver-rpc-net-getpeercountbytype)

### [기타(Miscellaneous)](./klay.md#caver-rpc-klay-sha3) <a id="miscellaneous"></a>
- [sha3](./klay.md#caver-rpc-klay-sha3)

[Klay]: ./klay.md
[Net]: ./net.md
[Governance]: ./governance.md
[거버넌스]: ./governance.md
