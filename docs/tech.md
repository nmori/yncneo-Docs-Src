#連携について
!!! Info "内容について"
    この内容はサービス改良の中で予告なく改定されることがあります

## 翻訳・発話サーバ

* ゆかりねっとコネクターNEOを通して翻訳と読み上げをサポートします。
!!! Tech "使用条件"
    * 翻訳/発話連携サーバプラグインをONにしていること
    * 翻訳１の翻訳エンジンを選定していること（これが使われます）

### 翻訳

* 翻訳/発話連携サーバプラグインが開いているHTTPサーバもしくはWebSocketサーバに下記のリクエストを送付してください。
* 送付方式：HTTPの場合はPOST、WSの場合はテキスト
=== "Request"
    ```js
    {
        operation: 'translate',
        params: [
            {
                id: '0000-0000-0000-0000',
                lang: 'en_US',
                text: 'こんにちは'
            }
        ]
    }
    ```
=== "Response"
    ```js
    {
        operation: 'translate',
        status: 'success/failure'
        id: '0000-0000-0000-0000',
        lang: 'ja_JP',
        text: 'Hello.' 
    }
    ```

* 要求時は、翻訳してほしい言語を指定します。
* 返答時には、推定した言語と翻訳した文が来ます。
* statusがfailureの場合は、処理に失敗しています。

### 読み上げ

* 翻訳/発話連携サーバプラグインが開いているHTTPサーバもしくはWebSocketサーバに下記のリクエストを送付してください。
* 送付方式：HTTPの場合はPOST、WSの場合はテキスト
=== "Request"
    ```js
    {
        operation: 'speech',
        params: [
            {
                id: '0000-0000-0000-0000',
                text: 'こんにちは',
                talker: 'ずんだもん/VOICEVOX'
            }
        ]
    }
    ```
=== "Response"
    ```js
    {
        operation: 'speech',
        status: 'sended/failure'
        id: '0000-0000-0000-0000',
        text: 'こんにちは.' 
    }
    ```
    
* 要求時は、翻訳してほしい言語を指定します。
* 返答時には、推定した言語と翻訳した文が来ます。
* statusがfailureの場合は、処理に失敗しています。

### 音声話者リスト

* 送付方式：HTTPの場合はPOST、WSの場合はテキスト
=== "Request"
    ```js
    {
        operation: 'speech.getvoicelist',
        params: [
            {
                id: '0000-0000-0000-0000',
            }
        ]
    }
    ```
=== "Response"
    ```js
    {
        operation: 'speech.getvoicelist',
        status: 'sended/failure'
        id: '0000-0000-0000-0000',
        voice: [
                'ずんだもん/VOICEVOX',
                '弦巻マキ(日)/CeVIO AI'
            ]
        }
    }
    ```