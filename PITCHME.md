# Linux/shellコマンドのメモ

+++

## 用語  

CLI: Command Line Interface  
Timestamp：**作成時刻・更新時刻・アクセス時刻**など、電子データに対して付与される何かの時刻を表す情報のこと。   
タイムスタンプの信頼性は、タイムスタンプを発行する時刻認証局(TSA:Time-Stamping Authority)が信頼できる第3者(TTP:Trusted Third Party)であることに基づいている。  
環境変数：外部コマンドから値を参照できるように、外部コマンドが格納されているファイルパスを設定した変数のこと  

+++

## ログインしているシェルの確認

以下は、シェルを確認した結果、zshellにログインしていることを確認している例  
```zsh
echo ＄SHELL
/bin/zsh
```
+++

## Linuxのディレクトリ

フォルダ構造をとっている  
FHS(Filesystem Hierarchy Standard)という標準仕様に従っている  
Windowsと比べると、Linuxでは何台ドライブがあろうが、Directory構造は一つのみ  

+++

## Linuxのディレクトリの役割

以下の種類がある  

/bin  
/dev  
/etc  
/home  
/sbin  
/tmp  
/usr  
/var  

---

# /bin  
実行ファイルを置くためのディレクトリ  
外部コマンドである（build-inではない）  
linuxコマンドの実行ファイルがある  
重要度の高いコマンドファイルが格納されている  

---

# /dev  
ディバイスファイルを格納するディレクトリ  
ハードウェアをファイルとして取り扱えるようにした特殊なファイル  。

---

# /etc  
設定ファイルを置くためのディレクトリ  
設定ファイルは、「.bash」、「.bash_profile」、「.bashrc」とかがある  
通常はテキスト形式の設定ファイル(コンフィグファイル)が使用される  
Linux自体の設定に関わるファイルもここに格納される  

---

# /home  
ユーザごとに割り当てられる、ホームディレクトリが配置されるディレクトリ  

---

# /sbin  
binと似ている  
実行ファイルを置くためのディレクトリ  
システムをシャットダウンするための実行ファイルはここにある  

---

# /tmp  
一時的なファイル（テンポラリファイル）を置くためのディレクトリ  
アプリケーション実行中に作業途中結果などを一時的に格納するときにはここに格納するのが一般的  
定期的に削除されることがあるので、ここに永続的に保存が必要何ファイルを置いてはいけない  

---

# /usr  
各種アプリケーションとそれに付随するファイルを置くためのディレクトリ  
内部にはbin,sbin,etcなどを持ち、内部にディレクトリ配下と似たような構造を持つ

---

# /var  
変化するデータを置くためのディレクトリ  
アプリケーションを動作させるために必要なデータ、ログ、電子メールなどがここに格納される  
要領を圧迫することが多いので、システム管理上では注意が必要なディレクトリ  

+++

## カーソルの移動  

---

カーソルを1文字進める  
```
ctr + f  
```

カーソルを行末にする  
```
ctr + e  
```

---

カーソルを1文字後退する  
```
ctr + b  
```

カーソルを行頭にする  
```
ctr + a  
```

+++

### 単語ごとに移動

単語の先頭に移動  
```
Meta + b  
```

単語の末尾に移動  
```
Meta + f  
```

なお、MacではMeta keyが設定されていないので、Terminalを選択した上で、Preference。  
Profile→key を選択して、「Use Oprion as Meta key」チェックボックスにチェックをいれる  

+++

### 削除

---  

カーソル前（右）の一字削除  
```
ctr + d  
→del key  
```

カーソル後（左）の一字削除  
```
ctr + h  
→backspace key  
```

---  

カーソルの前を一単語を削除  
```
ctr + w  
```

---  

<カット1>  
カーソル位置から行末まで（右方向に）削除する  
```
ctr + k  
→拡張のdel key  
```

<カット2>  
カーソル位置から行頭まで（左方向に）削除する  
```
ctr + u  
→拡張のbackspace key  
```

---  

<ヤック>  
最後に削除した内容を挿入  
```
ctr + y  
```

+++

## 直前のコマンドを入力する

```
ctr + p  
```

## インクリメンタル検索のプロンプト

入力したコマンドを検索するコマンド  

```
ctr + r  
```
+++

## ワイルドカードと任意文字

ワイルドカードはアスタリスクで指定  
```zsh
$ ls *.htmml
index.html test.htmml ...
```

任意の一文字のみを指定したいときはクエスチョンマークを使用する  
```zsh
$ ls ba??
bash
```
+++

## lsコマンドのオプション  

+++

### 様々なオプション
lsをはじめとする各コマンドには多くのオプションがある  

+++

#### lsとオプションについて

カレントディレクトリに存在している、ファイル・フォルダを表示させる  

```
ls
```

---

ファイルの状態詳細を確認（保存日時含む）  

```zsh
ls -la
```

---

ファイルの詳細を表示  
```zsh
$ ls -l
total 24
drwx------@  3 root  staff    96 Aug  1 13:21 Applications
# d: ファイルタイプ(dはディレクトリ/-は通常ファイル/lはシンボリックリンク)
# rwx------@：ファイルモード
# 3：リンク数
# root：所有者
# staff：所有グループ
# 96：サイズ
# Aug  1 13:21：タイムスタンプ
# Applications：ファイル名又はディレクトリ名
```

+++

以下のオプションあり  
2.1 その１　-aオプション：すべて表示  
2.2 その２　-lオプション：ファイルの詳細も表示する  
2.3 その３　-1オプション：リストを縦に並べる  
2.4 その４　-rオプション：逆順で表示する  
2.5 その５　-tオプション：更新時間順に並べる  
2.6 その６　-Sオプション：ファイルサイズ順でソートする  
2.7 その７　-Xオプション：ファイルを拡張子ごとにまとめる  
2.8 その８　-Rオプション：ディレクトリ内容を再帰的に表示する  
2.9 その９　--full-timeオプション：タイムスタンプの詳細を表示する  
2.10 その１０　-mオプション：ファイル名をカンマで区切って表示する  
2.11 その１１　-hオプション：単位を読みやすい形式で表示する  
2.12 その１２　-kオプション：キロバイト単位で表示する  
2.13 その１３　-iオプション：ファイル名の左にi-node番号を表示する  
2.14 その１４　-Fオプション：情報の付加  
2.15 その１５　--helpオプション：ヘルプの表示  

---

隠しファイルも含めた全てのファイルを表示  
```zsh
$ ls -a
```
ファイル種別を表示する  
```zsh
$ ls -F
```
+++

### オプションの指定方法
オプションは複数でも指定できる  
```zsh
$ ls -a -F
# 又は
$ ls -aF
```

+++

### 引数をとるオプション  

指定した数値の横幅で表示するオプション  
**(macでは使用できない？)**  

```zsh
$ ls -w 30
bin     lib      proc      sys # 30桁目で次の行へ
boot    lib64    root      tmp # 30桁目で次の行へ
dev     media    run       usr # 30桁目で次の行へ
```
+++

### ロングオプション

「ハイフン＋英数字1文字」で指定される  
```zsh
$ ls --quote-name
"bin" "etc"
# ファイル名をダブルクオートで括った形で表示する  
```
+++

# ファイル操作

## mkdirコマンド  

ファイル名と同じ名前のディレクトリは作成できない  

深いディレクトリを一気に作成する  
-pのオプションを指定することで作成可能  
```zsh
mkdir -p report/2020/09
```

---

## echoコマンド

ファイルを作成  
```zsh
echo <text> > <filename>
```

ファイルに追記  
```zsh
echo <text> >> <filename>
```
---

## typeコマンド  

**組み込みコマンド**と**外部コマンド**のどちらであるかを確認することができる  
```zsh
$ type set
set is a shell builtin # 組み込みであることを示す
$ type cp
cp is /bin/cp # This is the external command. so that was shown the file directory that is stored.
```

ファイルの中身を確認（catと同じ？）  

```zsh
$ type <filename>
```

---

## touchコマンド  
touchコマンドはタイムスタンプを変更するコマンド  
mtime（ファイルの内容を書き換えた日時）とctime(ファイルのアクセス権などを変更した日時)を書き換える

```zsh
touch <filename>
```

ちなみに、ファイルの新規作成の役割も果たす  


```zsh
usr@home % ls # ファイルの状態を表示
a.txt

touch b.txt # ファイルの新規作成

usr@home % ls # ファイルの状態を表示
a.txt
b.txt
```
---

タイムスタンプ変更の挙動確認  

ex)  

```zsh
usr@home % ls -la a.txt # ファイルの状態を表示
-rw-r--r--@ 1 user  staff  53 Sep  5 21:01 a.txt

usr@home % touch a.txt # タイムスタンプを変更

usr@home % ls -la a.txt # ファイルの状態を表示（タイムスタンプを変更した日時でタイムスタンプを記録）
-rw-r--r--@ 1 user  staff  53 Sep  5 21:03 a.txt
```

+++

## rm/rmdir ファイル・ディレクトリを削除する  

---

### rmコマンド
ファイルを削除する  

```zsh
$ rm test.txt
# テキストファイルが削除される
```
ファイルをまとめて削除する
```zsh
$ rm test1.txt test2.txt test3.txt # ファイルがまとめて削除される

$ rm *.txt # ファイルがまとめて削除される
```
ディレクトリと中に格納されているファイル両方を削除する  
-rオプションを使う  

```zsh
$ rm -r mydir1
# テキストファイルが削除される
```
---

### 空フォルダを削除する  

```zsh
$ rmdir myfolder1 
# フォルダの中にファイルが存在していたらフォルダは削除されない
```

+++

## catコマンド  
ファイルの内容を確認できる  
```zsh
$ cat hello world_3times.txt
hello world
hello world
hello world
# ファイルの内容がそのまま表示される
# ファイル名を続けて指定すると連結表示も可能
```
---

## catコマンド  
ファイル名を続けて指定すると連結表示も可能  
```zsh
$ cat hello world_3times.txt test.txt
# test.txtの内容
first line
second line
third line

# hello world_3times.txtの内容
hello world
hello world
hello world
# ファイル名を続けて指定すると連結表示も可能
```

---

行番号を表示する
```zsh
$ cat -n test.txt
     1	first line
     2	second line
     3	third line
```
---


何もファイル名を入力せずに実行する  
```zsh
$ cat 
# ←カーソル位置
# カーソルが次の行に下がった状態になり、文字を入力可能  
```

```zsh
$ cat 
hello # 文字を入力
hello # 入力した文字が返る
```

```zsh
$ cat 
hello # 文字を入力
hello # 入力した文字が返る

# ctr + d でcatモードが終了

$ # ←プロンプトに戻る
```

---

---memo---  

mv	[ファイル名]を[ディレクトリ]へ移動する	mv style.css assets/css  
cp	[ファイル1]を[ファイル2]という名前でコピーする	cp index.html about.html  

+++

## 環境変数
### 環境変数の確認
```zsh
$ printenv
SHELL=/bin/zsh
HOME=/Users/root
LOGNAME=root
USER=root
PATH=¥xxxx¥xxx¥xxx¥xx¥
...
```

+++

## export環境変数設定
「export」は、環境変数やシェル変数を設定するコマンド  

シェル変数を環境変数に変える  

```zsh
$ export <shell variables name>
```

---

環境変数をシェル変数に更新するときは「-n」オプションを使う

```zsh
$ export -n <shell variables name>
```

シェル変数を定義して、同時にエクスポートする  

```zsh
$ export <shell variables name> = variable 
# shell variables name:Arbitray name that you want to
# variable: folder directory?
```

+++

## コンピュータのシャットダウン・再起動  

シャットダウン  
```zsh
shutdown -h now
```

再起動   
```zsh
shutdown -r now
```

