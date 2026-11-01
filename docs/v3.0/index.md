# v3.0 のドキュメント

ゆかコネNEO **v3.0**（先行開発版）向けのドキュメントです。

!!! warning "v2.3 をお使いの方へ"
    v3.0 は画面の並びと設定の持ち方が v2.3 から変わっています。
    v2.3 の手順で読むと合わないところが出るので、[v2.3 のドキュメント](../v2.3/index.md)をご覧ください。
    どちらを使っているか分からないときは[ドキュメントのバージョン](../versions.md)へ。

## はじめて使う方

<div class="purpose-grid">
  <a href="guide/quickstart/" class="purpose-card">
    <div class="purpose-icon">⏱️</div>
    <h3>5分クイックスタート</h3>
    <p>まず字幕を出すところまで</p>
  </a>
  <a href="cs/cs_startup/" class="purpose-card">
    <div class="purpose-icon">⚙️</div>
    <h3>はじめての設定</h3>
    <p>起動してから配信に出すまでを順番に</p>
  </a>
  <a href="qa/troubleshooting/" class="purpose-card">
    <div class="purpose-icon">🩹</div>
    <h3>こんなときは</h3>
    <p>うまくいかないときの対処</p>
  </a>
</div>

## v2.3 から上げる方

先に [v2.3 → v3.0 の移行](../mig/mig_neo_v3.0.md) を読んでください。
**設定は自動では引き継がれません。**アプリの中から 1 回だけ取り込み操作が要ります。

## v3.0 で変わったところ（ざっくり）

| 変わったもの | 内容 | 詳しくは |
|:--|:--|:--|
| 中身の土台 | .NET 10 になりました。フォルダを置くだけで動くのは同じです。内蔵ブラウザが WebView2 になったぶん、**容量は v2.3 より小さくなりました** | [移行ページ](../mig/mig_neo_v3.0.md) |
| 設定の引き継ぎ | v2.3 の設定は自動では入りません。「設定の保存・復元」から取り込みます | [設定の保存・復元](startup/startup_profile.md) |
| 左メニュー | 見た目に関する項目（母国語と言語の表示／フォント設定と配置／色）を「レイアウトデザインの選択」にまとめました | [標準設定項目](startup/startup_basic.md) |
| コックピット | 配信中によく使うものだけを 1 枚にまとめた画面が増えました | [標準設定項目](startup/startup_basic.md) |
| 設定さがし | 左メニューの検索欄に項目名を入れると、その設定まで飛べます | [標準設定項目](startup/startup_basic.md) |
| はじめての案内 | 3 ステップのウィザードになりました（あなたのこと・やりたいこと → 声を入れる → 配信ソフトに出す） | [はじめての設定](cs/cs_startup.md) |
| プラグインの設定画面 | 設定画面を持つほぼすべてのプラグイン（約 60 本）で、設定画面が共通の形に変わりました | [プラグイン一覧](plugin/index.md) |
| 読み上げ | ボイスパレット・マイボイスが増え、詳細設定が 6 ページに整理されました | [読み上げ](plugin/plugin_playvoice.md) |
| 内蔵ブラウザ | CefSharp から WebView2 に変わりました | [内蔵ブラウザ](plugin/plugin_browser.md) |

## 最近の更新で増えたこと（v3.0.1～v3.0.13）

| 増えたこと | 内容 | 詳しくは |
|:--|:--|:--|
| ライブ設定 | 操作パネルのタブ「ライブ設定」で、配信ごとに変わる値（配信URLや部屋の名前など）をその場で入れられます。プラグインの帯をダブルクリックすると接続／切断できます（v3.0.12） | [ライブ設定とプラグインの帯](startup/startup_basic.md#live-settings) |
| いまの状態 | 配信中によく見るものを 1 枚にまとめた画面です。見出しから音声認識画面・字幕ウィンドウを開けます（v3.0.12） | [いまの状態](startup/startup_basic.md#cockpit) |
| 字幕デザイン | 一覧のタイルを OBS へドラッグするとブラウザソースが入ります。数字の手入力、「表記」タブ、「テンプレートの枠」の 3 択も増えました | [字幕デザイン](startup/startup_basic.md#design) |
| 字幕テンプレート | MMORPG・レトロ系・確定演出・紹介動画テロップ・アバター表示対応・カウンター連動・ワードバトルなど、60 種類になりました | [レイアウト](startup/startup_layout.md) / [ワードバトル](startup/startup_layout.md#word-battle) |
| 文字強調 | 効果が大きく増え（光と影・縁取り・動き・タイプライターなど）、重ねがけ・大きさ・文字の色・画像への差し替えができます。触るとすぐ字幕に反映されます（v3.0.13） | [表示拡張(文字強調)](plugin/plugin_viewextend.md) |
| カウンター・トリガー | 言葉を数えて、テンプレートや OBS に出したり、条件で動作させたりできます（v3.0.8） | [カウンター・トリガー](plugin/plugin_countertrigger.md) |
| オフライン翻訳（無料） | PC の中だけで動く翻訳エンジンです | [オプション設定](startup/startup_option.md#offline-translation) |
| オフライン音声認識 | 軽量モデル（v3.0.10）と句読点の付与（v3.0.11）を選べます | [音声認識できないとき](startup/startup_asr.md#offline-recognition) |
| ブラウザ音声認識 | マイクの選び直し・入力レベル・2 本同時の認識ができます | [音声認識できないとき](startup/startup_asr.md#browser-recognition) |
| モデルの保存先 | ダウンロードするモデルの置き場所を選び、不要なものを消せます | [モデルの保存先と管理](startup/startup_option.md#model-storage) |
| アクセス状況 | 字幕の受け口に来た要求の許可・拒否と理由が見られます（v3.0.9） | [アクセス状況](startup/startup_option.md#access-log) |
| AIアシスタント（MCP） | Claude などの AI クライアントからゆかコネの状態確認や操作ができます | [MCP からゆかコネを操作する](tech/tech_api_neo.md#mcp) |
| 読み上げ | Irodori-TTS、VoiSona の感情スタイル、読み上げの教育（教育／忘却コマンド）などが増えました | [読み上げ](plugin/plugin_playvoice.md) |
| Twitch・cluster | Twitch のチャット翻訳（v3.0.9）、cluster のコメント受信（v3.0.12） | [Twitch](plugin/plugin_twitch.md) / [clusterチャット転送](plugin/plugin_clustertransfer.md) |
| 表の使い方 | 正規表現・色付け・ルビ・辞書の表で、並べ替え・絞り込み・セクションが使えます（v3.0.11） | [正規表現](plugin/plugin_regexp.md) |

細かい変更は [更新履歴](../qa/history.md) をご覧ください。

## 目的から探す

* **英語字幕を出したい** → [無料で英語翻訳を出す](cs/cs_en.md) / [支援版で高品質翻訳](cs/cs_en_sp.md)
* **配信に載せたい** → [配信ソフトに取り込む](cs/cs_import_obs.md) / [OBSできれいに出す](cs/cs_obs.md)
* **VRChat で使いたい** → [VRChatのチャットとつなぐ](cs/cs_vrchat.md)
* **読み上げさせたい** → [読み上げ](plugin/plugin_playvoice.md)
* **認識がおかしい** → [音声認識できないとき](startup/startup_asr.md) / [辞書](plugin/plugin_dictionary.md)
* **設定項目の意味を知りたい** → [標準設定項目](startup/startup_basic.md) / [オプション設定](startup/startup_option.md)
* **AI に読ませたい** → [AIエージェント向け 検索インデックス](ai_docs/INDEX.md)
