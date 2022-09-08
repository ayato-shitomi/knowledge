# knowledge

Linux等の知識をメモする。

知識は財産です。（年間20万円までの知識には贈与税がかかりません）

## Django

### インストール

```bash
> python3 -m pip install django

# 上のコマンドでできなかった場合にはこれを実行せよ
> sudo apt install python3-django
```

### 新規プロジェクトの作成と確認

```bash
> django-admin startproject <プロジェクト名>
> cd <プロジェクト名>

> python3 manage.py runserver
```

`http://127.0.0.1:8000/`とかにアクセスしてやれば、確認できる。
URLがCLIに表示されます。
`Ctrl-C`とかで止めてねって感じ。
止めなくても自動反映されるからとても嬉しい！

### 新規アプリケーションの作成

```bash
> python3 manage.py startapp <アプリ名>
```

最初にViewを作成する。

`<アプリ名>/views.py`
```python
from django.http import HttpResponse
from django.shortcuts import render

# Create your views here.

def index(reqest):
	return HttpResponse("Hello world. You'r at the polls index.")
```

次にViewをURLに紐付ける。

`<アプリ名>/urls.py`
```python
from django.urls import path
from . import views

urlpatterns = [
	path('', views.index, name='index'),
]
```

URLに対して、モジュールを反映させる。

`<プロジェクト名>/urls.py`
```
from django.contrib import admin
from django.urls import include, path

urlpatterns = [
    path('admin/', admin.site.urls),
    path('<アプリ名>/', include('<アプリ名>.urls')),
]
```

→ To Be Continued


## Docker

### Dockerプロセスの確認をする

```bash
> sudo docker ps
```

### Dockerプロセスに接続する

```
> sudo docker exec -it <NAME> /bin/bash
```

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

### vimでのコピペ

単数行のコピペ
```
yy	コピー
p	貼り付けられます。
```

複数行のコピペ
```
Shift v	ビジュアルモードで行選択
y	コピー
p	貼り付けられます。
```

### コンフィグファイル

行数表示する。自動補完、自動インデントをする。
これである程度使いやすくなるはず！

`.vimrc`

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
highlight CursorLine ctermbg=8
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

セットアップホストは`10.11.13.2`です～

HomeBrewのインストール
```zsh
> curl -fsSL https://rawgit.com/kube/42homebrew/master/install.sh | zsh
```

Readlineのインストール
```zsh
> brew install readline
```

Fishのインストール
```zsh
> brew install fish
```

tmuxのインストール
```zsh
> brew install tmux
```

## Shell関連

### Bashコンソールを変更する

コンソールのフォーマットは`PS1`に入ってる。
それを変更してやればよい。

```bash
> PS1="\e[0;32m\u\e[m@\e[0;33m\h\e[m ~/\W \n$ "
```

紐解くとこのようになる。

> `\e[0;32m` + `\u` + `\e[m` + `@` + `\e[0;33m` + `\h` + `\e[m` + ` ~/` + `\W` + `\n` + `$ `

つまり、このようなSHELLを作ることができます。

```
USER@HOST ~/DIR
$ CMD
```
これもなおすすめ。
```bash
> PS1="\e[0;32m\u\e[m@\e[0;33m\h\e[m \s\v \e[0;34m[\d \t]\e[0m ~/\W \n`echo [$?]` > "
```

### Zshコンソールを変更する

42Guacamoleでは改行が許されないっぽいので、ちょっと短くした次第であります。

```
PS1="%F{green}%n%F{white}@%F{yellow}%m%F{white} %~ [%?] > "
```

### 出力の文字色を変更する

```python
print("Normal \x1b[31m RED \x1b[0m \tNormal")
print("Normal \x1b[32m GREEN \x1b[0m \tNormal")
```


|コード|役割|
|----|----|
|`\x1b[31m`|文字色を赤に変更|
|`\x1b[32m`|文字色を緑に変更|
|`\x1b[0m`|文字色等の変更を元に戻す|

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

### 環境変数にコマンドの実行結果を保存する

環境変数`$DATE`に`date`の結果を保存したい場合には以下のようにする。

```bash
> DATE=`date`
```

しかしながら、Fishの場合は`set`コマンドを使用して以下のようにする

```fish
> DATE (date)

### プロファイルや`.bashrc`などを即時反映させる

Bashの場合

```bash
> source ~/.bashrc
```

Zshの場合

```zsh
> source ~/.zshrc
```

## Shell芸人を目指して

ファイルの中の文字列を検索、ファイル名と行数も出力する。
```bash
> grep -n "検索したい文字列" 検索したいファイル
```

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

```zsh
> sudo npm install -g firebase
```

firebaseのインストールではNodeのバージョンが`14`必要な時がある。

### パッケージがない時

ファンクションを走らせると、パッケージがないと言われるときがある。

```
> npm install
```

このコマンドで必要パッケージがインストールされる。

## TypeScript

### 型を定義してないプロパティを読み込んではいけない (2339)

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

## Replit

### サーバーを再起動したい

```bash
> kill 1
```

## ショートカットキー

### Chrome、Brave等で閉じたタブを復元する

`Ctrl + Shift + t`

## Python

### ファイル入出力

```python
# 第一引数に読みたいファイルパスを取る
# 戻り地は内容が帰れば成功、"False"が失敗
def getFile(filePath):
    try:
        f = open(filePath, 'r', encoding="UTF-8")
        data = f.read()
        f.close()
        return data
    except:
        return False

# 第一引数に読みたいファイル
# 戻り地は"True"が成功、"False"が失敗
def setFile(filePath, index):
    try:
        f = open(filePath, 'w', encoding="UTF-8")
        f.write(index)
        f.close()
        return True
    except:
        return False
```

### Discord Bot

`Discord.py`のインストールが必要となる。

```bash
> python3 -m pip install -U discord.py
```

特定ユーザーにDMを送る

```python
userId = xxx

client.users.get(userId).send("MSG")
```

## Cron

クーロン、クロンタブ

```bash
# 編集
> sudo crontab -e

# 再起動
> /etc/init.d/cron restart

# システムログを確認
cat /var/log/syslog
```

10分おきに実行したい場合には以下のようにする。

```cron
*/10 * * * * CMD
```

```cron
* * * * * CMD > /var/log/git_push.log 2>&1
```

## imwheel

マウスのスクロール速度がやばいときに使うといい。
`/usr/bin/imwheel`をスタートアップに指定するとimwheelなしの生活に戻れない。

### インストール

```
> sudo apt install imwheel
```

### 設定

`~/.imwheelrc`

```
".*"
None, Up, Button4, 3
None, Down, Button5, 3
```

### 起動と管理

```bash
# 起動
> imwheel

# 設定を反映させる
> imwheel -k
```
