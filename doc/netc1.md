# NET-C 勉強会 1回目

## 前準備

* WSLの有効化

    - スタートから検索で「Windowsの機能の有効化または無効化」を探して開く

    - 「Linux用 Windows サブシステム」にチェックを入れる

    - ついでに「仮想マシン プラットフォーム」にもチェックを入れる

    - 指示に従い、必要があれば再起動

## WSLのインストール

* 「Microsoft Store」で「Ubuntu」を検索 → インストール → 起動

* username と password を入れて完了

    極力 root での作業は避けるべきだが、ファイルの編集が面倒だったり初心者が最初につまずく所なので、今回は root で作業する。

    Windows が動かなくなることは無いし、壊れたら、ubuntu を再インストールすれば良いので。

* コマンドプロンプトで、以下を実行

    ```sh
    > ubuntu config --default-user root
    ```

## Visula Studio Code (vscode)のインストール

* トップページからダウンロードせずに、Other platforms のリンクから

    https://code.visualstudio.com/#alt-downloads  
    Windows (System Installer) 64bit をダウンロード  
    \# User Installer は WSL と相性が悪いよう  
    → インストール。

* 日本語化

    Extentions で japanese を検索(Japanese Language Pack for Visual Studio Code)  
    → インストール

## WSL 用の機能拡張を追加

Extentions で wsl を検索(Remote - WSL)
→ インストール

* 左下の >< より Ubuntu を開く

* メニューのターミナル → 新しいターミナルを開く

    ubuntu のコンソールが開く

Ubuntu 上のファイルの編集やコマンドは、vscode で行なう。

## Web server のインストール

* ubuntu のパッケージ・カタログの更新

```sh
# apt update
```

* 軽量 Web server のインストール

```sh
# apt install lighttpd
```

* web server の実行

```sh
# /etc/init.d/lighttpd start
```

* web server の動作確認

    Windowsのブラウザで http://localhost/ を開く

* web server の停止

```sh
# /etc/init.d/lighttpd stop
```
