# knowledge
Linux等の知識をメモする。

知識は財産です。

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

" Command line Autocomplete
set wildmenu
```

### Norminette

Normをインストール後にPathがないと言われた場合、`.bashrc`などに以下を記述する

```.bashrc
export PATH="$HOME/.local/bin:$PATH"
```

### 複数マシンでSSHキーを使いまわす

> - 普段使用しているPCから秘密鍵をcat等で表示させて、コピーします。<br>
> - コピー先のPCでid_rsaにコピーした秘密鍵を書き込む<br>
> - コピーした先で`chmod 600 ~/.ssh/id_rsa && ssh-keygen -y -f ~/.ssh/id_rsa > ~/.ssh/id_rsa.pub`を実行<br>

詳しくは以下に。
https://qiita.com/LabPixel/items/d3e850144117eda2f1bd
