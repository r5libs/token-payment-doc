## API 驗證交易
- 格式
```bash
[POST] /verification

Ex: /verification/
Body:
{
  data: '1ZEFDMTdGOTU4RDJlZTUyM2EyMjA2MjA2OTk0NTk3QzEzRDgzMWVjN2U1Y2FFM0EzZDM0NDc0Zjk2ZjU0YjgyMUM2MzkxMDQxNkJGMDMwQzA5RTQzY0ZEOEQ3RmZhZTY3QjQ5N0I1MTdBMTcxZjlhQTg3OTU3NDE0NzM2NDIzMjkzMzBlZTNmMjRjNTFhZTc0MTViNGJkZjNmMjUyNzc4YTk4ODZjMWY4ZDRlNzA4OTUzMzgyNjJjYzEyMzQ1'
  callbackUrl: 'http://192.168.1.114:5115/verification/callback'
}
```

- 參數(JSON)
```js
{
  data: '', // 執行 TP_erc_MetaMask.transfer(...) 的返回值
  callbackUrl: '' // 後台回調網址
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

- 後台回調
[POST] callbackUrl
參數(JSON)
```bash
{
  result: {
    addressType: 地址類型. 1:erc, 2:trc
    contractAddress: 合約地址
    from: 轉出地址
    to: 轉入地址
    amount: 交易量
    txHash: 交易序號
    authKey: 認證Key
  },
  status: 'ok'
}

或

{
  error: {
    code: 錯誤碼. -1: 檢查交易過程發生錯誤, -2: 提交的交易資料不符
    message: 錯誤訊息
    txHash: 交易序號
    authKey: 認證Key
  },
  status: 'error'
}
```

## API 查詢U幣
- 格式
```bash
[GET] /{ownerAddress}/balance?{addressType}=&{contractAddress}=

Ex: /0xadb2b42f6bd96f5c65920b9ac88619dce4166f94/balance?addressType=1&contractAddress=0xdAC17F958D2ee523a2206206994597C13D831ec7
```

- 參數(Query String)
```bash
addressType: 地址類型. 1:erc, 2:trc
contractAddress: 合約地址
ownerAddress: 錢包地址
```

- 返回值(JSON)
```bash
{
  result: {
    addressType: 地址類型. 1:erc, 2:trc
    contractAddress: 合約地址
    ownerAddress: 錢包地址
    balance: 餘額
  },
  status: 'ok'
}

或

{
  error: {
    message: 錯誤訊息
  },
  status: 'error'
}
```

## API U幣轉移
- 格式
```bash
[POST] /transaction

Ex: /transaction
Body:
{
  addressType: '1',
  contractAddress: '0xdAC17F958D2ee523a2206206994597C13D831ec7',
  from: '', // 私鑰不顯示
  to: '0x1A5A4e7Af1D8BBD9C216c26F733ff98fD79Cc742',
  amount: '1'
}
```

- 參數(JSON)
```bash
{
  addressType: 地址類型. 1:erc, 2:trc
  contractAddress: 合約地址
  from: 轉出*私鑰*
  to: 轉入地址
  amount: 交易量
}
```

- 返回值(JSON)
```bash
{
  result: {
    addressType: 地址類型. 1:erc, 2:trc
    contractAddress: 合約地址
    from: 轉出地址
    to: 轉入地址
    amount: 交易量
    txHash: 交易序號
  },
  status: 'ok'
}

或

{
  error: {
    message: 錯誤訊息
  },
  status: 'error'
}
```
