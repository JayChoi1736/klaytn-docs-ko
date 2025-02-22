---
description: 스마트 컨트랙트와 상호작용하는 데 사용되는 caver-js 객체입니다.
---

# caver.klay.Contract

The `caver.klay.Contract` object makes it easy to interact with smart contracts on the Klaytn blockchain. When you create a new contract object, you give it the JSON interface of the respective smart contract and caver will auto convert all calls into low level ABI calls over RPC for you.

이를 통해 스마트 컨트랙트가 마치 자바스크립트 객체인 것처럼 스마트 컨트랙트와 상호작용할 수 있습니다.

## new contract <a id="new-contract"></a>

```javascript
new caver.klay.Contract(jsonInterface [, address] [, options])
```

JSON 인터페이스 오브젝트에 정의된 모든 메소드 및 이벤트로 새 컨트랙트 인스턴스를 생성합니다.

**파라미터**

| 이름            | 타입     | 설명                                                                                                                        |
|:------------- |:------ |:------------------------------------------------------------------------------------------------------------------------- |
| jsonInterface | Object | 컨트랙트를 인스턴스화하기 위한 JSON 인터페이스                                                                                               |
| address       | String | \(optional\) The address of the smart contract to call. `myContract.options.address = '0x1234..'`를 사용하여 나중에 추가할 수 있습니다. |
| options       | Object | \(optional\) The options of the contract.  자세한 내용은 아래 표를 참조하세요.                                                         |

옵션 개체에는 다음이 포함됩니다:

| 이름    | 타입     | 설명                                                                         |
|:----- |:------ |:-------------------------------------------------------------------------- |
| from  | String | \(optional\) The address from which transactions should be made.         |
| 가스 가격 | String | \(optional\) The gas price in peb to use for transactions.               |
| gas   | Number | \(optional\) The maximum gas provided for a transaction \(gas limit\). |
| 데이터   | String | \(optional\) The byte code of the contract. 컨트랙트가 배포될 때 사용됩니다.           |

**리턴값**

| 타입     | 설명                         |
|:------ |:-------------------------- |
| Object | 모든 메소드와 이벤트가 있는 컨트랙트 인스턴스. |

**예시**

```javascript
var myContract = new caver.klay.Contract([...], '0xde0B295669a9FD93d5F28D9Ec85E40f4cb697BAe', {
      from: '0x1234567890123456789012345678901234567891', // default from address
      gasPrice: '25000000000' // default gas price in peb, 25 Gpeb in this case
});

var myContract = new caver.klay.Contract([...], 'myContract', {
      from: '0x1234567890123456789012345678901234567891', // default from address
      gasPrice: '25000000000' // default gas price in peb, 25 Gpeb in this case
});
```

## options <a id="options"></a>

```javascript
myContract.options
```

컨트랙트 인스턴스에 대한 `options` 객체. `from`, `gas` and `gasPrice` are used as fallback values when sending transactions.

**속성**

| 이름            | 타입     | 설명                                                                           |
|:------------- |:------ |:---------------------------------------------------------------------------- |
| address       | String | 컨트랙트가 배포된 주소.  Also see [options.address](#options-address).                 |
| jsonInterface | Array  | 컨트랙트의 JSON 인터페이스.  Also see [options.jsonInterface](#options-jsoninterface). |
| 데이터           | String | 컨트랙트의 바이트 코드. 컨트랙트가 배포될 때 사용됩니다.                                             |
| from          | String | 트랜잭션이 만들어진 송신자 주소.                                                           |
| 가스 가격         | String | 트랜잭션에 사용할 peb 단위의 가스 가격.                                                     |
| gas           | Number | The maximum gas provided for a transaction \(gas limit\).                  |

**예시**

```javascript
> myContract.options;
{
    address: '0x1234567890123456789012345678901234567891',
    jsonInterface: [...],
    from: '0xde0B295669a9FD93d5F28D9Ec85E40f4cb697BAe',
    gasPrice: '10000000000000',
    gas: 1000000
}

> myContract.options.from = '0x1234567890123456789012345678901234567891'; // default from address
> myContract.options.gasPrice = '25000000000000'; // default gas price in peb
> myContract.options.gas = 5000000; // provide as fallback always 5M gas
```

## options.address <a id="options-address"></a>

```javascript
myContract.options.address
```

이 컨트랙트 인스턴스 `myContract`에 사용된 주소. All transactions generated by caver-js from this contract will contain this address as the "to". 주소는 소문자로 저장됩니다.

**속성**

| 이름      | 타입        | 설명                                                                     |
|:------- |:--------- |:---------------------------------------------------------------------- |
| address | String \ | `null` | The address for this contract or `null` if it is not yet set. |

**예시**

```javascript
>  myContract.options.address;
'0xde0b295669a9fd93d5f28d9ec85e40f4cb697bae'

// set a new address
>  myContract.options.address = '0x1234FFDD...';
```

## options.jsonInterface <a id="options-jsoninterface"></a>

```javascript
myContract.options.jsonInterface
```

이 컨트랙트 `myContract`의 ABI에서 파생된 JSON 인터페이스 객체.

**속성**

| 이름            | 타입    | 설명                                                         |
|:------------- |:----- |:---------------------------------------------------------- |
| jsonInterface | Array | 이 컨트랙트의 JSON 인터페이스. 이를 재설정하면 컨트랙트 인스턴스의 메소드 및 이벤트가 재생성됩니다. |

**예시**

```javascript
> myContract.options.jsonInterface;
[{
      "type":"function",
      "name":"foo",
      "inputs": [{"name":"a","type":"uint256"}],
      "outputs": [{"name":"b","type":"address"}]
 },{
      "type":"event",
      "name":"Event"
      "inputs": [{"name":"a","type":"uint256","indexed":true},{"name":"b","type":"bytes32","indexed":false}],
 }]

// set a new interface
> myContract.options.jsonInterface = [...];
```

## clone <a id="clone"></a>

```javascript
myContract.clone()
```

현재 컨트랙트 인스턴스를 복제합니다.

**파라미터**

없음

**리턴값**

| 타입     | 설명                |
|:------ |:----------------- |
| Object | 새로 복제된 컨트랙트 인스턴스. |

**예시**

```javascript
> var contract1 = new caver.klay.Contract(abi, address, {gasPrice: '12345678', from: fromAddress});
> var contract2 = contract1.clone();
> contract2.options.address = address2;
> (contract1.options.address !== contract2.options.address);
true
```

## deploy <a id="deploy"></a>

```javascript
myContract.deploy(options)
```

컨트랙트를 Klaytn 블록체인에 배포합니다. After successful deployment, the promise will be resolved with a new contract instance.

**파라미터**

`options`: 배포에 사용되는 옵션 객체:

| 이름        | 타입     | 설명                                                                             |
|:--------- |:------ |:------------------------------------------------------------------------------ |
| 데이터       | String | 컨트랙트의 바이트 코드.                                                                  |
| arguments | Array  | \(optional\) The arguments that get passed to the constructor on deployment. |

**리턴값**

`Object`: 트랜잭션 객체:

| 타입       | 설명                                                                                                                            |
|:-------- |:----------------------------------------------------------------------------------------------------------------------------- |
| Array    | arguments: 이전에 메소드에 전달되었던 인자. 이들은 변경될 수 있습니다.                                                                                 |
| Function | [send](#methods-mymethod-send): Will deploy the contract. 프로미스는 영수증 대신 새 컨트랙트 인스턴스를 반환할 것입니다.                                 |
| Function | [estimateGas](#methods-mymethod-estimategas): Will estimate the gas used for the deployment.                                  |
| Function | [encodeABI](#methods-mymethod-encodeabi): Encodes the ABI of the deployment, which is contract data + constructor parameters. |

**예시**

```javascript
> myContract.deploy({
      data: '0x12345...',
      arguments: [123, 'My String']
  })
  .send({
      from: '0x1234567890123456789012345678901234567891',
      gas: 1500000,
      value: 0,
  }, function(error, transactionHash) { ... })
  .on('error', function(error) { ... })
  .on('transactionHash', function(transactionHash) { ... })
  .on('receipt', function(receipt) {
     console.log(receipt.contractAddress) // contains the new contract address
   })
  .then(function(newContractInstance) {
      console.log(newContractInstance.options.address) // instance with the new contract address
  });

// When the data is already set as an option to the contract itself
> myContract.options.data = '0x12345...';

> myContract.deploy({
        arguments: [123, 'My String']
  })
  .send({
      from: '0x1234567890123456789012345678901234567891',
      gas: 1500000,
      value: 0,
  })
  .then(function(newContractInstance) {
      console.log(newContractInstance.options.address) // instance with the new contract address
  });

// Simply encoding
> myContract.deploy({
      data: '0x12345...',
      arguments: [123, 'My String']
  })
  .encodeABI();
'0x12345...0000012345678765432'

// Gas estimation
> myContract.deploy({
      data: '0x12345...',
      arguments: [123, 'My String']
  })
  .estimateGas(function(err, gas) {
      console.log(gas);
  });
```

## methods <a id="methods"></a>

```javascript
myContract.methods.myMethod([param1 [, param2 [, ...]]])
```

호출, 전송, 추정 또는 ABI 인코딩될 수 있는 해당 메소드에 대한 트랜잭션 객체를 생성합니다.

이 스마트 컨트랙트의 메소드는 다음을 통해 이용할 수 있습니다:

* 이름: `myContract.methods.myMethod(123)`
* 매개변수가 있는 이름: `myContract.methods['myMethod(uint256)'](123)`
* The signature\*: `myContract.methods['0x58cf5f10'](123)`

이를 통해 자바스크립트 컨트랙트 객체로부터 이름은 같지만 매개변수가 다른 함수를 호출할 수 있습니다.

## cf\) \*Function signature \(Function selector\) <a id="cf-function-signature-function-selector"></a>

The first four bytes of the call data for a function call specifies the function to be called.  
It is the first \(left, high-order in big-endian\) four bytes of the Keccak-256 \(SHA-3\) hash of the signature of the function.

The function signature can be made by 2 different methods.  
`1. caver.klay.abi.encodeFunctionSignature('funcName(paramType1,paramType2,...)')`  
`2. caver.utils.sha3('funcName(paramType1,paramType2,...)').substr(0, 10)`

ex\)

```javascript
caver.klay.abi.encodeFunctionSignature('myMethod(uint256)')
> 0x58cf5f10

caver.utils.sha3('myMethod(uint256)').substr(0, 10)
> 0x58cf5f10
```

**파라미터**

모든 메소드의 매개변수는 JSON 인터페이스에 정의된 스마트 컨트랙트 메소드에 의존합니다.

**리턴값**

`Object`: 트랜잭션 객체:

| 타입       | 설명                                                                                                                                                                                                             |
|:-------- |:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Array    | arguments: 이전에 메소드에 전달되었던 인자. 이들은 변경될 수 있습니다.                                                                                                                                                                  |
| Function | [call](#methods-mymethod-call): Will call the "constant" method and execute its smart contract method in the Klaytn Virtual Machine without sending a transaction \(cannot alter the smart contract state\). |
| Function | [send](#methods-mymethod-send): Will send a transaction to the smart contract and execute its method \(can alter the smart contract state\).                                                                 |
| Function | [estimateGas](#methods-mymethod-estimategas): Will estimate the gas used when the method would be executed on the blockchain.                                                                                  |
| Function | [encodeABI](#methods-mymethod-encodeabi): Encodes the ABI for this method. 트랜잭션을 사용하여 메소드를 호출하거나 인수로써 다른 스마트 컨트랙트 메소드에 전달될 수 있습니다.                                                                             |

**예시**

```javascript
// calling a method
> myContract.methods.myMethod(123).call({from: '0xde0B295669a9FD93d5F28D9Ec85E40f4cb697BAe'}, function(error, result) {
      ...
  });

// or sending and using a promise
> myContract.methods.myMethod(123).send({from: '0xde0B295669a9FD93d5F28D9Ec85E40f4cb697BAe'})
  .then(function(receipt) {
    // receipt can also be a new contract instance, when coming from a "contract.deploy({...}).send()"
  });

// or sending and using the events
> myContract.methods.myMethod(123).send({from: '0xde0B295669a9FD93d5F28D9Ec85E40f4cb697BAe'})
  .on('transactionHash', function(hash) {
      ...
  })
  .on('receipt', function(receipt) {
      ...
  })
  .on('error', console.error);
```

## methods.myMethod.call <a id="methods-mymethod-call"></a>

```javascript
myContract.methods.myMethod([param1 [, param2 [, ...]]]).call(options [, callback])
```

Will call a "constant" method and execute its smart contract method in the Klaytn Virtual Machine without sending any transaction. Note that calling cannot alter the smart contract state.

**파라미터**

| 이름       | 타입       | 설명                                                                                                                                                                       |
|:-------- |:-------- |:------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| options  | Object   | \(optional\) The options used for calling.  자세한 내용은 아래 표를 참조하세요.                                                                                                       |
| callback | Function | \(optional\) This callback will be fired with the result of the smart contract method execution as the second argument, or with an error object as the first argument. |

옵션 개체에는 다음이 포함됩니다:

| 이름    | 타입     | 설명                                                                                   |
|:----- |:------ |:------------------------------------------------------------------------------------ |
| from  | String | \(optional\) The address the call “transaction” should be made from.               |
| 가스 가격 | String | \(optional\) The gas price in peb to use for this call "transaction".              |
| gas   | Number | \(optional\) The maximum gas provided for this call "transaction" \(gas limit\). |

**리턴값**

`Promise` returns `Mixed`: The return value\(s\) of the smart contract method. 하나를 반환하면, 그대로 반환됩니다. If it has multiple return values, they are returned as an object with properties and indices.

**예시**

```javascript
// using the callback
> myContract.methods.myMethod(123).call({from: '0xde0B295669a9FD93d5F28D9Ec85E40f4cb697BAe'}, function(error, result) {
      ...
  });

// using the promise
> myContract.methods.myMethod(123).call({from: '0xde0B295669a9FD93d5F28D9Ec85E40f4cb697BAe'})
  .then(function(result) {
      ...
  });
```

```text
// Solidity: MULTI-ARGUMENT RETURN
contract MyContract {
    function myFunction() returns(uint256 myNumber, string myString) {
        return (23456, "Hello!%");
    }
}
```

```javascript
> var MyContract = new caver.klay.Contract(abi, address);
> MyContract.methods.myFunction().call().then(console.log);
Result {
      myNumber: '23456',
      myString: 'Hello!%',
      0: '23456', // these are here as fallbacks if the name is not known or given
      1: 'Hello!%'
}
```

```text
// Solidity: SINGLE-ARGUMENT RETURN
contract MyContract {
    function myFunction() returns(string myString) {
        return "Hello!%";
    }
}
```

```javascript
> var MyContract = new caver.klay.Contract(abi, address);
> MyContract.methods.myFunction().call().then(console.log);
"Hello!%"
```

## methods.myMethod.send <a id="methods-mymethod-send"></a>

```javascript
myContract.methods.myMethod([param1 [, param2 [, ...]]]).send(options [, callback])
```

스마트 컨트랙트에 트랜잭션을 보내고 그 메소드를 실행합니다. Note that this can alter the smart contract state.

**파라미터**

| 이름       | 타입       | 설명                                                                                                                          |
|:-------- |:-------- |:--------------------------------------------------------------------------------------------------------------------------- |
| options  | Object   | 전송에 사용되는 옵션.  자세한 내용은 아래 표를 참조하세요.                                                                                          |
| callback | Function | \(optional\) This callback will be fired first with the "transactionHash", or with an error object as the first argument. |

옵션 개체에는 다음이 포함됩니다:

| 이름    | 타입        | 설명                                                                                             |
|:----- |:--------- |:---------------------------------------------------------------------------------------------- |
| from  | String    | 트랜잭션을 보낼 송신자 주소.                                                                               |
| 가스 가격 | String    | \(optional\) The gas price in peb to use for this transaction.                               |
| gas   | Number    | The maximum gas provided for this transaction \(gas limit\).                                 |
| value | Number \ | String \| BN \| BigNumber | \(optional\) The value transferred for the transaction in peb. |

**리턴값**

`callback`은 32바이트 트랜잭션 해시를 반환합니다.

`PromiEvent`: 프로미스(promise)가 조합된 이벤트 이미터(event emitter). Will be resolved when the transaction receipt is available, or if this `send()` is called from a `someContract.deploy()`, then the promise will be resolved with the new contract instance. 추가로 다음과 같은 이벤트를 사용할 수 있습니다:

| 이름              | 타입     | 설명                                                                                                                                                                                                     |
|:--------------- |:------ |:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| transactionHash | String | 트랜잭션이 전송된 직후 및 트랜잭션 해시를 사용할 수 있을 때 발생합니다.                                                                                                                                                              |
| receipt         | Object | 트랜잭션 영수증을 사용할 수 있을 때 발생합니다.  컨트랙트의 영수증에는 `logs` 속성이 없지만, 대신 이벤트 이름을 키로, 이벤트를 속성으로 하는 `events` 속성이 있습니다. See [getPastEvents return values](#getpastevents) for details about the returned event object. |
| error           | 에러     | 전송 중 오류가 발생하면 발생됩니다. 가스 부족 에러(out-of-gas)가 발생한 경우 두 번째 인자는 트랜잭션 영수증입니다.                                                                                                                                |

**예시**

```javascript
// using the callback
> myContract.methods.myMethod(123).send({from: '0xde0B295669a9FD93d5F28D9Ec85E40f4cb697BAe'}, function(error, transactionHash) {
    ...
  });

// using the promise
> myContract.methods.myMethod(123).send({from: '0xde0B295669a9FD93d5F28D9Ec85E40f4cb697BAe'})
  .then(function(receipt) {
    // receipt can also be a new contract instance, when coming from a "contract.deploy({...}).send()"
  });


// using the event emitter
> myContract.methods.myMethod(123).send({from: '0xde0B295669a9FD93d5F28D9Ec85E40f4cb697BAe'})
  .on('transactionHash', function(hash) {
    ...
  })
  .on('receipt', function(receipt) {
    console.log(receipt);
  })
  .on('error', console.error); // If there is an out-of-gas error, the second parameter is the receipt.

// receipt example
{
   "transactionHash": "0x9fc76417374aa880d4449a1f7f31ec597f00b1f6f3dd2d66f4c9c6c445836d8b",
   "transactionIndex": 0,
   "blockHash": "0xef95f2f1ed3ca60b048b4bf67cde2195961e0bba6f70bcbea9a2c4e133e34b46",
   "blockNumber": 3,
   "contractAddress": "0x11f4d0A3c12e86B4b5F39B213F7E19D048276DAe",
   "gasUsed": 30234,
   "events": {
     "MyEvent": {
       returnValues: {
         myIndexedParam: 20,
         myOtherIndexedParam: '0x123456789...',
         myNonIndexParam: 'My String'
       },
       raw: {
         data: '0x7f9fade1c0d57a7af66ab4ead79fade1c0d57a7af66ab4ead7c2c2eb7b11a91385',
         topics: ['0xfd43ade1c09fade1c0d57a7af66ab4ead7c2c2eb7b11a91ffdd57a7af66ab4ead7', '0x7f9fade1c0d57a7af66ab4ead79fade1c0d57a7af66ab4ead7c2c2eb7b11a91385']
       },
       event: 'MyEvent',
       signature: '0xfd43ade1c09fade1c0d57a7af66ab4ead7c2c2eb7b11a91ffdd57a7af66ab4ead7',
       logIndex: 0,
       transactionIndex: 0,
       transactionHash: '0x7f9fade1c0d57a7af66ab4ead79fade1c0d57a7af66ab4ead7c2c2eb7b11a91385',
       blockHash: '0xfd43ade1c09fade1c0d57a7af66ab4ead7c2c2eb7b11a91ffdd57a7af66ab4ead7',
       blockNumber: 1234,
       address: '0xde0B295669a9FD93d5F28D9Ec85E40f4cb697BAe'
    },
    "MyOtherEvent": {
      ...
    },
    "MyMultipleEvent":[{...}, {...}] // If there are a multiple of the same events, they will be in an array.
  }
}
```

## methods.myMethod.estimateGas <a id="methods-mymethod-estimategas"></a>

```javascript
myContract.methods.myMethod([param1 [, param2 [, ...]]]).estimateGas(options [, callback])
```

Will estimate the gas that a method execution will take when executed in the Klaytn Virtual Machine. The estimation can differ from the actual gas used when later sending a transaction, as the state of the smart contract can be different at that time.

**파라미터**

| 이름       | 타입       | 설명                                                                                                                                                      |
|:-------- |:-------- |:------------------------------------------------------------------------------------------------------------------------------------------------------- |
| options  | Object   | \(optional\) The options used for calling.  자세한 내용은 아래 표를 참조하세요.                                                                                      |
| callback | Function | \(optional\) This callback will be fired with the result of the gas estimation as the second argument, or with an error object as the first argument. |

옵션 개체에는 다음이 포함됩니다:

| 이름    | 타입        | 설명                                                                                                                                                  |
|:----- |:--------- |:--------------------------------------------------------------------------------------------------------------------------------------------------- |
| from  | String    | \(optional\) The address from which the call "transaction" should be made.                                                                        |
| gas   | Number    | \(optional\) The maximum gas provided for this call "transaction" \(gas limit\). 특정 값을 설정하면 가스 부족 오류를 감지하는 데 도움이 됩니다. 모든 가스가 사용되면 같은 숫자를 반환합니다. |
| value | Number \ | String \| BN \| BigNumber | \(optional\) The value transferred for the call "transaction" in peb.                                               |

**리턴값**

`Promise`는 `Number`를 반환합니다 - 모의 호출/트랜잭션에 사용된 가스.

**예시**

```javascript
// using the callback
> myContract.methods.myMethod(123).estimateGas({gas: 5000000}, function(error, gasAmount) {
    if(gasAmount == 5000000)
      console.log('Method ran out of gas');
  });

// using the promise
> myContract.methods.myMethod(123).estimateGas({from: '0xde0B295669a9FD93d5F28D9Ec85E40f4cb697BAe'})
  .then(function(gasAmount) {
    ...
  })
  .catch(function(error) {
    ...
  });
```

## methods.myMethod.encodeABI <a id="methods-mymethod-encodeabi"></a>

```javascript
myContract.methods.myMethod([param1 [, param2[, ...]]]).encodeABI()
```

이 메소드에 대한 ABI를 인코딩합니다. This can be used to send a transaction, call a method, or pass it into another smart contract method as arguments.

**파라미터**

없음

**리턴값**

| 타입     | 설명                                  |
|:------ |:----------------------------------- |
| String | 트랜잭션 또는 호출을 통해 전송할 인코딩된 ABI 바이트 코드. |

**예시**

```javascript
> myContract.methods.myMethod(123).encodeABI();
'0x58cf5f1000000000000000000000000000000000000000000000000000000000000007B'
```

## once <a id="once"></a>

```javascript
myContract.once(event [, options], callback)
```

Subscribes to an event and unsubscribes immediately after the first event or error. 단일 이벤트에 대해서만 발생합니다.

**파라미터**

| 이름       | 타입       | 설명                                                                                                                                           |
|:-------- |:-------- |:-------------------------------------------------------------------------------------------------------------------------------------------- |
| event    | String   | 컨트랙트, 또는 모든 이벤트를 받기 위한 `"allEvents"`에서의 이벤트 이름.                                                                                              |
| options  | Object   | \(optional\) The options used for deployment.  자세한 내용은 아래 표를 참조하세요.                                                                        |
| callback | Function | 이 콜백은 첫 번째 이벤트를 두 번째 인수로, 또는 오류를 첫 번째 인수로 하여 발생됩니다. See [getPastEvents return values](#getpastevents) for details about the event structure. |

옵션 개체에는 다음이 포함됩니다:

| 이름     | 타입     | 설명                                                                                                                                                  |
|:------ |:------ |:--------------------------------------------------------------------------------------------------------------------------------------------------- |
| 필터     | Object | \(optional\) Lets you filter events by indexed parameters, _e.g._, `{filter: {myNumber: [12,13]}}` means all events where "myNumber" is 12 or 13. |
| topics | Array  | \(optional\) This allows you to manually set the topics for the event filter. 필터 특성 및 이벤트 서명이 제공되면, `topic[0]` 가 자동으로 설정되지 않습니다.                  |

**리턴값**

`undefined`

**예시**

```javascript
> myContract.once('MyEvent', {
    filter: {myIndexedParam: [20,23], myOtherIndexedParam: '0x123456789...'}, // Using an array means OR: e.g. 20 or 23
  }, function(error, event) { console.log(event); });

// event output example
{
    returnValues: {
        myIndexedParam: 20,
        myOtherIndexedParam: '0x123456789...',
        myNonIndexParam: 'My String'
    },
    raw: {
        data: '0x7f9fade1c0d57a7af66ab4ead79fade1c0d57a7af66ab4ead7c2c2eb7b11a91385',
        topics: ['0xfd43ade1c09fade1c0d57a7af66ab4ead7c2c2eb7b11a91ffdd57a7af66ab4ead7', '0x7f9fade1c0d57a7af66ab4ead79fade1c0d57a7af66ab4ead7c2c2eb7b11a91385']
    },
    event: 'MyEvent',
    signature: '0xfd43ade1c09fade1c0d57a7af66ab4ead7c2c2eb7b11a91ffdd57a7af66ab4ead7',
    logIndex: 0,
    transactionIndex: 0,
    transactionHash: '0x7f9fade1c0d57a7af66ab4ead79fade1c0d57a7af66ab4ead7c2c2eb7b11a91385',
    blockHash: '0xfd43ade1c09fade1c0d57a7af66ab4ead7c2c2eb7b11a91ffdd57a7af66ab4ead7',
    blockNumber: 1234,
    address: '0xde0B295669a9FD93d5F28D9Ec85E40f4cb697BAe'
}
```

## events <a id="events"></a>

```javascript
myContract.events.MyEvent([options][, callback])
```

이벤트를 구독합니다.

**파라미터**

| 이름       | 타입       | 설명                                                                                                                   |
|:-------- |:-------- |:-------------------------------------------------------------------------------------------------------------------- |
| options  | Object   | \(optional\) The options used for deployment.  자세한 내용은 아래 표를 참조하세요.                                                |
| callback | Function | \(optional\) This callback will be fired for each event as the second argument, or an error as the first argument. |

옵션 개체에는 다음이 포함됩니다:

| 이름        | 타입     | 설명                                                                                                                                                  |
|:--------- |:------ |:--------------------------------------------------------------------------------------------------------------------------------------------------- |
| 필터        | Object | \(optional\) Lets you filter events by indexed parameters, _e.g._, `{filter: {myNumber: [12,13]}}` means all events where "myNumber" is 12 or 13. |
| fromBlock | Number | \(optional\) The block number from which to get events on.                                                                                        |
| topics    | Array  | \(optional\) This allows to manually set the topics for the event filter. 필터 특성 및 이벤트 서명이 제공되면, `topic[0]` 가 자동으로 설정되지 않습니다.                      |

**리턴값**

`EventEmitter`: 이벤트 이미터는 다음 이벤트를 가집니다:

| 이름    | 타입     | 설명                           |
|:----- |:------ |:---------------------------- |
| 데이터   | Object | 이벤트 객체를 인수로 각 수신 이벤트를 발생합니다. |
| error | Object | 구독 오류가 발생하면 발생합니다.           |

반환된 이벤트 `Object`의 구조는 다음과 같습니다:

| 이름               | 타입             | 설명                                                                                                                              |
|:---------------- |:-------------- |:------------------------------------------------------------------------------------------------------------------------------- |
| event            | String         | 이벤트 이름.                                                                                                                         |
| signature        | String \      | `null` | The event signature, `null` if it is an anonymous event.                                                               |
| address          | String         | 이 이벤트가 발생한 주소.                                                                                                                  |
| returnValues     | Object         | The return values coming from the event, _e.g._, `{myVar: 1, myVar2: '0x234...'}`.                                              |
| logIndex         | Number         | 블록에서 이벤트 인덱스 위치의 정수값.                                                                                                           |
| transactionIndex | Number         | 이벤트가 생성된 트랜잭션의 인덱스 위치의 정수값.                                                                                                     |
| transactionHash  | 32-byte String | 이 이벤트가 생성된 블록의 해시. 아직 보류 중인 경우 `null`.                                                                                          |
| blockHash        | 32-byte String | 이 이벤트가 생성된 블록의 해시. 아직 보류 중인 경우 `null`.                                                                                          |
| blockNumber      | Number         | 이 로그가 생성된 블록 번호. 아직 보류 중인 경우 `null`.                                                                                            |
| raw.data         | String         | 색인화되지 않은 로그 매개변수를 포함하는 데이터.                                                                                                     |
| raw.topics       | Array          | 최대 4개의 32바이트 주제를 가진 배열, 주제 1-3은 이벤트의 색인화된 매개변수가 포함됩니다.                                                                          |
| id               | String         | 로그 식별자. It is made through concatenating "log\_" string with `keccak256(blockHash + transactionHash + logIndex).substr(0, 8)` |

**예시**

```javascript
> myContract.events.MyEvent({
    filter: {myIndexedParam: [20,23], myOtherIndexedParam: '0x123456789...'}, // Using an array means OR: e.g. 20 or 23
    fromBlock: 0
  }, function(error, event) { console.log(event); })
  .on('data', function(event){
      console.log(event); // same results as the optional callback above
  })
  .on('error', console.error);

// event output example
{
    returnValues: {
        myIndexedParam: 20,
        myOtherIndexedParam: '0x123456789...',
        myNonIndexParam: 'My String'
    },
    raw: {
        data: '0x7f9fade1c0d57a7af66ab4ead79fade1c0d57a7af66ab4ead7c2c2eb7b11a91385',
        topics: ['0xfd43ade1c09fade1c0d57a7af66ab4ead7c2c2eb7b11a91ffdd57a7af66ab4ead7', '0x7f9fade1c0d57a7af66ab4ead79fade1c0d57a7af66ab4ead7c2c2eb7b11a91385']
    },
    event: 'MyEvent',
    signature: '0xfd43ade1c09fade1c0d57a7af66ab4ead7c2c2eb7b11a91ffdd57a7af66ab4ead7',
    logIndex: 0,
    transactionIndex: 0,
    transactionHash: '0x7f9fade1c0d57a7af66ab4ead79fade1c0d57a7af66ab4ead7c2c2eb7b11a91385',
    blockHash: '0xfd43ade1c09fade1c0d57a7af66ab4ead7c2c2eb7b11a91ffdd57a7af66ab4ead7',
    blockNumber: 1234,
    address: '0xde0B295669a9FD93d5F28D9Ec85E40f4cb697BAe',
    id: 'log_41d221bc',
}
```

## events.allEvents <a id="events-allevents"></a>

```javascript
myContract.events.allEvents([options] [, callback])
```

Same as [events](#events) but receives all events from this smart contract. 선택적으로 filter 속성은 해당 이벤트를 필터링할 수 있습니다.

## getPastEvents <a id="getpastevents"></a>

```javascript
myContract.getPastEvents(event [, options] [, callback])
```

이 컨트랙트의 이전 이벤트를 가져옵니다.

**파라미터**

| 이름       | 타입       | 설명                                                                                                                                |
|:-------- |:-------- |:--------------------------------------------------------------------------------------------------------------------------------- |
| event    | String   | 컨트랙트, 또는 모든 이벤트를 받기 위한 `"allEvents"`에서의 이벤트 이름.                                                                                   |
| options  | Object   | \(optional\) The options used for deployment.  자세한 내용은 아래 표를 참조하세요.                                                             |
| callback | Function | \(optional\) This callback will be fired with an array of event logs as the second argument, or an error as the first argument. |

옵션 개체에는 다음이 포함됩니다:

| 이름        | 타입     | 설명                                                                                                                                                  |
|:--------- |:------ |:--------------------------------------------------------------------------------------------------------------------------------------------------- |
| 필터        | Object | \(optional\) Lets you filter events by indexed parameters, _e.g._, `{filter: {myNumber: [12,13]}}` means all events where "myNumber" is 12 or 13. |
| fromBlock | Number | \(optional\) The block number from which to get events on.                                                                                        |
| toBlock   | Number | \(optional\) The block number to get events up to \(defaults to `"latest"`\).                                                                   |
| topics    | Array  | \(optional\) This allows manually setting the topics for the event filter. 필터 특성 및 이벤트 서명이 제공되면, `topic[0]` 가 자동으로 설정되지 않습니다.                     |

**리턴값**

`Promise` returns `Array`: An array with the past event objects, matching the given event name and filter.

**예시**

```javascript
> myContract.getPastEvents('MyEvent', {
      filter: {myIndexedParam: [20,23], myOtherIndexedParam: '0x123456789...'}, // Using an array means OR: e.g. 20 or 23
      fromBlock: 0,
      toBlock: 'latest'
  }, function(error, events) { console.log(events); })
  .then(function(events) {
      console.log(events) // same results as the optional callback above
  });

[{
    returnValues: {
        myIndexedParam: 20,
        myOtherIndexedParam: '0x123456789...',
        myNonIndexParam: 'My String'
    },
    raw: {
        data: '0x7f9fade1c0d57a7af66ab4ead79fade1c0d57a7af66ab4ead7c2c2eb7b11a91385',
        topics: ['0xfd43ade1c09fade1c0d57a7af66ab4ead7c2c2eb7b11a91ffdd57a7af66ab4ead7', '0x7f9fade1c0d57a7af66ab4ead79fade1c0d57a7af66ab4ead7c2c2eb7b11a91385']
    },
    event: 'MyEvent',
    signature: '0xfd43ade1c09fade1c0d57a7af66ab4ead7c2c2eb7b11a91ffdd57a7af66ab4ead7',
    logIndex: 0,
    transactionIndex: 0,
    transactionHash: '0x7f9fade1c0d57a7af66ab4ead79fade1c0d57a7af66ab4ead7c2c2eb7b11a91385',
    blockHash: '0xfd43ade1c09fade1c0d57a7af66ab4ead7c2c2eb7b11a91ffdd57a7af66ab4ead7',
    blockNumber: 1234,
    address: '0xde0B295669a9FD93d5F28D9Ec85E40f4cb697BAe'
},{
      ...
}]
```

