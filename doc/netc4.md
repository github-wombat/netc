# NET-C 勉強会 4回目

## ファイルシステム

* 絶対パスと相対パス

* 管理領域

    - スーパーブロック
    - 空きエリア管理領域
    - i-node 管理領域
    - ディレクトリーデータ 管理領域
    - ユーザーデータ管理領域

    https://www.ibm.com/developerworks/jp/linux/library/l-linux-filesystem/
    https://monoist.atmarkit.co.jp/mn/articles/1003/02/news112.html

* i-node

    ```sh
    # stat <file/directory>
    ```

* ディレクトリーデータ 管理領域

    ```sh
    # ls -ai
    ```

* ハードリンク
* シンボリックリンク

## 環境変数

* シェル変数と環境変数

    ```sh
    # <変数>=<値>
    # echo $<変数>  / ${<変数>}
    # export <変数>
    ```

* アプリと環境変数

    ```sh
    # date
    # TZ=America/New_York date
    # TZ=Europe/Paris date
    /usr/share/zoneinfo
    # tr \\0 \\n < /proc/<pid>/environ
    ```

## Pythonパッケージ

```sh
# apt intsall python3-pip
# pip install google_trans_new
# TGT=en ./python_trans < trans.txt 
```

    en 英語
    zh 中国語
    ko 韓国
    fr フランス
    de ドイツ
    it イタリア
    ru ロシア
        c.f. /usr/share/locale