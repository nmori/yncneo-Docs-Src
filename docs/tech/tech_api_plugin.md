#プラグイン系APIについて

!!! Info "内容について"
    この内容はサービス改良の中で予告なく改定されることがあります


## 翻訳・発話サーバ

* ゆかりねっとコネクターNEOを通して読み上げ設定のコントロールをサポートします。

* ゆかりねっとコネクターNEOを通して翻訳と読み上げをサポートします。
!!! Tech "使用条件"
    * 翻訳/発話連携サーバプラグインをONにしていること
    * 翻訳１の翻訳エンジンを選定していること（これが使われます）
    * 送信先ポートはレジストリから取得します

!!! Tech "使用条件"
    * プラグイン v2.3以上

### HTTP経由
#### 発話の停止

* 送付方式：HTTP(GET)

=== "停止指示"
    ```js
        http://localhost:15520/api/command?target=Plugin_PlayVoice&command=stop
    ```

#### 発話パラメータの設定

* 送付方式：HTTP(GET)

=== "停止パラメータ"

|パラメータ|値    |例          |
|---------|------|------------|
|engine   |エンジン名|さとうささら/CeVIO_64|
|pitch    |高さ    | 1.0 |
|accent   |抑揚    | 1.0 |
|speed   |速度    | 1.0 |
|volume   | 音量  | 1.0 |
|quality   |声質    | 1.0 |

* engineに指定する文字の区切り文字 ``/`` は、``%2F`` に置き換えてください

=== "停止指示"
    ```js
        http://localhost:15520/api/command?target=Plugin_PlayVoice&command=set&engine=さとうささら%2FCeVIO_64
    ```


### 共通項目
#### 通信ポートの特定

* 通信ポートはレジストリから取得できます

!!! Tech "使用条件"
    * ポートを開放したときに更新されます

* レジストリ位置：HKCU\Software\YukarinetteConnectorNeo\TransServer

|名前|型|意味|
|:--|:--|:--|
|WebSocket|DWord32|WebSocketポート番号|
|HTTP|DWord32|HTTPポート番号|

### プラグイン通信
#### 翻訳（１言語）

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

#### 翻訳（複数言語）

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

#### 読み上げ

* 翻訳/発話連携サーバプラグインが開いているHTTPサーバもしくはWebSocketサーバに下記のリクエストを送付してください。
* 送付方式：HTTPの場合はPOST、WSの場合はテキスト

!!! info "パラメータ拡張"
    * v2.0.73よりパラメータが追加されました。(volume)
    * volumeは発話音量の設定です。（`float`型、単位は`倍`。有効指定範囲 `0.2～2`　）

=== "Request(Standard)"
    ```js
    {
        operation: 'speech',
        params: [
            {
                id: '0000-0000-0000-0000',
                text: 'こんにちは',
                talker: 'ずんだもん-ノーマル/VOICEVOX'
            }
        ]
    }
    ```
=== "Request(Extend)"
    ```js
    {
        operation: 'speech',
        params: [
            {
                id: '0000-0000-0000-0000',
                text: 'こんにちは',
                talker: 'ずんだもん-ノーマル/VOICEVOX',
                volume: 1.0
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

* 要求時は、発話してほしいボイスキャラクターを指定するとその音源で話そうとします。
* statusがfailureの場合は、プラグインが無効な場合など要求が出せなかった場合にでます。
* statusがsendedの場合、要求自体はだせたという意味で、発話が完了したわけではありません。

#### 音声話者リスト

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

#### 発話の強制停止

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


#### バージョンの取得

!!! Tips "対応プラグインバージョン: v1.4a以上"

* 送付方式：HTTPの場合はPOST、WSの場合はテキスト

=== "Request"
    ```js
    {
        operation: 'version',
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
        operation: 'version',
        status: 'success',
        version: [
            {
                System: '1.959',
                Plugin: '1.4a'
            }
        ]
        id: '0000-0000-0000-0000',
    }
    ```
=== "Response(NG)"
    ```js
    {
        operation: 'version',
        status: 'failure',
        id: '0000-0000-0000-0000'
    }
    ```
|名前|型|意味|
|:--|:--|:--|
|System|String|NEO本体のバージョン|
|Plugin|String|翻訳/発話連携サーバプラグイン|

#### OSCの送信

* 翻訳/発話連携サーバプラグインが開いているHTTPサーバもしくはWebSocketサーバに下記のリクエストを送付してください。
* 送付方式：HTTPの場合はPOST、WSの場合はテキスト
* 対応バージョン：v2.0.73～

=== "Request"
    ```js
    {
        operation: 'osc',
        params: [
            {
                address: '/comment/text',
                id: '0000-0000-0000-0000',
                text: 'こんにちは',
                target : [
                    'vrchat',
                    'virtualcast',
                    'unity',
                    'neosvr'
                ]
            }
        ]
    }
    ```
=== "Response(OK)"
    ```js
    {
        operation: 'osc',
        status: 'sended'
        id: '0000-0000-0000-0000',
        text: 'こんにちは.' 
    }
    ```
=== "Response(NG)"
    ```js
    {
        operation: 'osc',
        status: 'failure'
        id: '0000-0000-0000-0000',
        text: 'こんにちは.' 
    }
    ```
!!! info "連携に必要なプラグイン名"
    |送信先        |有効化すべきプラグイン|
    |-------------------|------------------------------|
    |vrchat       |VRChatプラグイン　　　　　　　　　　|
    |virtualcast   |VirtualCastプラグイン　　　　　　　　　　|
    |unity         |VMCプラグイン　　　　　　　　　　|
    |neosvr       |NeosVRプラグイン　　　　　　　　　　|

* 指定したOSC通信をプラットフォームに送信します。
* statusがfailureの場合は、プラグインが無効な場合など要求が出せなかった場合にでます。
* statusがsendedの場合、要求自体はだせたという意味です。

## 入力支援

* ゆかりねっとコネクターNEOの文字入力を支援します
!!! Tech "使用条件"
    * 入力支援プラグインをONにしていること
    * 送信先ポートはレジストリから取得します

### 遠隔操作

* 送付方式：HTTP(GET)

=== "１行前に移動"
    ```js
        http://localhost:15520/api/command?target=Plugin_InputAssist&command=prev
    ```
=== "１行後に移動"
    ```js
        http://localhost:15520/api/command?target=Plugin_InputAssist&command=next
    ```
=== "カーソル行を送信"
    ```js
        http://localhost:15520/api/command?target=Plugin_InputAssist&command=send
    ```
=== "カーソル行を送り次の行に移動"
    ```js
        http://localhost:15520/api/command?target=Plugin_InputAssist&command=sendnext
    ```

## 歌詞プラグイン

* ゆかりねっとコネクターNEOの文字入力を支援します
!!! Tech "使用条件"
    * 入力支援プラグインをONにしていること
    * 送信先ポートはレジストリから取得します

### 遠隔操作

* 送付方式：HTTP(GET)

=== "再生"
    ```js
        http://localhost:15520/api/command?target=Plugin_LyricAssist&command=play
    ```
=== "一時停止"
    ```js
        http://localhost:15520/api/command?target=Plugin_LyricAssist&command=pause
    ```
=== "停止"
    ```js
        http://localhost:15520/api/command?target=Plugin_LyricAssist&command=stop
    ```
=== "ファイルロード"
    * ``sukiyuki.stl`` を読み込む場合
    ```js
        http://localhost:15520/api/command?target=Plugin_LyricAssist&command=load&file=d:/sukiyuki.stl
    ```
## OSCプラグイン

* 指定したOSCメッセージを送付します。

!!! Tech "使用条件"
    * OSCプラグインをONにしていること
    * 送信先ポートはレジストリから取得します
    * OSCプラグイン v1.5以上で有効

### OSCメッセージの遠隔発火

* 送付方式：HTTP(GET)

=== "実行"
    * 送信タグ名 ``EyeClose`` を送りたい場合
    ```js
        http://localhost:15520/api/command?target=Plugin_VRChat_OSC&command=exec&tag=EyeClose
    ```

## HTTPコールプラグイン

* 指定したHTTP呼び出し(GET)を送付します。

!!! Tech "使用条件"
    * HTTPプラグインをONにしていること
    * 送信先ポートはレジストリから取得します
    * ゆかりねっとコネクターNEO v2.0～で有効

### HTTPメッセージの遠隔発火

* 送付方式：HTTP(GET)

=== "実行"
    * 送信タグ名 ``CALL`` を送りたい場合
    ```js
        http://localhost:15520/api/command?target=Plugin_HTTPCall&command=exec&tag=CALL
    ```
## clusterウェブトリガープラグイン

* 指定したHTTP呼び出し(GET)を送付します。

!!! Tech "使用条件"
    * clusterウェブトリガープラグインをONにしていること
    * 送信先ポートはレジストリから取得します
    * ゆかりねっとコネクターNEO v2.0～で有効

### ウェブトリガーの遠隔発火

* 送付方式：HTTP(GET)

=== "実行"
    * 送信タグ名 ``Trig1`` を発火したい場合
    ```js
        http://localhost:15520/api/command?target=Plugin_ClusterTrigger&command=exec&tag=Trig1
    ```
## NeosVRプラグイン

* NeosVRと通信してトリガーをかけることができます。

!!! Tech "使用条件"
    * NeosVRプラグインをONにしていること
    * ゆかりねっとコネクターNEO v2.0～で有効

### NeosVRメッセージの遠隔発火

* 送付方式：HTTP(GET)

=== "実行"
    * 送信タグ名 ``CALL`` を送りたい場合
    ```js
        http://localhost:15520/api/command?target=Plugin_NeosVR&command=exec&tag=CALL
    ```
    ```
## VTuberStudio プラグイン

* VTuberStudioと通信してトリガーをかけることができます。

!!! Tech "使用条件"
    * VTuberStudioプラグインをONにしていること
    * ゆかりねっとコネクターNEO v2.0.17～で有効

### VTuberStudioキーバインドアクションの遠隔発火

* 送付方式：HTTP(GET)

=== "実行"
    * 送信タグ名 ``CALL`` を送りたい場合
    ```js
        http://localhost:15520/api/command?target=Plugin_VtuberStudio&command=exec&tag=CALL
    ```

