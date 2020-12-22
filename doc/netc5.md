# NET-C 勉強会 5回目

## ML(Markup Language)

* ML とは
* ML の歴史
    - roff
    - TeX
    - SGML
    - HTML
    - XML

## HTML(HyperText Markup Language)
* 基本構造
```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>HTML</title>
    </head>
    <body>
        <h1>見出し</h1>
        <p>段落</p>
    </body>
</html>
```
* DTD(Document Type Definition 文書型定義)
```
<!DOCTYPE html>
```
* htmlタグ
```
<html> ... </html>
```
* headタグ
    - 情報定義
    - CSSやJavascriptの読込
    - タイトル

* bodyタグ

## HTTP(HyperText Transfer Protocol)
* ステートレスなプロトコル
* リクエスト
```
GET /index.html HTTP/1.0
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:84.0) Gecko/20100101 Firefox/84.0
```

* レスポンス
```
HTTP/1.0 200 OK
Content-Type: text/html
Content-Length: 3388
Connection: close
Date: Mon, 21 Dec 2020 02:26:28 GMT
Server: lighttpd/1.4.57

<!DOCTYPE html>
<html>
...
```

* GET と POST

    - GET request
    ```
    GET /cgi-bin/python_cgi?name=net-c&furigana=%E3%81%AD%E3%81%A3%E3%81%A8%E3%81%97%E3%83%BC HTTP/1.1
    ```

    - POST request
    ```
    POST /cgi-bin/python_cgi HTTP/1.1

    name=net-c&furigana=%E3%81%AD%E3%81%A3%E3%81%A8%E3%81%97%E3%83%BC
    ```

## Chrome と Firefox の debug 機能

F12 か Ctrl+Shift+C
