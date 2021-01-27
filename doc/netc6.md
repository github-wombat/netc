# NET-C 勉強会 6回目

## コンピューター・ネットワークの歴史

- ARPA(Advance Research Project Agency) 1958
  + 米国政府により設立(スプートニク・ショック)
  + 宇宙開発がNASAに移管したので、その他の研究に注力
  + ARPANET 1969
    * 核攻撃された場合に備える分散ネットワーク
    * NCP (Network Control Program)
    * リモートログインや FTP(File Transfer Protocol) や 電子メール

- BBS(電子掲示板) 1974
  + 民間主導
  + パソコン通信へ 1980年代中期

- UUCP (Unix to Unix CoPy) 1976
  + AT&T ベル研 UNIX Version7 より導入
  + 電子メールとネットニュース
  + 米国大学間通信(usenet) 1977
  + 日本大学間通信(Junet) 1984

## ネットワーク・プロトコル

- 1980年代
  + IBM SNA (メインフレーム)
  + DECNET (ミニコン)
  + Xerox XNS
  + Novell Netware
  + NetBIOS
  + AppleTalk
  + TCP/IP

  ISOによる標準化(OSI)の動き

- 1990年頃
  + TCP/IP の勝利
  + OSI の失敗

  OSIは名前と概念のみ残る

## 参照モデル

| 階層 | OSI参照モデル  | | TCP/IP参照モデル |
|---|---|---|---|
|7| アプリケーション層 | 具体的な通信サービス | アプリケーション層 |
|6| プレゼンテーション層 | データの表現方法 | ^ |
|5| セッション層 | 接続の手順 | ^ |
|4| トランスポート層 | データ通信の制御 | トランスポート層 |
|3| ネットワーク層 | ネットワークの通信経路 | インターネット層 |
|2| データリンク層 | 直接接続での通信 | ネットワークインターフェイス層|
|1| 物理層 | 物理的な接続 | ^ |

## IPC(プロセス間通信・InterProcess communication)

- ファイル
- パイプ
- 名前付きパイプ
- シグナル
- メッセージキュー
- 共有メモリー
- ソケット(BSD)
- etc

## BSDソケット

1983年 4.2BSD

|   | SOCK_STREAM | SOCK_DGRAM |
|---|---|---|
| AF_INET / AF_INET6| TCP | UDP |
| AF_UNIX | UNIXドメインソケット | UNIXドメインソケット |

## BSD(Berkeley Software Distribution)

  - AT&Tベル研究所で作られたオリジナル UNIX の初期コードが大学研究者に提供
  - カルフォルニア大学バークレー校(UCB)による派生UNIX(1978年)
  - BSD Unix のさらに亜流UNIX が NextStep → Mac OS X
  - PC への移植版 Unix として 386BSD が作られたが、BSD と AT&T との間で Unix の権利についての訴訟が行なわれ BSD Unix の開発が終了
  - 386BSD も権利関係で問題となるコードの差し替えが必要となり、動く状態に戻すのに手間取る(FreeBSD)
  - その間に、ゼロから作られた Unix クローンである Linux が台頭

## レイヤー1(物理層)

- RS-232C
- 10BASE-T / 100BASE-T / 1000BASE-T
- DSL(ADSL)
- 無線

## レイヤー2(データリンク層)

- Ethenet(IEEE 802.3)
- 無線LAN(IEEE 802.22 a/b/g/n)
- PPP(Point-to-Point Protocol)
  + PPPoE (PPP over Ethernet)

  | 階層 | OSI参照モデル  | native接続 | ダイアルアップ接続 | フレッツ光等 |
  |---|---|---|---|---|
  |2| データリンク層 | Ethernet | PPP | PPPoE<br>Ethernet |
  |1| 物理層 | 100BASE-T等 | RS-232C等 | 光ケーブル等 |

### Ethenet

- フレームの構成
  + プリアンブル : 8バイト
    * 10101010_10101010_10101010_10101010_10101010_10101010_10101010_10101011
  + 宛先MACアドレス : 6バイト
    * ユニキャスト/マルチキャスト
    * グローバルアドレス/ローカルアドレス
  + 送信元MACアドレス : 6バイト
  + タイプ : 2バイト
  + データ本体 : 46〜1500バイト
  + FCS(Frame Check Sequence) エラー検出 : 4バイト

### レイヤー2スイッチ

- リピーターハブ / ダムハブ / バカハブ
- スイッチングハブ

## レイヤー3(データリンク層)

- IP(v4,v6)
- ARP(Address Resolution Protocol)

### IPv4

<table class="wikitable" style="text-align:center" width="100%">
<caption><b>パケット形式図</b>
</caption>
<tbody><tr>
<th>0</th>
<th>1</th>
<th>2</th>
<th>3</th>
<th>4</th>
<th>5</th>
<th>6</th>
<th>7</th>
<th>8</th>
<th>9</th>
<th>10</th>
<th>11</th>
<th>12</th>
<th>13</th>
<th>14</th>
<th>15</th>
<th>16</th>
<th>17</th>
<th>18</th>
<th>19</th>
<th>20</th>
<th>21</th>
<th>22</th>
<th>23</th>
<th>24</th>
<th>25</th>
<th>26</th>
<th>27</th>
<th>28</th>
<th>29</th>
<th>30</th>
<th>31</th>
</tr>
<tr>
<td colspan="4">バージョン
</td>
<td colspan="4">ヘッダ長
</td>
<td colspan="8">サービス種別
</td>
<td colspan="16">全長
</td></tr>
<tr>
<td colspan="16">識別子
</td>
<td colspan="3">フラグ
</td>
<td colspan="13">断片位置
</td></tr>
<tr>
<td colspan="8">生存時間
</td>
<td colspan="8">プロトコル
</td>
<td colspan="16">チェックサム
</td></tr>
<tr>
<td colspan="32">送信元アドレス
</td></tr>
<tr>
<td colspan="32">宛先アドレス
</td></tr>
<tr>
<td colspan="32">拡張情報
</td></tr>
<tr>
<td colspan="32">データ<br><br>
</td></tr></tbody></table>

- **バージョン** IPv4 は4 (0100)
- **ヘッダ長** 4byte単位。通常、拡張情報が無いので 5 (20byte)
- **サービス種別** 重視するサービス (信頼性/転送量/遅延度/優先度)
- **全長** IPヘッダを含むパケットの全長(byte単位)
- **断片情報** パケットが分割された場合の情報
  + **識別子** パケットが分割されても、この値が同一なら元のパケットは1つと判断する。
  + **フラグ** 断片化のフラグ
  + **断片位置** 断片の復元に使う
- **生存時間** ルーターを通る毎に1つ減る。0になるとパケットは消滅
- **プロトコル** 上位(レイヤー4)のプロトコル (TCP/UDP等)
- **チェックサム** IPヘッダーのチェックサム
- **送信元アドレス** 送信元IPアドレス
- **宛先アドレス** 送信先IPアドレス
- **拡張情報** オプション

### IPv6

IPv4 アドレスの枯渇問題を解消する為に導入された

### IPアドレスとサブネットマスク

- **IPアドレス**
  IPネットワーク上の識別番号
  IPv4は32bit、通常、1byte毎の10進数をドットで繋いだ形で表記される
  192.168.1.1

- **サブネットマスク**
  同一ネットワーク(レイヤー2の範囲)か判断する
  IPアドレスと同じ形だが、先頭から1が続き、途中から0が続き終る
  1の部分がネットワークアドレス、0の部分がホストアドレスと判断される
  255.255.255.0 (2進数では 11111111.11111111.11111111.00000000)
  192.168.1.1/255.255.255.0 又は1の数で、 192.168.1.1/24

### ARP(Address Resolution Protocol)

MACアドレス(レイヤー2)とIPアドレス(レイヤー3)の対応表の交換

### Linux のIP関連コマンド

昔からのnet-toolsは非推奨。 現在は iproute2
- IP情報 `ifconfig → ip address(a)`
- route情報 `netstat -r → ip route(r)`
- ARP情報 `arp → ip neigh(n)`
- ソケット情報 `netstat → ss`

### レイヤー3スイッチ

- ルーティング機能とレイヤー2スイッチを統合したもの
- どの機能に重点を置くかで、ルーターと呼ばれたりL3スイッチと呼ばれたり


## レイヤー4(トランスポート層)

### UDP

```plantuml

participant "送信" as S
participant "受信" as R

S ->x R
note right: 受信側が待受けていないと破棄

?-> R
note right: 受信開始
activate R
S -> R
S -> R

...

S -> R

?-> R
note right: 受信終了
deactivate R

S ->x R

```

### TCP

```plantuml
participant "Client1" as C1
participant "Client2" as C2
box Server
participant "Listen" as L

C1 ->x L: connect
note right: 受信側が待受けていないと失敗

...

?-> L
note right: listen
activate L

C1 -> L: connect
activate C1
create participant "Socket1" as S1
L -> S1: accept
activate S1

C1 -> S1: send
S1 -> C1: recv

|||

C2 -> L: connect
activate C2
create participant "Socket2" as S2
L -> S2: accept
activate S2

S2 -> C2: recv
C2 -> S2: send

|||

C2 -> S2: disconnect
deactivate C2
deactivate S2

||| 

S1 -> C1: disconnect
deactivate C1
deactivate S1

|||

?-> L
note right: close
deactivate L

end box
```