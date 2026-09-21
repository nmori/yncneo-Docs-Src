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

## 目的から探す

* **英語字幕を出したい** → [無料で英語翻訳を出す](cs/cs_en.md) / [支援版で高品質翻訳](cs/cs_en_sp.md)
* **配信に載せたい** → [配信ソフトに取り込む](cs/cs_import_obs.md) / [OBSできれいに出す](cs/cs_obs.md)
* **VRChat で使いたい** → [VRChatのチャットとつなぐ](cs/cs_vrchat.md)
* **読み上げさせたい** → [読み上げ](plugin/plugin_playvoice.md)
* **認識がおかしい** → [音声認識できないとき](startup/startup_asr.md) / [辞書](plugin/plugin_dictionary.md)
* **設定項目の意味を知りたい** → [標準設定項目](startup/startup_basic.md) / [オプション設定](startup/startup_option.md)
* **AI に読ませたい** → [AIエージェント向け 検索インデックス](ai_docs/INDEX.md)
