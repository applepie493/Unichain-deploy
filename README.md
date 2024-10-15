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
```
unichain(フォルダ）
├── 
```
中身が空だと思うので
```
nano ファイル名.sol
```
で作成し、中身は
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

contract ファイル名 is ERC20 {
    // トークンの初期供給量
    uint256 constant _initialSupply = 1000000 * 10**18;

    // コンストラクタ: トークンの名前とシンボルを指定
    constructor() ERC20("ファイル名", "MTK") {
        // コントラクトのデプロイ時に、デプロイアドレスに初期供給量を割り当て
        _mint(msg.sender, _initialSupply);
    }
}
```
## ４.デプロイ
```
forge create ファイル名.sol:ファイル名 --rpc-url Alchemy等からUnichainから取得 --private-key ぷらいべーときー
```
Transaction hash: 0x4e5aaec1a712324d30b11c142afa49aae6d7032a0ba0be3569d53f7259f75c33
などが表示されたらOK

## ５.デプロイのときにエラーが出た場合
import "@openzeppelin　←がインストールされてないよ
```
forge install OpenZeppelin/openzeppelin-contracts
```
git status exited with code 128:
fatal: not a git repository (or any of the parent directories): .git ← gitを初期化
```
git init
```
Error: 
The target directory is a part of or on its own an already initialized git repository,
and it requires clean working and staging areas, including no untracked files.

Check the current git repository's status with `git status`.
Then, you can track files with `git add ...` and then commit them with `git commit`,
ignore them in the `.gitignore` file, or run this command again with the `--no-commit` flag.

If none of the previous steps worked, please open an issue at:
https://github.com/foundry-rs/foundry/issues/new/choose
```
git status
echo ".DS_Store" >> .gitignore
git add .
```
で解決しました。
エラーを修正後
```
forge install OpenZeppelin/openzeppelin-contracts
```
でいけるはず・・・


# 5.参考文献
<https://docs.unichain.org/docs/building-on-unichain/deploy-a-smart-contract>
