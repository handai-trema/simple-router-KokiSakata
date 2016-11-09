# 情報ネットワーク学演習Ⅱ 10/12 レポート課題

## 課題内容 (ルータの CLI を作ろう)

ルータのコマンドラインインタフェース (CLI) を作ろう。

次の操作ができるコマンドを作ろう。

* ルーティングテーブルの表示
* ルーティングテーブルエントリの追加と削除
* ルータのインタフェース一覧の表示
* そのほか、あると便利な機能

コントローラを操作するコマンドの作りかたは、第3回パッチパネルで作った patch_panel コマンドを参考にしてください。

##解答
今回、ルータのコマンドラインインターフェース作成するために、binファイル内にsimple_routerというコマンド実行ファイルを作成した。
以降、作成した機能毎に簡単に説明していく。

### ルーティングテーブルの表示
以下のようなコマンドを作成した。
```
./bin/simple_router ShowTable
```
このコマンドの実行結果を以下に示す。
```
root@ensyuu2-VirtualBox:~/simple-router-KokiSakata# ./bin/simple_router ShowTable
routing table
Destination/netmask | Next hop
0.0.0.0/0	    | 192.168.1.2
192.168.1.0/24	    | 192.168.1.1
```
以上より、デフォルトのルーティングテーブルが正しく表示されていることがわかる。

### ルーティングテーブルエントリの追加と削除
#### ルーティングテーブルエントリの追加
以下のようなコマンドを作成した。
```
./bin/simple_router AddTable <宛先アドレス>　<サブネットマスク長> <次の転送先>
```
このコマンドを用いて宛先アドレスを192.168.1.0、サブネットマスク長を24、次の転送先を192.168.1.1としてルーティングテーブルエントリの追加を行ったあとに、その時点でのルーティングテーブルを表示したのが以下である。
```
root@ensyuu2-VirtualBox:~/simple-router-KokiSakata# ./bin/simple_router AddTable 192.168.1.0 24 192.168.1.1
root@ensyuu2-VirtualBox:~/simple-router-KokiSakata# ./bin/simple_router ShowTable
routing table
Destination/netmask | Next hop
0.0.0.0/0	    | 192.168.1.2
192.168.1.0/24	    | 192.168.1.1
root@ensyuu2-VirtualBox:~/simple-router-KokiSakata# 
```
以上より、新しいエントリの情報がルーティングテーブルに正しく追加されていることがわかる。

#### ルーティングテーブルエントリの削除
以下のようなコマンドを作成した。
```
./bin/simple_router DeleteTable <宛先アドレス>　<サブネットマスク長>
```
上述の追加コマンドに続いて、このコマンドを用いて宛先アドレスを192.168.1.0、サブネットマスク長を24としてルーティングテーブルエントリの削除を行ったあとに、その時点でのルーティングテーブルを表示したのが以下である。
```
root@ensyuu2-VirtualBox:~/simple-router-KokiSakata# ./bin/simple_router DeleteTable 192.168.1.0 24
root@ensyuu2-VirtualBox:~/simple-router-KokiSakata# ./bin/simple_router ShowTable
routing table
Destination/netmask | Next hop
0.0.0.0/0	    | 192.168.1.2
root@ensyuu2-VirtualBox:~/simple-router-KokiSakata# 
```
以上より、指定したエントリの情報がルーティングテーブルから正しく削除されていることがわかる。

### ルータのインタフェース一覧の表示
以下のようなコマンドを作成した。
```
./bin/simple_router ShowInterface
```
上述の追加と削除のあとに、このコマンドを用いてルータのインタフェース一覧を表示したのが以下である。
```
root@ensyuu2-VirtualBox:~/simple-router-KokiSakata# ./bin/simple_router ShowInterface
interface list
port | mac address  	 | ip address/netmask
1    | 01:01:01:01:01:01 | 192.168.1.1/24
2    | 02:02:02:02:02:02 | 192.168.2.1/24
```
以上より、ルータのインターフェースの一覧が正しく表示されていることがわかる。


## 謝辞
プログラムのコードを考える上で、田中達也くんのプログラムとレポートを参考にしました。ありがとうございました。
