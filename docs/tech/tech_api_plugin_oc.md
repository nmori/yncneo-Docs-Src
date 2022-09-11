#わんコメ互換APIについて
!!! Info "内容について"
    この内容はサービス改良の中で予告なく改定されることがあります

!!! Tech "通信先"
    * ゆかりねっとコネクターNEOのWebポートに送付してください。デフォルトは ``15520`` です。

## 発話の受信(HTTP)

* 発話結果をJSONとして受け取れます。

!!! Tech "使用条件"
    * 特になし
* 送付方式：GET
* 送付先 :　http://127.0.0.1:15520/comment.json
* ポート番号は後述のレジストリから取得してください

=== "Query"
    ``` js
        {
            "comments": [
                {
                    "data": {
                        "id": "ed9ab6fd-151f-462b-bc4e-c894561c3f97",
                        "userId": "8141cf31-1685-4e88-97ce-9ae92981174b",
                        "name": "nao",
                        "profileImage": "/image/nao.png",
                        "badges": [],
                        "hasGift": false,
                        "comment": "<span class=\"origin\">テストです</span>⁣⁣<span class=\"t\"><span class=\"par\">(</span>It's a test<span class=\"par\">)</span></span>⁣⁣",
                        "timestamp": 1660709231.1491292,
                        "displayName": "nao",
                        "isFirstTime": false
                    },
                    "id": "00000000-0000-0000-0000-000000000000",
                    "service": "YNC_Plugin_DirectInput",
                    "name": "#",
                    "url": ""
                }
            ],
            "listeners": {
                "id": "00000000-0000-0000-0000-000000000000",
                "name": "#",
                "url": "#",
                "write": true,
                "speech": false,
                "enabled": true,
                "color": {
                    "r": 32,
                    "g": 32,
                    "b": 32
                },
                "translate": "",
                "type": "YNC",
                "listeners": [
                    {
                        "id": "8141cf31-1685-4e88-97ce-9ae92981174b",
                        "name": "nao",
                        "profileImage": "/image/nao.png",
                        "badges": {},
                        "firstCommentTime": 0,
                        "lastCommentTime": 0,
                        "count": 0,
                        "giftCount": 0
                    }
                ]
            }
        }
    ```

* 成功すると 上記JSONを得られます。
* 統計データなどはダミー値です。
* メッセージは ``comment`` に入ります。翻訳がある場合は ``class t`` に入ります。
* 新たなメッセージか、更新されたかは、 ``id`` で判断してください。

## 発話の受信(WebSocket)

* 発話結果をJSONとして受け取れます。

!!! Tech "使用条件"
    * わんコメ仕様テンプレプラグインがONになっていること

!!! Tech "通信先"
    * わんコメ仕様プラグインのWebsocketポートに接続してください。デフォルトは ``54000`` です。

* 送付方式：GET
* 送付先 :　ws://127.0.0.1:54000/ 
* ポート番号は後述のレジストリから取得してください

=== "Response(v3)"
    ``` js
        {
            "type": "comments",
            "data": [
                {
                    "data": {
                        "id": "a43e07a3-5b8c-4274-8d16-624edf383824",
                        "userId": "8141cf31-1685-4e88-97ce-9ae92981174b",
                        "name": "nao",
                        "profileImage": "http://127.0.0.1:15520/image/nao.png",
                        "badges": [],
                        "hasGift": false,
                        "comment": "<span class=\"origin\">123</span>⁣⁣<span class=\"t\"><span class=\"par\">(</span>123 \n<span class=\"par\">)</span></span>⁣⁣",
                        "timestamp": 1660715431.4722717,
                        "displayName": "nao",
                        "isFirstTime": false
                    },
                    "id": "a43e07a3-5b8c-4274-8d16-624edf383824",
                    "service": "YNC_Plugin_DirectInput",
                    "name": "#",
                    "url": ""
                }
            ]
        }
    ```
=== "Response(v4)"
    ``` js
        {
        "type": "comments",
        "data": {
            "comments": [{
            "id": "56e5b273-b216-4dfb-808d-3e4c448f115f",
            "service": "YNC_Plugin_DirectInput",
            "name": "#",
            "url": "about.blank",
            "data": {
                "id": "56e5b273-b216-4dfb-808d-3e4c448f115f",
                "liveId": "e68e52bd-9c36-4aee-a2f4-e76c94ab0944",
                "userId": "e68e52bd-9c36-4aee-a2f4-e76c94ab0944",
                "name": "なお",
                "isOwner": false,
                "isModerator": false,
                "isMember": false,
                "timestamp": 1662841943.4777987,
                "badges": [],
                "hasGift": false,
                "profileImage": "http://127.0.0.1:15521/image/なお.png",
                "originalProfileImage": "http://127.0.0.1:15521/image/なお.png",
                "comment": "123",
                "displayName": "なお",
                "isFirstTime": false
            },
            "meta": {
                "interval": 0
            }
            }],
            "options": {}
        }
        }
    ```

* 音声認識がおこなわれるたびに上記JSONがテキストメッセージとして送信されます。
* メッセージは ``comment`` に入ります。翻訳がある場合は ``class t`` に入ります。
* 新たなメッセージか、更新されたかは、 ``id`` で判断してください。

## 通信ポートの特定

* 通信ポートはレジストリから取得できます
* HTTPのみ、ゆかりねっと内部APIと同じ通信ポートを使います。

!!! Tech "使用条件"
    * ポートを開放したときに更新されます

* レジストリ位置：HKCU\Software\YukarinetteConnectorNeo\OneCommeServer

|名前|型|意味|
|:--|:--|:--|
|WebSocket|DWord32|WebSocketポート番号|

* レジストリ位置：HKCU\Software\YukarinetteConnectorNeo

|名前|型|意味|
|:--|:--|:--|
|HTTP|DWord32|HTTPポート番号|