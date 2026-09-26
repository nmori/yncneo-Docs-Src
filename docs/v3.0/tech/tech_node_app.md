# Node.js アプリの配り方

<!-- version-banner -->
!!! info ""
    ゆかコネNEO **v3.0** のドキュメントです（v3.0.0 beta 30 から）。v2.3 にはこの仕組みはありません。

!!! Info "内容について"
    この内容はサービス改良の中で予告なく改定されることがあります。利用者向けの説明は [Node.js アプリ連携](../plugin/plugin_nodehost.md) にあります。

[Node.js アプリ連携](../plugin/plugin_nodehost.md) プラグイン (Plugin_NodeHost) を使うと、Node.js で作ったアプリを
**node.exe を同梱せずに**配れます。利用者の ゆかコネNEO がアプリを起動・停止し、黒い画面も出しません。

| これまで | これから |
|---|---|
| node.exe (約 100MB) を作品ごとに同梱 | 同梱しない。ゆかコネNEO が Node.js v24 を 1 つだけ入れて全アプリで使う |
| 利用者が start-server.bat を起動し、黒い画面を開いたままにする | ゆかコネNEO と一緒に起動・終了する (落ちても残らない) |
| 「OBS より先に起動」を説明書で案内 | 不要 |
| ポートが塞がっていたら netstat / taskkill を案内 | 起動しない理由と、ポートを使っているプロセスを画面に出す |
| 字幕は「配信ソフト向けテキスト出力」の txt を監視 | txt もそのまま使える。WebSocket で直に受け取ることもできる |

## 1. 配り方

アプリのフォルダに `ync-app.json` を 1 つ足して zip にするだけです。`node` フォルダは要りません
(入っていても利用者の側で省きます)。`node_modules` は今までどおり同梱してください
(利用者の PC で `npm install` は走りません)。

```
my-caption-app/
├── ync-app.json      ← 足すのはこれだけ
├── server.js
├── config.json
├── package.json
├── node_modules/
└── public/
```

`ync-app.json` の例:

```json
{
  "id": "my-caption-app",
  "name": "字幕表示アプリ",
  "version": "1.0.0",
  "author": "作者名",
  "main": "server.js",
  "node": ">=22",
  "ports": [3000],
  "urls": [
    { "label": "字幕", "url": "http://localhost:3000/index.html" },
    { "label": "要約", "url": "http://localhost:3000/summary.html" }
  ],
  "obsFileOutputDir": "public",
  "autoStart": true
}
```

| 項目 | 意味 | 無いとき |
|---|---|---|
| `id` | 置き場のフォルダ名。英小文字・数字・`. _ -` で 64 文字まで | 必須 |
| `name` / `version` / `author` | 画面と、入れる前の確認に出す | `name` は `id` |
| `main` | 起動するファイル (アプリのフォルダからの相対) | `index.js` |
| `args` | `main` の後ろに付ける引数 (文字の配列) | なし |
| `node` | 要る Node.js の版。`">=22"` / `"24"` / `"^24.3"` | 問わない |
| `ports` | 待ち受けるポート。起動の前に空きを確かめる | 確かめない |
| `urls` | 利用者が OBS に貼る URL。画面にコピーのボタンが並ぶ | 起動時のログに出た `http://localhost:…` を拾って出す |
| `obsFileOutputDir` | 「配信ソフト向けテキスト出力」の書き出し先にしてほしいフォルダ。画面でパスをコピーできる | 案内しない |
| `autoStart` | ゆかコネNEO と一緒に起動するかの初めの値 (利用者が変えられる) | `true` |

- 作業フォルダはアプリのフォルダです (`start-server.bat` の `cd /d "%~dp0"` と同じ)。
- 同じ `id` を入れ直すと、前のフォルダは `_backup` へ退避されます。利用者が書き換えた
  `style.css` や `config.json` はそこから戻せます。
- `ync-app.json` の無い zip / フォルダも入れられます (package.json の `main` か `server.js` を起動)。
  ただし URL やポートの案内は出ません。

## 2. アプリに渡る環境変数

| 変数 | 中身 |
|---|---|
| `YNC_WS_TEXT_URL` | 字幕の WebSocket (**言語ごと**の簡単な形)。例 `ws://127.0.0.1:11901/text` |
| `YNC_WS_CAPTION_URL` | 字幕の WebSocket (**テンプレートと同じ**完全な形)。例 `ws://127.0.0.1:11901/` |
| `YNC_WS_TEXTONLY_URL` | 確定した原文だけをプレーンテキストで 1 行ずつ |
| `YNC_WS_BASE` | 上の 3 つの共通部分 |
| `YNC_HTTP_URL` | ゆかコネNEO の HTTP (テンプレートや `/api/…`) |
| `YNC_APP_ID` / `YNC_APP_DIR` | このアプリの ID と置き場 |
| `YNC_DATA_DIR` | 書き込み用のフォルダ。入れ直しても消えない |
| `YNC_LANG` | ゆかコネNEO の表示言語 (`ja` / `en` など) |

★ **ポートを決め打ちしないでください。** ゆかコネNEO は空いているポートを選ぶので、PC によって変わります。
ゆかコネNEO を閉じるとアプリも終わり、次に ゆかコネNEO を起動したときに (「ゆかコネNEO と一緒に起動する」が入なら)
新しい値で起動し直されるので、起動時に読めば足ります。

## 3. 字幕を WebSocket で受け取る

Node.js 22 以上は `WebSocket` が組み込みなので、追加のパッケージは要りません。
最小の例は、ゆかコネNEO のインストール先の `Plugin\Plugin_NodeHost\samples\caption-log\` にあります。

### `/text` (言語ごとの形)

```json
{
  "textList": { "ja": "こんにちは", "en": "Hello" },
  "fixedText": true,
  "talkerName": "話者名",
  "talkerID": "…",
  "MessageID": "…",
  "isAlreadyShown": false,
  "isDeleted": false,
  "isOwnersTalkData": true
}
```

### `/` (テンプレートと同じ完全な形)

`Text2`〜`Text5` が翻訳 1〜4、原文は `Text1` か `Text6` です (「配信ソフト向けテキスト出力」の
Native.txt / Translate1〜4.txt と同じ並び)。`Lang1`〜`Lang6` が言語、`TextFixed` が確定、
`isDeleted` が消去、`MsgID` が発話の ID です。

- 原文がどちらに入るかは利用者の「母国語の表示」の設定で変わります (上に出す=`Text1`、下に出す=`Text6`、
  出さない=どちらにも入らない)。`m.Text1 || m.Text6` のように両方を見てください。
- 話している途中の字幕も届きます (`TextFixed: false`)。
- 確定は 2 回届くことがあります (1 回目は翻訳前、2 回目が訳文付き)。同じ `MsgID` で上書きしてください。
- `KeepTime` は秒ですが、ゆかコネNEO が消す時刻を決めている設定では 0 以下になります。
  そのときは自分で消さず、`isDeleted: true` が届くのを待ってください。
- `/text` の `textList` は言語が鍵なので、原文と同じ言語の翻訳先があると 1 つにまとまります。
  原文を出さない設定では原文が入りません。

### 「配信ソフト向けテキスト出力」の txt を監視しているアプリを書き換える例

Native.txt / Translate1〜4.txt を chokidar で監視し、変わったら socket.io で `fileChanges` を送っている
サーバーの例です。txt の監視の代わりに字幕を直に受け取り、同じ `fileChanges` を出します。
環境変数が無い (従来どおり .bat などで起動した) ときは txt を監視し続けるので、
両方の配り方で動きます。

```js
// server.js の、txt の監視を始めるところ (resetFileWatchers(config.files);) を置き換える
const captionUrl = process.env.YNC_WS_CAPTION_URL;

if (captionUrl) {
  let delay = 1000;
  const connect = () => {
    const ws = new WebSocket(captionUrl);
    ws.addEventListener('open', () => { delay = 1000; });
    ws.addEventListener('message', (ev) => {
      let m;
      try { m = JSON.parse(ev.data); } catch { return; }
      if (m.isDeleted) return;

      // Native.txt, Translate1.txt … Translate4.txt と同じ並び
      const lanes = [m.Text1 || m.Text6 || '', m.Text2 || '', m.Text3 || '', m.Text4 || '', m.Text5 || ''];
      io.emit('fileChanges', config.files.map((file, i) => ({ file, content: lanes[i] ?? '' })));
    });
    ws.addEventListener('close', () => {
      setTimeout(connect, delay);
      delay = Math.min(delay * 2, 10000);
    });
    ws.addEventListener('error', () => {});
  };
  connect();
} else {
  resetFileWatchers(config.files);
}
```

トークの見出し・要約 (Summary.txt) は WebSocket では届かないので、txt の監視を残してください。

## 4. 動作の確かめ方

1. ゆかコネNEO で「Node.js アプリ連携」を「使う」にし、設定の「フォルダから追加」で作業中のフォルダを選ぶ
2. アプリのページの「ログ」に `console.log` が出る。`! ` で始まる行は標準エラー
3. 直したら、同じフォルダをもう一度「フォルダから追加」して「再起動」

ログは `<アプリの置き場>\ync-app.log` にも残ります (1MB で 1 世代だけ回す)。

## 5. 気をつけること

- アプリは利用者の PC で自由に動くプログラムです。利用者には「信頼できる作者のものだけを入れて」と案内しています。
- Node.js の版は ゆかコネNEO の更新で上がります (現在 v24 LTS)。`node` に上限は書けません。
- 利用者の PC には npm がありません。`postinstall` などは走りません。
