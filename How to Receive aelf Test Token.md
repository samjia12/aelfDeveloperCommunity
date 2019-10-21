# Test Token Tutorial (aelf Bug Bounty)

This page is to teach you how to receive test token, so you can use to participate in aelf Bug Bounty Program

## Test Token Names and Their Purposes

Mainchain Test Token Name: TELF

Uses: Can be used for samechain / cross-chain transaction, purchase resources, vote, as a transaction fee and other scenarios. 

Sidechains Test Token Names: STA/STB

Uses: Can be used for samechain / cross-chain transaction, can be used as a transaction fee and other scenarios.


Note:

STA and STB are tokens for two side chains, which can be used for transaction fee. When making transactions, 0.1 of the token will be charged for gas fee. When the contract implements by acs1 standard, the fee will be charged based on the amount of tokens.


## When Can You Receive the Test Token
Oct 24th - Nov 5th

## How Many Test Tokens Can You Get
You can get 100 of each token for different chains. 

## How to Receive Test Token

1. Address: https://apply-token-test.aelf.io/

2. You must have a aelf Wallet. Quickly receive the test token in two steps:

a) If you already have a wallet:
        Just go ahead and fill in your address wallet directly, CLICK ```Continue to get token``` to receive test token
        
![alt text](https://images-cdn.shimo.im/d9ldYVq6wMEkFzcD/image.png)

b) If you don't have a wallet:
You can generate a test wallet in aelf blockchain system
CLICK   ```Click to get a new wallet```  , you will get your own 
 ```Wallet Info```  which tells your test wallet mnemonic, privatekey and address. Please make sure you store those info.
Then, follow the step  ```a```  to get your test token

![alt text](https://images-cdn.shimo.im/A82yNEYBYqItiYPn/image.png__thumbnail)

Apply Result：
![alt text](https://images-cdn.shimo.im/UWb1dRvJYt8a6r4v/image.png__thumbnail
)

## Check Your Test Token on Your aelf Wallet
You will receive your test tokens on aelf mainchain and both sidechains, check it out on the corresponding three wallet URL addresses:

Https://wallet-test.aelf.io/

Https://wallet-test-side01.aelf.io/

Https://wallet-test-side02.aelf.io/

Note:
1. For this Bug Bounty Program, your aelf Wallet info (mnemonic and privateKey) can only be used on aelf mainchain H5 wallet (mobile version)

2. Do not use aelf wallet in the invisible mode, the invisible mode cannot store your wallet information

![alt text](https://images-cdn.shimo.im/FmZvXLNcrkgVyo1w/image.png__thumbnail)

## Check Your Test Token on aelf Block Explorer
Go to  ```https://apply-token-test.aelf.io/``` . Go to ```Open Test Websites```, then, you will be able to test out aelf Mainchain explorer, Mainchain wallet, Sidechain explorers, and Sidechain wallets
         
![alt text](https://uploader.shimo.im/f/XIsY4Q6hcT43CHh2.png!thumbnail)

aelf v0.8.0 beta ：

https://github.com/AElfProject/AElf 

aelf-boilerplate：

https://github.com/AElfProject/aelf-boilerplate

aelf Wallet ：

https://github.com/AElfProject/aelf-web-wallet

aelf Explorer： 

https://github.com/AElfProject/aelf-block-explorer

Documents：

https://docs.aelf.io/

## Instructions of Cross-connect Transaction:
Cross-chain transactions on H5 wallet is not supported.

If you want to experience cross-chain transactions, you can use SDK to realize cross-chain transaction.

SDK codebase:
https://github.com/AElfProject/aelf-sdk-cross-chain.js

Cross-chain transactions require tokens from the originating chain and the target chain (for example, tolens being sent from mainchain to a sidechain will consumes TELF and STA/STB).
