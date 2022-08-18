#プラグイン系APIについて

!!! Info "内容について"
    この内容はサービス改良の中で予告なく改定されることがあります

## 翻訳・発話サーバ

* ゆかりねっとコネクターNEOを通して翻訳と読み上げをサポートします。
!!! Tech "使用条件"
    * 翻訳/発話連携サーバプラグインをONにしていること
    * 翻訳１の翻訳エンジンを選定していること（これが使われます）

### 翻訳（１言語）

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
=== "Response(OK)"
    ```js
    {
        operation: 'translate',
        status: 'success'
        id: '0000-0000-0000-0000',
        lang: 'ja_JP',
        text: 'Hello.' 
    }
    ```
=== "Response(NG)"
    ```js
    {
        operation: 'translate',
        status: 'failure'
        id: '0000-0000-0000-0000',
        lang: 'ja_JP',
        text: 'こんにちは.' 
    }
    ```
* 要求時は、翻訳してほしい言語を指定します。
* 返答時には、推定した言語と翻訳した文が来ます。
* statusがfailureの場合は、処理に失敗しています。

### 翻訳（複数言語）

!!! Tips "対応プラグインバージョン: v1.4以上"

* 翻訳/発話連携サーバプラグインが開いているHTTPサーバもしくはWebSocketサーバに下記のリクエストを送付してください。
* 送付方式：HTTPの場合はPOST、WSの場合はテキスト

=== "Request"
    ```js
    {
        operation: 'translates',
        params: [
            {
                id: '0000-0000-0000-0000',
                lang: [
                    'ja_JP',
                    'en_US',
                    'fr_FR'
                ],
                text: 'こんにちは'
            }
        ]
    }
    ```
=== "Response(OK) Case1"
    ```js
    {
        operation: 'translates',
        status: 'success'
        id: '0000-0000-0000-0000',
        detect_language : 'ja_JP',
        result : [
            {
                lang: 'ja_JP',
                text: 'こんにちは' 
            },
            {
                lang: 'en_US',
                text: 'Hello.' 
            },
            {
                lang: 'fr_FR',
                text: 'bonjour.' 
            }
        ]
    }
    ```
=== "Response(OK) Case2"
    ```js
    {
        operation: 'translates',
        status: 'success'
        id: '0000-0000-0000-0000',
        detect_language : 'unknown',
        result : [
            {
                lang: 'ja_JP',
                text: 'こんにちは' 
            },
            {
                lang: 'en_US',
                text: 'Hello.' 
            },
            {
                lang: 'fr_FR',
                text: 'bonjour.' 
            }
        ]
    }
    ```

=== "Response(NG)"
    ```js
    {
        operation: 'translates',
        status: 'failure'
        id: '0000-0000-0000-0000',
        message: '翻訳サーバに接続できません'
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
=== "Response(OK)"
    ```js
    {
        operation: 'speech',
        status: 'sended'
        id: '0000-0000-0000-0000',
        text: 'こんにちは.' 
    }
    ```
=== "Response(NG)"
    ```js
    {
        operation: 'speech',
        status: 'failure'
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
=== "Response(OK)"
    ```js
    {
        operation: 'speech.getvoicelist',
        status: 'sended'
        id: '0000-0000-0000-0000',
        voice: [
                'ずんだもん/VOICEVOX',
                '弦巻マキ(日)/CeVIO AI'
            ]
        }
    }
    ```
=== "Response(NG)"
    ```js
    {
        operation: 'speech.getvoicelist',
        status: 'failure'
        id: '0000-0000-0000-0000'
    }
    ```

### 発話の強制停止

* 送付方式：HTTPの場合はPOST、WSの場合はテキスト
* キューをクリアするため、現在発話動作に入っているものは読み上げします。

=== "Request"
    ```js
    {
        operation: 'speech.stop',
        params: [
            {
                id: '0000-0000-0000-0000',
            }
        ]
    }
    ```
=== "Response(OK)"
    ```js
    {
        operation: 'speech.stop',
        status: 'sended'
        id: '0000-0000-0000-0000',
    }
    ```
=== "Response(NG)"
    ```js
    {
        operation: 'speech.stop',
        status: 'failure'
        id: '0000-0000-0000-0000'
    }
    ```