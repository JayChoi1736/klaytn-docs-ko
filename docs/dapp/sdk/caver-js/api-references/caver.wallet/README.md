# caver.wallet

`caver.wallet` is a package that manages [Keyring](keyring.md) instances in in-memory wallet. `caver.wallet` accepts all [SingleKeyring](keyring.md#singlekeyring), [MultipleKeyring](keyring.md#multiplekeyring), and [RoleBasedKeyring](keyring.md#rolebasedkeyring), and manages them by address.

## Class <a href="#class" id="class"></a>

### KeyringContainer <a href="#keyringcontainer" id="keyringcontainer"></a>

```javascript
caver.wallet
```

`KeyringContainer` is a class that manages [SingleKeyring](keyring.md#singlekeyring), [MultipleKeyring](keyring.md#multiplekeyring), and [RoleBasedKeyring](keyring.md#rolebasedkeyring) instances. Caver가 초기화될 때 `caver.wallet` 안에 KeyringContainer 인스턴스를 생성합니다. `caver.wallet`를 통해 인메모리 지갑에 키링 인스턴스를 저장하고 관리할 수 있습니다.

**속성**

| 이름     | 타입     | 설명                              |
| ------ | ------ | ------------------------------- |
| length | number | keyringContainer에 포함된 키링의 수입니다. |

## caver.wallet.generate <a href="#caver-wallet-generate" id="caver-wallet-generate"></a>

```javascript
caver.wallet.generate(numberOfKeyrings [, entropy])
```

Generates instances of [SingleKeyring](keyring.md#singlekeyring) in the keyringContainer with randomly generated private keys.

**파라미터**

| 이름               | 타입     | 설명                                                                           |
| ---------------- | ------ | ---------------------------------------------------------------------------- |
| numberOfKeyrings | number | The number of [SingleKeyring](keyring.md#singlekeyring) instances to create. |
| entropy          | string | (선택 사항) 엔트로피를 증가시키는 임의의 문자열입니다.                                              |

**리턴값**

| 타입    | 설명                        |
| ----- | ------------------------- |
| Array | 생성된 인스턴스의 주소를 포함하는 배열입니다. |

**예시**

```javascript
// generate without entropy
> caver.wallet.generate(3)
[
    '0xb4b0c3781082cf818bfaf5adfc73fdf59d92c1cd',
    '0x9957dfd92e4b70f91131c573293343bc5f21f215',
    '0xed2fe179c18fa528da2392532998560bd1008511'
]

// generate with entropy
> caver.wallet.generate(3, caver.utils.randomHex(32))
[
    '0xb4b0c3781082cf818bfaf5adfc73fdf59d92c1cd',
    '0x9957dfd92e4b70f91131c573293343bc5f21f215',
    '0xed2fe179c18fa528da2392532998560bd1008511'
]
```

## caver.wallet.newKeyring <a href="#caver-wallet-newkeyring" id="caver-wallet-newkeyring"></a>

```javascript
caver.wallet.newKeyring(address, key)
```

주어진 파라미터로 키링 인스턴스를 생성하며 `caver.wallet`에 추가한다.

If `key` is a private key string, a [SingleKeyring](keyring.md#singlekeyring) instance that uses a single private key is created. If `key` is an array containing private key strings, a [MultipleKeyring](keyring.md#multiplekeyring) instance that use multiple private keys is created. If `key` is a 2D array of which each element contains the private key(s) to be used for each role, a [RoleBasedKeyring](keyring.md#rolebasedkeyring) instance is created. 사용할 키링은 `caver.wallet`에 추가해야 합니다.

**파라미터**

| 이름      | 타입        | 설명                                                                                                                                                                                         |
| ------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| address | string    | 주소 문자열입니다.                                                                                                                                                                                 |
| key     | string \ | Array | The private key string, an array of private keys, or a 2D array of which each array element contains keys defined for each [role](../../../../../klaytn/design/accounts.md#roles). |

**리턴값**

| 타입 | 설명                                                                                                                                                                                                    |
| -- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 객체 | The keyring instance ([SingleKeyring](keyring.md#singlekeyring), [MultipleKeyring](keyring.md#multiplekeyring) or [RoleBasedKeyring](keyring.md#rolebasedkeyring)) added to caver.wallet is returned. |

**예시**

```javascript
// Create a instance of SingleKeyring and add to caver.wallet
> caver.wallet.newKeyring('0x{address in hex}', '0x{private key}')
SingleKeyring {
    _address: '0x386a4bb40abbfaa59cecdc3ced202475895fd569',
    _key: PrivateKey { _privateKey: '0x{private key}' }
}

// Create a instance of MultipleKeyring and add to caver.wallet
> caver.wallet.newKeyring('0x{address in hex}', ['0x{private key1}', '0x{private key2}'])
MultipleKeyring {
    _address: '0x17e7531b40ad5d7b5fa7b4ec78df64ce1cb36d24',
    _keys: [ 
        PrivateKey { _privateKey: '0x{private key1}' },
        PrivateKey { _privateKey: '0x{private key2}' }
    ]
}

// Create a instance of RoleBasedKeyring and add to caver.wallet
> const roleBasedKeys = [
    ['0x{private key1}', '0x{private key2}'],
    ['0x{private key3}', '0x{private key4}'],
    ['0x{private key5}', '0x{private key6}'],
]
> caver.wallet.newKeyring('0x{address in hex}', roleBasedKeys)
RoleBasedKeyring {
    _address: '0xe7e9184c125020af5d34eab7848bab799a1dcba9',
    _keys: [
        [
            PrivateKey { _privateKey: '0x{private key1}' },
            PrivateKey { _privateKey: '0x{private key2}' }
        ],
        [ 
            PrivateKey { _privateKey: '0x{private key3}' },
            PrivateKey { _privateKey: '0x{private key4}' }
        ],
        [ 
            PrivateKey { _privateKey: '0x{private key5}' },
            PrivateKey { _privateKey: '0x{private key6}' }
        ]
    ]
}
```

## caver.wallet.updateKeyring <a href="#caver-wallet-updatekeyring" id="caver-wallet-updatekeyring"></a>

```javascript
caver.wallet.updateKeyring(keyring)
```

`caver.wallet` 안에 있는 키링을 업데이트합니다. When a new `keyring` instance ([SingleKeyring](keyring.md#singlekeyring), [MultipleKeyring](keyring.md#multiplekeyring) or [RoleBasedKeyring](keyring.md#rolebasedkeyring)) is passed as a parameter, the existing keyring stored in the `caver.wallet` that matches the `address` property of the given `keyring` instance is found and replaced with the given one. 일치하는 키링을 찾을 수 없는 경우 에러가 발생합니다.

**파라미터**

| 이름      | 타입 | 설명                                                                                                                                                                                            |
| ------- | -- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Keyring | 객체 | The new keyring ([SingleKeyring](keyring.md#singlekeyring), [MultipleKeyring](keyring.md#multiplekeyring) or [RoleBasedKeyring](keyring.md#rolebasedkeyring)) to be stored in `caver.wallet`. |

**리턴값**

| 타입 | 설명                                                                                                                                                                                          |
| -- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 객체 | The updated keyring ([SingleKeyring](keyring.md#singlekeyring), [MultipleKeyring](keyring.md#multiplekeyring) or [RoleBasedKeyring](keyring.md#rolebasedkeyring)) stored in `caver.wallet`. |

**예시**

```javascript
> caver.wallet.updateKeyring(newKeyring)
SingleKeyring {
    _address: '0x386a4bb40abbfaa59cecdc3ced202475895fd569',
    _key: PrivateKey { _privateKey: '0x{private key}' }
}
```

## caver.wallet.getKeyring <a href="#caver-wallet-getkeyring" id="caver-wallet-getkeyring"></a>

```javascript
caver.wallet.getKeyring(address)
```

`caver.wallet` 주소에 일치하는 키링 인스턴스를 반환합니다.

**파라미터**

| 이름      | 타입     | 설명             |
| ------- | ------ | -------------- |
| address | string | 조회할 키링의 주소입니다. |

**리턴값**

| 타입 | 설명                                                                                                                                                                                                 |
| -- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 객체 | The found keyring instance ([SingleKeyring](keyring.md#singlekeyring), [MultipleKeyring](keyring.md#multiplekeyring) or [RoleBasedKeyring](keyring.md#rolebasedkeyring)) stored in `caver.wallet`. |

**예시**

```javascript
> caver.wallet.getKeyring('0x386a4bb40abbfaa59cecdc3ced202475895fd569')
SingleKeyring {
    _address: '0x386a4bb40abbfaa59cecdc3ced202475895fd569',
    _key: PrivateKey { _privateKey: '0x{private key}' }
}
```

## caver.wallet.isExisted <a href="#caver-wallet-isexisted" id="caver-wallet-isexisted"></a>

```javascript
caver.wallet.isExisted(address)
```

Returns `true` if there is a keyring matching the address.

**파라미터**

| 이름      | 타입     | 설명                                         |
| ------- | ------ | ------------------------------------------ |
| address | string | The address of keyring to check existence. |

**리턴값**

| 타입      | 설명                                                                                 |
| ------- | ---------------------------------------------------------------------------------- |
| boolean | `true` means a keyring matching with the address is existed in the `caver.wallet`. |

**예시**

```javascript
> caver.wallet.isExisted('0x386a4bb40abbfaa59cecdc3ced202475895fd569')
true
```

## caver.wallet.add <a href="#caver-wallet-add" id="caver-wallet-add"></a>

```javascript
caver.wallet.add(keyring)
```

Adds an instance of keyring to the `caver.wallet`. If the newly given keyring has the same address with one of the keyrings that already exist in `caver.wallet`, an error is returned. In this case, use [updateKeyring](./#caver-wallet-updatekeyring) to update the existing keyring in `caver.wallet`.

**파라미터**

| 이름      | 타입 | 설명                                                                                                                                                                                         |
| ------- | -- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Keyring | 객체 | A keyring instance ([SingleKeyring](keyring.md#singlekeyring), [MultipleKeyring](keyring.md#multiplekeyring) or [RoleBasedKeyring](keyring.md#rolebasedkeyring)) to add to `caver.wallet`. |

**리턴값**

| 타입 | 설명                                                                                                                                                                                 |
| -- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 객체 | The added keyring ([SingleKeyring](keyring.md#singlekeyring), [MultipleKeyring](keyring.md#multiplekeyring) or [RoleBasedKeyring](keyring.md#rolebasedkeyring)) in `caver.wallet`. |

**예시**

```javascript
> caver.wallet.add(keyring)
SingleKeyring {
    _address: '0x386a4bb40abbfaa59cecdc3ced202475895fd569',
    _key: PrivateKey { _privateKey: '0x{private key}' }
}
```

## caver.wallet.remove <a href="#caver-wallet-remove" id="caver-wallet-remove"></a>

```javascript
caver.wallet.remove(address)
```

Deletes the keyring from `caver.wallet` whose address matches the address of the given keyring.

**파라미터**

| 이름      | 타입     | 설명                                                         |
| ------- | ------ | ---------------------------------------------------------- |
| address | string | An address of the keyring to be deleted in `caver.wallet`. |

**리턴값**

| 타입      | 설명                                                |
| ------- | ------------------------------------------------- |
| boolean | `true` if keyring is removed from `caver.wallet`. |

**예시**

```javascript
> caver.wallet.remove('0x6a3edfad6d1126020d5369e9097db39281876c5d')
true
```

## caver.wallet.signMessage <a href="#caver-wallet-signmessage" id="caver-wallet-signmessage"></a>

```javascript
caver.wallet.signMessage(address, message, role [, index])
```

Signs the message with Klaytn-specific prefix using keyring stored in caver.wallet. 다음 메서드는 Klaytn 고유의 서명을 계산합니다.

```
sign(keccak256("\x19Klaytn Signed Message:\n" + len(message) + message)))
```

If the user has not provided the index parameter, `caver.wallet.signMessage` signs message using all the private keys used by the role. If the index parameter is given, `caver.wallet.signMessage` signs message using only one private key at the given index. The role used in caver-js can be found from `caver.wallet.keyring.role`.

**파라미터**

| 이름      | 타입     | 설명                                                                                                            |
| ------- | ------ | ------------------------------------------------------------------------------------------------------------- |
| address | string | 사용될 키링의 주소입니다.                                                                                                |
| 메시지     | string | 서명할 메시지입니다.                                                                                                   |
| role    | number | 키의 역할을 나타내는 숫자입니다. `caver.wallet.keyring.role`를 사용할 수 있습니다.                                                   |
| index   | number | (선택 사항) 사용하고자 하는 개인키의 인덱스입니다. 인덱스는 각각의 역할에 정의된 개인키들의 배열 길이보다 작아야 합니다. 인덱스가 정의되지 않았을 경우, 이 메서드는 모든 개인키를 사용합니다. |

**리턴값**

| 타입 | 설명                 |
| -- | ------------------ |
| 객체 | 서명 결과를 포함하는 객체입니다. |

반환된 객체는 다음을 포함합니다.

| 이름          | 타입     | 설명                                                     |
| ----------- | ------ | ------------------------------------------------------ |
| messageHash | string | Klaytn 고유의 접두사를 가진 메시지의 해시입니다.                         |
| 서명          | Array  | An array of [SignatureData](keyring.md#signaturedata). |
| 메시지         | string | 서명할 메시지입니다.                                            |

**예시**

```javascript
// Sign message with roleTransactionKey which uses two private keys
> caver.wallet.signMessage('0x386a4bb40abbfaa59cecdc3ced202475895fd569', 'message to sign', caver.wallet.keyring.role.roleTransactionKey)
{
    messageHash: '0x9c4c1ae0aa1faf7e59eaf6fcf36a34542698197b379a9949b58c92925e74c069',
    signatures: [
        SignatureData { _v: '0x1c', _r: '0xb3239...', _s: '0x584d2...' },
        SignatureData { _v: '0x1b', _r: '0x13c64...', _s: '0x60c61...' }
    ],
    message: 'message to sign'
}

// Sign message with roleTransactionKey and index
> caver.wallet.signMessage('0x386a4bb40abbfaa59cecdc3ced202475895fd569', 'message to sign', caver.wallet.keyring.role.roleTransactionKey, 1)
{
    messageHash: '0x9c4c1ae0aa1faf7e59eaf6fcf36a34542698197b379a9949b58c92925e74c069',
    signatures: [
        SignatureData { _v: '0x1b', _r: '0x13c64...', _s: '0x60c61...' }
    ],
    message: 'message to sign'
}
```

## caver.wallet.sign <a href="#caver-wallet-sign" id="caver-wallet-sign"></a>

```javascript
caver.wallet.sign(address, transaction [, index] [, hasher])
```

Signs the transaction as a `sender` of the transaction and appends `signatures` in the transaction object using the keyring in `caver.wallet`.

For [Account Update](../caver.transaction/basic.md#accountupdate) transaction, use [roleTransactionKey](../../../../../klaytn/design/accounts.md#roles), otherwise, use [roleTransactionKey](../../../../../klaytn/design/accounts.md#roles). If the user has not defined an `index`, `caver.wallet.sign` signs the transaction using all the private keys used by the role. If `index` is defined, the `caver.wallet.sign` signs the transaction using only one private key at the given index.

**파라미터**

| 이름      | 타입       | 설명                                                                                                                                                                                                                                                                                                                                                            |
| ------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| address | string   | 사용될 키링의 주소입니다.                                                                                                                                                                                                                                                                                                                                                |
| 트랜잭션    | 객체       | An instance of [Transaction](../caver.transaction/#class).                                                                                                                                                                                                                                                                                                    |
| index   | number   | (선택 사항) 사용하고자 하는 개인키의 인덱스입니다. 인덱스는 각각의 역할에 정의된 개인키들의 배열 길이보다 작아야 합니다. 인덱스가 정의되지 않았을 경우, 이 메서드는 모든 개인키를 사용합니다.                                                                                                                                                                                                                                                 |
| hasher  | function | (optional) A hash function to get the transaction hash. If `hasher` is given as a parameter, it calculates the transaction hash instead of the default method for calculating transaction hash implemented in caver-js. See [Basic](../../../../../klaytn/design/transactions/basic.md) for details about the default method for transaction hash generation. |

**리턴값**

`Promise`는 `객체`를 반환: 서명된 트랜잭션입니다.

| 타입 | 설명                                                                     |
| -- | ---------------------------------------------------------------------- |
| 객체 | 서명된 트랜잭션 데이터입니다. The sign(s) is added to the `transaction.signatures`. |

For more information about fields by transaction type, see [caver.transaction](../caver.transaction/).

**예시**

```javascript
// 이 예시는 ValueTransfer 트랜잭션 사용
// Please refer to [caver.transaction] for how to use various transaction types.
> const transaction = caver.transaction.valueTransfer.create({
    from: '0xe7e9184c125020af5d34eab7848bab799a1dcba9',
    to: '0x3424b91026bdc5ec55df4548e6ebf0f28b60abd7',
    value: 1,
    gas: 30000,
})

> const customHasher = () => { ... }

// Sign a transaction with the address of RoleBasedKeyring which use two private keys for roleTransactionKey
> caver.wallet.sign('0xe7e9184c125020af5d34eab7848bab799a1dcba9', transaction).then(console.log)
ValueTransfer {
    _type: 'TxTypeValueTransfer',
    _from: '0xe7e9184c125020af5d34eab7848bab799a1dcba9',
    _gas: '0x7530',
    _signatures: [
        SignatureData { _v: '0x4e43', _r: '0xd78a2...', _s: '0x379e9...' },
        SignatureData { _v: '0x4e43', _r: '0x70a58...', _s: '0x2ab28...' }
    ],
    _to: '0x3424b91026bdc5ec55df4548e6ebf0f28b60abd7',
    _value: '0x1',
    _chainId: '0x2710',
    _gasPrice: '0x5d21dba00',
    _nonce: '0x0'
}

// Sign a transaction with the address of RoleBasedKeyring which use two private keys for roleTransactionKey and index
> caver.wallet.sign('0xe7e9184c125020af5d34eab7848bab799a1dcba9', transaction, 1).then(console.log)
ValueTransfer {
    _type: 'TxTypeValueTransfer',
    _from: '0xe7e9184c125020af5d34eab7848bab799a1dcba9',
    _gas: '0x7530',
    _signatures: [
        SignatureData { _v: '0x4e43', _r: '0x70a58...', _s: '0x2ab28...' }
    ],
    _to: '0x3424b91026bdc5ec55df4548e6ebf0f28b60abd7',
    _value: '0x1',
    _chainId: '0x2710',
    _gasPrice: '0x5d21dba00',
    _nonce: '0x0'
}

// Sign a transaction with the address of RoleBasedKeyring which use two private keys for roleTransactionKey and hasher
> caver.wallet.sign('0xe7e9184c125020af5d34eab7848bab799a1dcba9', transaction, customHasher).then(console.log)
ValueTransfer {
    _type: 'TxTypeValueTransfer',
    _from: '0xe7e9184c125020af5d34eab7848bab799a1dcba9',
    _gas: '0x7530',
    _signatures: [
        SignatureData { _v: '0x4e44', _r: '0x7a8b6...', _s: '0x17139...' },
        SignatureData { _v: '0x4e43', _r: '0x7f978...', _s: '0x1a532...' }
    ],
    _to: '0x3424b91026bdc5ec55df4548e6ebf0f28b60abd7',
    _value: '0x1',
    _chainId: '0x2710',
    _gasPrice: '0x5d21dba00',
    _nonce: '0x0'
}

// Sign a transaction with the address of RoleBasedKeyring which use two private keys for roleTransactionKey, index and hasher
> caver.wallet.sign('0xe7e9184c125020af5d34eab7848bab799a1dcba9', transaction, 0, customHasher).then(console.log)
ValueTransfer {
    _type: 'TxTypeValueTransfer',
    _from: '0xe7e9184c125020af5d34eab7848bab799a1dcba9',
    _gas: '0x7530',
    _signatures: [
        SignatureData { _v: '0x4e44', _r: '0x7a8b6...', _s: '0x17139...' }
    ],
    _to: '0x3424b91026bdc5ec55df4548e6ebf0f28b60abd7',
    _value: '0x1',
    _chainId: '0x2710',
    _gasPrice: '0x5d21dba00',
    _nonce: '0x0'
}
```

## caver.wallet.signAsFeePayer <a href="#caver-wallet-signasfeepayer" id="caver-wallet-signasfeepayer"></a>

```javascript
caver.wallet.signAsFeePayer(address, transaction [, index] [, hasher])
```

Signs the transaction as `fee payer` of the transaction and appends `feePayerSignatures` in the transaction object using the keyring in `caver.wallet`.

For signing a transaction as a fee payer, use [roleFeePayerKey](../../../../../klaytn/design/accounts.md#roles). If the user has not defined an `index`, `caver.wallet.signAsFeePayer` signs the transaction using all the private keys used by the role. If `index` is defined, the `caver.wallet.signAsFeePayer` signs the transaction using only one private key at the given index.

If the `transaction.feePayer` is not defined, the address of keyring which is founded from `caver.wallet` is assigned.

**파라미터**

| 이름      | 타입       | 설명                                                                                                                                                                                |
| ------- | -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| address | string   | 사용될 키링의 주소입니다.                                                                                                                                                                    |
| 트랜잭션    | 객체       | An instance of [FeeDelegatedTransaction](../caver.transaction/fee-delegation.md).                                                                                                 |
| index   | number   | (선택 사항) 사용하고자 하는 개인키의 인덱스입니다. 인덱스는 각각의 역할에 정의된 개인키들의 배열 길이보다 작아야 합니다. 인덱스가 정의되지 않았을 경우, 이 메서드는 모든 개인키를 사용합니다.                                                                     |
| hasher  | function | (optional) A function to get the transaction hash. If hasher is defined as a parameter, this is used to get the transaction hash instead of a default implementation in caver-js. |

**리턴값**

`Promise`는 `객체`를 반환: 서명된 트랜잭션입니다.

| 타입 | 설명                                                                                       |
| -- | ---------------------------------------------------------------------------------------- |
| 객체 | 서명된 트랜잭션 데이터입니다. The signing result is appended to the `transaction.feePayerSignatures`. |

For more information about fields by transaction type, see [caver.transaction](../caver.transaction/).

**예시**

```javascript
// This example uses the FeeDelegatedValueTransfer transaction.
// Please refer to [caver.transaction] for how to use various transaction types.
> const transaction = caver.transaction.feeDelegatedValueTransfer.create({
    from: '0x6fddbcb99d31b8755c2b840a367f53eea4b4f45c',
    to: '0x3424b91026bdc5ec55df4548e6ebf0f28b60abd7',
    value: 1,
    gas: 30000,
})

> const customHasher = () => { ... }

// Sign a transaction with the address of RoleBasedKeyring which use two private keys for roleFeePayerKey
> caver.wallet.signAsFeePayer('0xe7e9184c125020af5d34eab7848bab799a1dcba9', transaction).then(console.log)
FeeDelegatedValueTransfer {
    _type: 'TxTypeFeeDelegatedValueTransfer',
    _from: '0x6fddbcb99d31b8755c2b840a367f53eea4b4f45c',
    _gas: '0x7530',
    _signatures: [ SignatureData { _v: '0x01', _r: '0x', _s: '0x' } ],
    _feePayer: '0xe7e9184c125020af5d34eab7848bab799a1dcba9',
    _feePayerSignatures: [
        SignatureData { _v: '0x4e44', _r: '0x7010e...', _s: '0x65d6b...' },
        SignatureData { _v: '0x4e43', _r: '0x96ef2...', _s: '0x77f34...' }
    ],
    _to: '0x3424b91026bdc5ec55df4548e6ebf0f28b60abd7',
    _value: '0x1',
    _chainId: '0x2710',
    _gasPrice: '0x5d21dba00',
    _nonce: '0x0'
}

// Sign a transaction with the address of RoleBasedKeyring which use two private keys for roleFeePayerKey, index
> caver.wallet.signAsFeePayer('0xe7e9184c125020af5d34eab7848bab799a1dcba9', transaction, 0).then(console.log)
FeeDelegatedValueTransfer {
    _type: 'TxTypeFeeDelegatedValueTransfer',
    _from: '0x6fddbcb99d31b8755c2b840a367f53eea4b4f45c',
    _gas: '0x7530',
    _signatures: [ SignatureData { _v: '0x01', _r: '0x', _s: '0x' } ],
    _feePayer: '0xe7e9184c125020af5d34eab7848bab799a1dcba9',
    _feePayerSignatures: [
        SignatureData { _v: '0x4e44', _r: '0x7010e...', _s: '0x65d6b...' }
    ],
    _to: '0x3424b91026bdc5ec55df4548e6ebf0f28b60abd7',
    _value: '0x1',
    _chainId: '0x2710',
    _gasPrice: '0x5d21dba00',
    _nonce: '0x0'
}

// Sign a transaction with the address of RoleBasedKeyring which use two private keys for roleFeePayerKey and hasher
> caver.wallet.signAsFeePayer('0xe7e9184c125020af5d34eab7848bab799a1dcba9', transaction, customHasher).then(console.log)
FeeDelegatedValueTransfer {
    _type: 'TxTypeFeeDelegatedValueTransfer',
    _from: '0x6fddbcb99d31b8755c2b840a367f53eea4b4f45c',
    _gas: '0x7530',
    _signatures: [ SignatureData { _v: '0x01', _r: '0x', _s: '0x' } ],
    _feePayer: '0xe7e9184c125020af5d34eab7848bab799a1dcba9',
    _feePayerSignatures: [
        SignatureData { _v: '0x4e43', _r: '0xe48bf...', _s: '0x1cf36...' },
        SignatureData { _v: '0x4e43', _r: '0x82976...', _s: '0x3c5e0...' }
    ],
    _to: '0x3424b91026bdc5ec55df4548e6ebf0f28b60abd7',
    _value: '0x1',
    _chainId: '0x2710',
    _gasPrice: '0x5d21dba00',
    _nonce: '0x0'
}

// Sign a transaction with the address of RoleBasedKeyring which use two private keys for roleFeePayerKey, index and hasher
> caver.wallet.signAsFeePayer('0xe7e9184c125020af5d34eab7848bab799a1dcba9', transaction, 0, customHasher).then(console.log)
FeeDelegatedValueTransfer {
    _type: 'TxTypeFeeDelegatedValueTransfer',
    _from: '0x6fddbcb99d31b8755c2b840a367f53eea4b4f45c',
    _gas: '0x7530',
    _signatures: [ SignatureData { _v: '0x01', _r: '0x', _s: '0x' } ],
    _feePayer: '0xe7e9184c125020af5d34eab7848bab799a1dcba9',
    _feePayerSignatures: [
        SignatureData { _v: '0x4e43', _r: '0x82976...', _s: '0x3c5e0...' }
    ],
    _to: '0x3424b91026bdc5ec55df4548e6ebf0f28b60abd7',
    _value: '0x1',
    _chainId: '0x2710',
    _gasPrice: '0x5d21dba00',
    _nonce: '0x0'
}
```
