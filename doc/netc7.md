# NET-C 勉強会 7回目

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
#### パケット

|オフセット|0|1|2|3|
|---|---|---|---|---|
|0| 送信元ポート番号||宛先ポート番号||
|4| データ長||チェックサム||
|8+| データ||||

- 送信元ポート番号
- 宛先ポート番号
- データ長
  ヘッダー含むバイト数(8〜65507)
- チェックサム(IPv4はオプション 0)

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

#### パケット

|オフセット|0|1|2|3|
|---|---|---|---|---|
|0| 送信元ポート番号||宛先ポート番号||
|4| シーケンス番号||||
|8| 確認応答番号||||
|12| ヘッダ長・フラグ||ウィンドウサイズ||
|16| チェックサム||緊急ポインタ||
|20| オプション||||
|24| データ||||

- 送信元ポート番号
- 宛先ポート番号
- シーケンス番号
  送信したデータの順序を示す
  相手から受信した確認応答番号
- 確認応答番号
  相手か受信したシーケンス番号+データサイズ
- ヘッダ長
  TCPヘッダの長さ(4byte単位)
- フラグ
  + URG
    緊急データ
  + ACK
    確認応答番号が有効
  + PSH
    バッファリング無しで上位に渡す
  + RST
    コネクションの強制切断(異常)
  + SYN
    コネクションの確立
  + FIN
    コネクションの終了要求
- ウィンドウサイズ
  受信ウィンドウの大きさ
- チェックサム
- 緊急ポインタ
  URG が 1 の時、緊急データの開始位置を示す

#### 3way ハンドシェイク

```plantuml
participant "Client" as C
participant "Server" as S

group 接続要求
C -> S : SYN=1,ACK=0,シーケンス番号=1000(初回ランダム)
end
group 接続許可
C <- S : SYN=1,ACK=1,シーケンス番号=2000(初回ランダム),確認応答番号=1001
end
group 接続開始
C -> S : SYN=0,ACK=1,シーケンス番号=1001,確認応答番号=2001
end
```

シーケンス番号: 前回、相手から受信した確認応答番号
確認応答番号: 相手か受信したシーケンス番号+1

#### データ送受信

```plantuml
participant "Client" as C
participant "Server" as S

group 100byte
C -> S : SYN=0,ACK=1,シーケンス番号=1001,確認応答番号=2001
end
group 1300byte
C <- S : SYN=0,ACK=1,シーケンス番号=2001,確認応答番号=1101
end
group 300byte
C -> S : SYN=0,ACK=1,シーケンス番号=1101,確認応答番号=3301
end
```

シーケンス番号: 前回、相手から受信した確認応答番号
確認応答番号: 前回、相手から受信したシーケンス番号 + データサイズ

#### 切断

```plantuml
participant "Client" as C
participant "Server" as S

group 切断要求
C <- S : ACK=1,FIN=1,シーケンス番号=3301,確認応答番号=1401
end
group 切断応答
C -> S : ACK=1,FIN=0,シーケンス番号=1401,確認応答番号=3302
end
group 切断要求
C -> S : ACK=1,FIN=1,シーケンス番号=1401,確認応答番号=3302
end
group 切断応答
C <- S : ACK=1,FIN=0,シーケンス番号=3302,確認応答番号=1402
end
```

シーケンス番号: 前回、相手から受信した確認応答番号
確認応答番号: 相手か受信したシーケンス番号+1