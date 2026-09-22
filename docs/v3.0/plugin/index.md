# プラグインでゆかコネをパワーアップ！

<!-- version-banner -->
!!! info ""
    ゆかコネNEO **v3.0** のドキュメントです。v2.3 をお使いの方は [v2.3 版のこのページ](../../v2.3/plugin/index.md) を、違いを知りたい方は [v2.3 から v3.0 への移行](../../mig/mig_neo_v3.0.md) をご覧ください。


<div class="tips-box">
  <h4>プラグインとは？</h4>
  <p>プラグイン（追加機能）を使えば、自分好みにゆかコネをカスタマイズできます。必要な機能だけを選んで追加するから、自分の使い方にピッタリ合わせられます！</p>
</div>

!!! info "v3.0 でのプラグインについて"
    * **設定画面を持つほぼすべてのプラグイン（約 60 本）で、設定画面が新しくなりました。**見た目が揃い、表示言語で出し分けられ、各項目に「何を入れる欄か」の説明が付いています
    * **v2.3 向けにビルドされたプラグインは読み込めません。**公式配布のものはすべて対応済みですが、自作・個人配布のものは v3.0（.NET 10）対応版が必要です
    * 内蔵ブラウザを使う 4 本（内蔵ブラウザ／コメントスクリーン／ニコ生／clusterウェブトリガ）は、**WebView2** に切り替わりました
    * → [v2.3 から v3.0 への移行](../../mig/mig_neo_v3.0.md)

## やりたいことから選ぶ { #purpose }

<div class="purpose-grid">
  <a href="#voice" class="purpose-card">
    <div class="purpose-icon">🔊</div>
    <h3>声で読み上げたい</h3>
    <p>文字を音声で読み上げられるようになる</p>
  </a>
  <a href="#display" class="purpose-card">
    <div class="purpose-icon">📺</div>
    <h3>字幕をおしゃれにしたい</h3>
    <p>見た目や表示方法をカスタマイズできる</p>
  </a>
  <a href="#streaming" class="purpose-card">
    <div class="purpose-icon">📡</div>
    <h3>配信で使いたい</h3>
    <p>OBSやXSplitなどと連携できる</p>
  </a>
  <a href="#platform" class="purpose-card">
    <div class="purpose-icon">🌐</div>
    <h3>他のサービスと連携したい</h3>
    <p>DiscordやVRChatなどと接続できる</p>
  </a>
</div>

<div class="tips-box">
  <h4>試してみるのがいちばん！</h4>
  <p>使ってみないとわからないこともあります。気になるプラグインはとりあえず試してみて、自分に合うかどうか確かめてみましょう。合わなければ簡単に無効化もできます。</p>
</div>

## カテゴリー別プラグイン一覧 { #catalog }

### 読み上げ { #voice }

自分の声を機械的に読み上げてくれるプラグインです。

|プラグイン名|できるようになること|詳細|
|------------|-------------------|-----|
|棒読みちゃん連携|自分の声を棒読みちゃんで読み上げられる|[詳しく見る](plugin_bouyomi.md)|
|Softalk読み上げ|認識した文字をSoftalkで読み上げられる|[詳しく見る](plugin_softalk.md)|
|読み上げ連携|VOICEVOXなどの高品質な音声で読み上げられる|[詳しく見る](plugin_playvoice.md)|

### サウンド { #sound }

特定の言葉をきっかけに音や動画を再生できます。

|プラグイン名|できるようになること|詳細|
|------------|-------------------|-----|
|動画再生|言葉に合わせて動画クリップを表示できる|[詳しく見る](plugin_MediaPlayer.md)|
|音源再生|特定のセリフで効果音や音楽を流せる|[詳しく見る](plugin_playsound.md)|

### 認識の修正や変換 { #text }

音声認識の結果を自分好みに修正・変換できます。

|プラグイン名|できるようになること|詳細|
|------------|-------------------|-----|
|辞書|専門用語や名前を正しく認識できるようになる|[詳しく見る](plugin_dictionary.md)|
|正規表現|細かいルールで文字を自動修正できる|[詳しく見る](plugin_regexp.md)|
|ノムリッシュ変換|文章をノムリッシュ調に変換して楽しめる|[詳しく見る](plugin_nomlish.md)|
|文字変換|漢字やカタカナなど文字種を自由に変換できる|[詳しく見る](plugin_ConvertString.md)|
|強制整形|字幕の改行や区切りを自分で設定できる|[詳しく見る](plugin_forcestyle.md)|
|ルビ付与|難しい漢字にふりがなをつけられる|[詳しく見る](plugin_ruby.md)|
|ゆかコネ互換|文字幅と文字サイズを自動調整して、旧ゆかコネと同じ見え方にできる|[詳しく見る](plugin_viewcompat.md)|
|不適切語の置換|不適切な言葉を自動で検出して置き換えられる|[詳しく見る](plugin_replacefwords.md)|
|GPT3整形/AIアシスタント|AIが字幕を整形したり会話に応答してくれる|[詳しく見る](plugin_GPT3.md)|

### 表示関連 { #display }

字幕の見た目をカスタマイズできます。

|プラグイン名|できるようになること|詳細|
|------------|-------------------|-----|
|内蔵ブラウザ|ブラウザ内で字幕表示をカスタマイズできる|[詳しく見る](plugin_browser.md)|
|歌詞支援|歌っている曲の歌詞を表示できる|[詳しく見る](plugin_LyricAssist.md)|
|フォト読み込み|特定の言葉で画像を表示できる|[詳しく見る](plugin_photopickup.md)|
|表示拡張(スタンプ)|文字の代わりに絵文字やスタンプを表示できる|[詳しく見る](plugin_viewextend.md)|
|色の変更(β)|条件に合わせて色や表現を変更します|[詳しく見る](plugin_regexp_color.md)|
|遅延|字幕の表示タイミングを調整できる|[詳しく見る](plugin_delay.md)|
|表示時間の自動調整|文字数に応じて字幕の表示時間を自動で変えられる|[詳しく見る](plugin_dynamickeeptime.md)|
|インフォグラフィックス(実験的)|会話の内容を図にして表示できる|[詳しく見る](plugin_infographics.md)|

### Windows連携 { #windows }

Windowsの他の機能と連携できます。

|プラグイン名|できるようになること|詳細|
|------------|-------------------|-----|
|クリップボード連携|認識した内容をクリップボードにコピーできる|[詳しく見る](plugin_clipboard.md)|
|MIDI入力|MIDIキーボードからの入力を取り込める|[詳しく見る](plugin_midiinput.md)|
|ホットキー|特定の言葉でショートカットキーを実行できる|[詳しく見る](plugin_hotkey.md)|

### 配信（OBS・コメント） { #streaming }

配信ソフトと連携して字幕を表示できます。

|プラグイン名|できるようになること|詳細|
|------------|-------------------|-----|
|コメジェネ連携|HTML5コメントジェネレータで動くような字幕にできる|[詳しく見る](plugin_commentgen.md)|
|配信ソフト向けテキスト出力|XSplitなどで字幕を表示できる|[詳しく見る](plugin_OBSFile.md)|
|OBS連携 WSv4|OBSに字幕を直接送信できる|[詳しく見る](plugin_OBS.md)|
|OBS連携 WSv5|OBS v28以降に字幕を送信できる|[詳しく見る](plugin_OBS5.md)|

### アプリ連携 { #apps }

他のアプリケーションと連携できます。

|プラグイン名|できるようになること|詳細|
|------------|-------------------|-----|
|わんコメテンプレ連携|わんコメの字幕テンプレートを使用できる|[詳しく見る](plugin_OCTemplateGen.md)|
|わんコメ連携|わんコメにコメントとして字幕を送れる|[詳しく見る](Plugin_OCComm.md)|
|VaNiiツール連携|VaNiiシリーズで字幕を表示できる|[詳しく見る](plugin_vanii.md)|
|VRオーバーレイ|VR空間に字幕をオーバーレイ表示できる|[詳しく見る](plugin_vroverlay.md)|
|ばもきゃ連携|VMCProtocolで3Dモデルと連動できる|[詳しく見る](plugin_vmc.md)|
|MTGカード支援|MTGカードを自動で表示できる|[詳しく見る](plugin_MTGCard.md)|
|VTubeStudio連携|VTubeStudioの画面に字幕を表示できる|[詳しく見る](plugin_VtubeStudio.md)|

### プラットフォーム連携 { #platform }

オンラインサービスやVRプラットフォームと連携できます。

|プラグイン名|できるようになること|詳細|
|------------|-------------------|-----|
|clusterウェブトリガ|clusterのギミックを音声で操作できる|[詳しく見る](plugin_cluster_wtrig.md)|
|clusterチャット転送|clusterのチャットに自分の声を表示できる|[詳しく見る](plugin_clustertransfer.md)|
|バーチャルキャスト連携|バーチャルキャストで字幕を表示できる|[詳しく見る](plugin_vcas.md)|
|VRChat OSC連携|VRChatで自分の声を字幕として表示できる|[詳しく見る](plugin_vrchat_osc.md)|
|NeosVR 連携|NeosVRで字幕を表示できる|[詳しく見る](plugin_neosvr.md)|
|Discord BOT連携|Discordのチャットに自動で字幕を送信できる|[詳しく見る](plugin_dicord.md)|
|Discord Webhook連携|Discordのチャンネルに字幕を転送できる|[詳しく見る](plugin_dicordwebhook.md)|
|Notion連携|Notionに字幕内容を自動記録できる|[詳しく見る](plugin_notion.md)|
|Twitchチャット連携|Twitchチャットに字幕を送信できる|[詳しく見る](plugin_twitch.md)|
|ニコニコ生放送連携|ニコニコ生放送のコメントとして字幕を送信できる|[詳しく見る](plugin_niconama.md)|
|YouTube Live字幕送信|YouTube Liveのクローズドキャプションを使える|[詳しく見る](plugin_youtube.md)|
|YouTube タイムコード生成|動画編集用のタイムコードを自動生成できる|[詳しく見る](plugin_youtubetimecode.md)|
|ZOOM連携|ZOOMミーティングで字幕を表示できる|[詳しく見る](plugin_zoom.md)|
|Slack Webhook連携|Slackのチャンネルに字幕を送信できる|[詳しく見る](plugin_slackwebhook.md)|
|Teams Webhook連携|Teamsのチャンネルに字幕を送信できる|[詳しく見る](plugin_teamswebhook.md)|
|コメントスクリーン連携|コメントスクリーンと連携できる|[詳しく見る](plugin_comscr.md)|

### API・ツール拡張 { #api }

より高度なカスタマイズやシステム連携が可能です。

|プラグイン名|できるようになること|詳細|
|------------|-------------------|-----|
|翻訳・発話連携|外部システムと連携して翻訳処理ができる|[詳しく見る](plugin_transSrv.md)|
|HTTPコール|特定の言葉でWebサービスを呼び出せる|[詳しく見る](plugin_httpcall.md)|
|WebSocketコール|WebSocketで他のアプリと通信できる|[詳しく見る](plugin_wscall.md)|
|UDP通信|UDP通信で字幕データを送信できる|[詳しく見る](plugin_udpunit.md)|
|ファイル出力|字幕データをファイルに保存できる|[詳しく見る](plugin_exporter.md)|
|会話の記録|話した内容を記録して、あとから見返したり書き出したりできる|[詳しく見る](plugin_talkhistory.md)|
|字幕共有|自分の字幕（原文・翻訳）を共有コードで相手に届けたり、相手の字幕を受け取ったりできる（v3.0 新規）|[詳しく見る](plugin_captionshare.md)|
|Python連携|Pythonスクリプトで独自機能を作れる|[詳しく見る](plugin_pythonunit.md)|

### つかいやすさ向上 { #usability }

日常的な使用をもっと便利にするプラグインです。

|プラグイン名|できるようになること|詳細|
|------------|-------------------|-----|
|直接入力|キーボードから直接入力できる|[詳しく見る](plugin_directinput.md)|
|入力支援|メモ帳のような画面から文章を入力できる|[詳しく見る](plugin_InputAssist.md)|
|起動支援|PCが起動したときに自動で立ち上がるようにできる|[詳しく見る](plugin_startup.md)|
|アップデート通知|新バージョンを自動で確認できる|[詳しく見る](plugin_update.md)|

<div class="tips-box">
  <h4>プラグインの有効化方法</h4>
  <p>使いたいプラグインが見つかったら、<a href="enabled/">プラグインの有効化ページ</a>を参考に有効化してみましょう。プラグインは必要に応じて追加・削除できるので、気軽に試せます！</p>
</div>
