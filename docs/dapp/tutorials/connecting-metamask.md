# Connecting MetaMask

> **참고**: MetaMask는 주로 이더리움 지갑으로서 사용되지만, 동일한 주소 구조를 지닌 Klaytn과도 호환 가능합니다. Klaytn also has a browser extension wallet called [Kaikas](../developer-tools/#kaikas), so it basically provides the same features as MetaMask, except for Remix.

## 1단계: 메타마스크 설치하기 <a href="#install-metamask" id="install-metamask"></a>

* We will be using Chrome browser in this example. ([**Install Chrome**](https://www.google.com/intl/en\_us/chrome/))
*   Chrome 확장 프로그램 탭에서 [**MetaMask 확장 프로그램**](https://chrome.google.com/webstore/detail/metamask/nkbihfbeogaeaoehlefnkodbefgpgknn?hl=en)을 추가합니다.

    > **참고:** 다른 브라우저를 사용하는 경우 별도 설치가 필요할 수 있습니다.
* You can start MetaMask by clicking on the icon in the upper right-hand corner of your chrome browser.

## 2단계: 메타마스크 지갑 생성 <a href="#generate-a-metamask" id="generate-a-metamask"></a>

![Create a Wallet](../../bapp/tutorials/img/new-to-metamask.png)

* Click on \[Create a Wallet].
* 암호를 생성합니다.
*   12개의 단어로 구성된 시드 구문이 주어지면 이를 안전한 곳에 적습니다.

    > **참고:** 해당 구문을 알아야만 지갑 복구가 가능합니다. 타인에게 노출 시 계정의 자금을 모두 잃을 수 있습니다. 그렇기에 시드 구문은 수기로 적어두거나 외부 연결이 차단된 장치에 기록하기를 권장합니다.

![Seed phrase and Wallet](../../bapp/tutorials/img/metamask-secret-backup.png)

## 3단계: Connect to Klaytn Cypress Network (Mainnet) <a href="#connect-to-klaytn-cypress-network-mainnet" id="connect-to-klaytn-cypress-network-mainnet"></a>

> Here's a simple way. [Connect your wallet to the Klaytn Cypress Network (Mainnet)](https://chainlist.org/chain/8217).

* Click on the upper Networks tab, which is on Ethereum Mainnet as default, and select \[Add network].
* Enter the Endpoint Node (EN) data of the Klaytn chain.
  * Cypress
    * 네트워크 이름: Klaytn Cypress
    * 새 RPC URL: (기본값: [https://public-node-api.klaytnapi.com/v1/cypress](https://public-node-api.klaytnapi.com/v1/cypress))
    * 블록 탐색기 URL: [https://scope.klaytn.com/](https://scope.klaytn.com/)
    * 체인 ID: 8217
    * Currency Symbol: KLAY
* Click \[Save] to add Klaytn Cypress Network.

![Network Setup and Custom RPC](../../bapp/tutorials/img/metamask-add-cypress-1.png) ![Network Setup and Custom RPC](../../bapp/tutorials/img/metamask-add-cypress-2.png)

## 4단계: Send KLAY <a href="#send-klay" id="send-klay"></a>

**주의:** 다음 단계들은 KLAY를 필요로 합니다.

* Click \[Send] on the main page and enter the recipient address and the amount of KLAY.

![Send KLAY 1](img/metamask-send-klay-1.png)

**NOTE:** Sending KLAY requires a transaction, for which you need KLAY.

* Since Klaytn v1.9.0, a [dynamic gas fee mechanism](https://medium.com/klaytn/dynamic-gas-fee-pricing-mechanism-1dac83d2689) has replaced the existing fixed price policy.
* So you don't have to set the fixed gas fee manually.
* Check the amount to send and the transaction fee and click \[Confirm] to complete the KLAY transfer, after which you will be redirected to the main page.
* Click \[Activity] on the main page to confirm the transaction history.

![Send KLAY 2](img/metamask-send-klay-2.png)

## Connect to Klaytn Baobab Network (Testnet) <a href="#connect-to-klaytn-baobab-network-testnet" id="connect-to-klaytn-baobab-network-testnet"></a>

### Obtain KLAY to make a transaction

> **Note:** This tutorial uses Public EN of the Testnet (Baobab) to connect to the network. Make sure to use Baobab when you are running a test.

> Here's a simple way. [Connect your wallet to the Klaytn Baobab Network (Testnet)](https://chainlist.org/chain/1001).

* Baobab
  * Network Name: Klaytn Baobab
  * New RPC URL: [https://api.baobab.klaytn.net:8651](https://api.baobab.klaytn.net:8651)
  * Block Explorer URL: [https://baobab.scope.klaytn.com/](https://baobab.scope.klaytn.com/)
  * Chain ID: 1001
  * Currency Symbol: KLAY
* Click \[Save] to add Klaytn Baobab Network.

![Network Setup](img/connect-testnet-1.png)

* To test the connection of the Klaytn Wallet, you will need to make a transaction, which requires KLAY.
* Click on the kebab menu (three dots) in the upper right corner and select \[Account details].
* Click \[Export Private Key] to obtain your private key.

![Export Private Key](img/connect-testnet-2.png)

* When using Baobab Testnet, you can obtain Test Klay in [**Klaytn Faucet**](https://baobab.wallet.klaytn.foundation/access?next=faucet).
* Enter your private key on Klaytn Wallet and log in by clicking \[Access]. (Attach 0x in front of the private key.)
* Click \[Run Faucet]. 150 Testnet KLAY will be sent to your account and the balance will be updated accordingly. You can claim Testnet KLAY from Faucet once every 24 hours per account.

![Obtain KLAY from Faucet](img/connect-testnet-3.png)

* Come back to MetaMask and confirm the KLAY that you received.

![Check your balance](img/connect-testnet-4.png)
