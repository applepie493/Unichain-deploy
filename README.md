# Unichain-deploy

個人的な備忘録です。

Unichainのテストネットがあり、deployしてみました。

# 1.プロジェクトディレクトリの作成
```
mkdir unichain（任意）&& cd unichain
```

# 2.Foundrynの設定
```
curl -L https://foundry.paradigm.xyz | bash
```
初めてなら多分依存関係でエラーがでる
```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> /Users/izumishunsuke/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"
```
で次に
```
brew install libusb
source /Users/任意/.zshenv
```
sourceで更新するかターミナル再起動して下記を実行
```
curl -L https://foundry.paradigm.xyz | bash
source /Users/任意/.zshenv
```
sourceで更新するかターミナル再起動

```
forge --version
```
でforge 0.2.0とか表示されたらOK


# 3.フォルダの中身
 unichain
    ├── 

## 1.プロジェクトディレクトリの作成する
```
mkdir hardhat-move-evm
```

## 2.プロジェクトディレクトリへ移動
```
cd hardhat-move-evm
```

## 3.hardhatのプロジェクトを作成
 ```
 npx hardhat init
```
 
 今回は、JSを選択しました。

## 4.依存関係の確認

```
npm install --save-dev "hardhat@^2.19.0" "@nomicfoundation/hardhat-toolbox@^3.0.0"
```


## 5.dotenvのインストール
```
npm install dotenv
```


## 6..envファイルの作成
```
touch .env
```
中身は`PRIVATE_KEY=<your private key>` <br>
エディタはnanoを使用。


## 7.hardhat.config.jsの書き換え
```
require("@nomicfoundation/hardhat-toolbox");
require('dotenv').config();

module.exports = {
  defaultNetwork: "m1",
  networks: {
    hardhat: {
    },
    m1: {
      url: "https://mevm.devnet.m1.movementlabs.xyz/v1",
      accounts: [process.env.PRIVATE_KEY],
      chainId: 336,
      gasPrice: "auto",
    }
  },
  solidity: {
    version: "0.8.19",
    settings: {
      optimizer: {
        enabled: true,
        runs: 200
      }
    }
  },
  paths: {
    sources: "./contracts",
    tests: "./test",
    cache: "./cache",
    artifacts: "./artifacts"
  }
}
```


## 8.実行
```
npx hardhat run scripts/deploy.js --network m1
```


# 4.実行結果
`Lock with 0.001ETH and unlock timestamp 1702990817 deployed to ********************************`


# 5.参考文献
<https://docs.movementlabs.xyz/developers/developer-tools/fractal/fractal-hardhat>
