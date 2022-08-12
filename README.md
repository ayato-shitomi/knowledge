# knowledge

Linux等の知識をメモする。

<img src="src/knowledge.jpg">

知識は財産です。（年間20万円までの知識には贈与税がかかりません）

## Gitコマンド

初めてのリポジトリを生成する。

```bash
> git init
> git add .
> git remote add origin <KEY>
> git push origin master
```

### ブランチ関連

```bash
> git branch -a    # ブランチのリストを表示
> git swich "ブランチ名"    # ブランチを切り替える
> git merge ブランチ名    # 他のブランチから変更点を取り込む
```

## Tmuxコマンド

### 基本操作

```
Ctrl-b "    上下にペインを分割
Ctrl-b %    左右にペインを分割
Ctrl-b 矢印 ペインを移動
Ctrl-b o    次のペインに移動
Ctrl-b t    時間表示だってｗ
Ctrl-b {    次のペインと現在のペインの位置を入れ替え
```

### Tmuxコピーモード

システムのコピーモードはSHIFTを使えば良い

```
Ctrl-b [  コピーモード開始
SPACE     選択開始
ENTER     コピー
Ctrl-b ]  ペースト
```

### コンフィグファイル

```
# ~/.tmux.conf

# マウスでウィンドウ・ペインの切り替えやリサイズを可能にする
set-option -g mouse on

# マウスホイールでヒストリではなくスクロールできるようにする
set -g mouse on
set -g terminal-overrides 'xterm*:smcup@:rmcup@'
```

## Vim

### vimでの画面分割

```
:vs       分割
ctrl+w w  ほかのペインへ移動
```

### コンフィグファイル

行数表示する。自動補完、自動インデントをする。
これである程度使いやすくなるはず！

```
" View
set number

" Tabsize
set tabstop=4

" Indent
set autoindent

" Autocomplete
inoremap {<Enter> {}<Left><CR><ESC><S-o><TAB>
inoremap [<Enter> []<Left><CR><ESC><S-o><TAB>
inoremap (<Enter> ()<Left><CR><ESC><S-o><TAB>
inoremap <<Enter> <><Left><CR><ESC><S-o><TAB>

" Highlight
set cursorline
set hlsearch
syntax enable

" Command line Autocomplete
set wildmenu
```

## Norminette

Normをインストール後にPathがないと言われた場合、`.bashrc`などに以下を記述する

```.bashrc
export PATH="$HOME/.local/bin:$PATH"
```

## SSH

### 複数マシンで同じキーを使う

> - 普段使用しているPCから秘密鍵をcat等で表示させて、コピーします。<br>
> - コピー先のPCでid_rsaにコピーした秘密鍵を書き込む<br>
> - コピーした先で`chmod 600 ~/.ssh/id_rsa && ssh-keygen -y -f ~/.ssh/id_rsa > ~/.ssh/id_rsa.pub`を実行<br>

詳しくは以下に。
https://qiita.com/LabPixel/items/d3e850144117eda2f1bd

## 42 Guacamole

HomeBrewのインストール
```zsh
> curl -fsSL https://rawgit.com/kube/42homebrew/master/install.sh | zsh
```

Readlineのインストール
```zsh
brew install readline
```

## Shell関連

### ログインShellを変更する

Shellのパスを確認したあとに、`chsh`をして変更すればよい。

```zsh
ayato@ayato-VBox:~/$ echo $SHELL
/bin/bash

ayato@ayato-VBox:~/$ which fish
/usr/bin/fish

ayato@ayato-VBox:~/$ chsh
Password: 
Changing the login shell for ayato
Enter the new value, or press ENTER for the default
	Login Shell [/bin/bash]: /usr/bin/fish
```

## Linuxの権限

## Firebase等の環境

### npmのインストール

npmはインストールしただけでは古い場合がある。

```bash
> sudo apt install npm
> sudo npm install -g npm
```

### yarnのインストール

yarnは`apt`でインストールしたらだめっす。

```bash
> sudo npm install --global yarn
```
### nのインストール

`n`はNodeのバージョン管理ツール

```bash
> sudo npm install -g n
```

### firebase

firebaseのインストールではNodeのバージョンが`14`必要な時がある。

### パッケージがない時

ファンクションを走らせると、パッケージがないと言われるときがある。

```
> npm install
```

このコマンドで必要パッケージがインストールされる。

## TypeScript

### 型を定義してないプロパティを読み込んでは行けない (2339)

以下のようなコードはエラーになる。

```ts
this.unko.getUnko().doUnko((unkoStruct) => {
  const unkoSize = unko.size;
  const unkoName = unko.name;
});
```

正しくは、以下のように型を指定してやればいい。

```ts
this.unko.getUnko().doUnko((unkoStruct : any) => {
  const unkoSize = unko.size;
  const unkoName = unko.name;
});
```
