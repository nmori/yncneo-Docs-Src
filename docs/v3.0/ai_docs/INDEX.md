# ゆかコネNEO AI支援ドキュメント

<!-- version-banner -->
!!! info ""
    ゆかコネNEO **v3.0** のドキュメントです。v2.3 をお使いの方は [v2.3 版のこのページ](../../v2.3/ai_docs/INDEX.md) を、違いを知りたい方は [v2.3 から v3.0 への移行](../../mig/mig_neo_v3.0.md) をご覧ください。


> このフォルダは、AIアシスタントがユーザーを効率的にサポートするためのクイックリファレンスです。
> 詳細な手順や画像付き解説は [公式ドキュメント](https://nmori.github.io/yncneo-Docs/) を参照してください。

!!! danger "AI アシスタントへ：まずバージョンを確認してください"
    ゆかコネNEO には **v2.3** と **v3.0** があり、**画面の構成と設定の持ち方が違います**。
    ユーザーがどちらを使っているか分からないまま v3.0 の手順を案内すると、
    「書いてあるとおりに操作しても、その項目が無い」という結果になります。

    確認の仕方：ゆかコネNEO のタイトルバーに `YukarinetteConnector NEO v◯.◯.◯` と出ています。

    * `2.3` で始まる → **v2.3 のドキュメント**（`/v2.3/` 配下）を参照してください
    * `3.0` で始まる → このドキュメント（`/v3.0/` 配下）が対象です

    v2.3 と v3.0 の差分は [v2.3 → v3.0 の移行](../../mig/mig_neo_v3.0.md) にまとまっています。

## v3.0 で変わった主なところ（AI 向け要約）

| 変更点 | 影響 |
|:--|:--|
| 実行基盤が .NET Framework 4.8 → **.NET 10**（自己完結型、約 2.4GB） | ランタイムの導入は不要。**v2.3 向けにビルドされたプラグインは読み込めない** |
| 設定の保存先フォルダ名が変わった | 初回起動で自動取り込み。意味が変わった項目は「設定保存・復元」→**「v2.3設定を移行」**が必要 |
| 左メニューから「母国語と言語の表示」「フォント設定と配置」「色」が消えた | **「レイアウトデザインの選択」→「見た目を調整する」**の中（テンプレ/文字/色/配置/タイミング/表示内容） |
| 「OBSからの参照設定」が左メニューに独立 | OBS へ貼るアドレスはここ |
| **コックピット**（左メニュー先頭）が追加 | いま出ている字幕・表示テスト・OBS のアドレス |
| **「設定をさがす」**（左メニューの検索欄）が追加 | 項目名 + Enter でその設定へ移動。「項目が見つからない」への第一の回答 |
| 初回案内が **3 ステップのウィザード**に | v2.3 の 7 手順の説明は当てはまらない |
| 内蔵ブラウザが CefSharp → **WebView2** | WebView2 ランタイムが必要。ログイン状態は入り直しになることがある |
| プラグインの設定画面 36 本が **WPF の共通土台**へ | 下書き方式（適用／破棄／続ける）。表示言語で出し分け |
| VRChat OSC のシナリオ原稿で **TEXT 行と素の行の送り先が入れ替わった** | v2.3 の台本はエラーを出さずに逆に動く。移行で書き直しが要る |
| 翻訳エンジンから **Google 無料 / IBM Watson** が消えた | 選んでいた枠は移行で「翻訳しない」になる |
| ext-pack の 3 本（`ListAddTime` / `SmartScroll` / `Smart_Vue`）を削除、40 本を作り直し | レイアウトの選び直しが要る |
| 起動オプション **`/pcore`** を追加 | P コアだけで動かす（既定 OFF） |


---

## ユースケース別ガイド

### やりたいことから探す

| やりたいこと | 参照ドキュメント | 公式ドキュメント |
|-------------|-----------------|-----------------|
| **初めて使う** | [QUICKSTART_SCENARIOS.md](./QUICKSTART_SCENARIOS.md) | [5分クイックスタート](../guide/quickstart.md) |
| **設定項目を調べる** | [SETTINGS_REFERENCE.md](./SETTINGS_REFERENCE.md) | [標準設定項目](../startup/startup_basic.md) |
| **プラグインを設定する** | [PLUGINS_REFERENCE.md](./PLUGINS_REFERENCE.md) | [プラグイン一覧](../plugin/index.md) |
| **GUI操作を知りたい** | [YNC_NEO_GUI_REFERENCE.md](./YNC_NEO_GUI_REFERENCE.md) | [標準設定項目](../startup/startup_basic.md) |
| **トラブル解決** | [FAQ_TROUBLESHOOTING.md](./FAQ_TROUBLESHOOTING.md) | [こんなときは](../qa/troubleshooting.md) |

---

## 主要ユースケース別クイックガイド

### 1. 配信で字幕を表示したい

**必要な設定:**
1. 音声認識ソース選択（Chrome/Edge推奨）
2. 翻訳言語・エンジン設定
3. レイアウト選択（「多言語」が汎用的）
4. OBSへの取り込み

**参照:**
- [QUICKSTART_SCENARIOS.md #Scenario 1](./QUICKSTART_SCENARIOS.md#sc1)
- 公式: [OBSできれいに出す](../cs/cs_obs.md) / [配信ソフトに取り込む](../cs/cs_import_obs.md)

---

### 2. VRChatで字幕を表示したい

**必要な設定:**
1. Plugin_VRCHAT_OSC を有効化
2. VRChat側でOSCを有効化（Action Menu → Options → OSC）
3. 送信ポート: 9000（VRChat固定）

**参照:**
- [QUICKSTART_SCENARIOS.md #Scenario 3](./QUICKSTART_SCENARIOS.md#sc3)
- [PLUGINS_REFERENCE.md #Plugin_VRCHAT_OSC](./PLUGINS_REFERENCE.md#plugin_vrchat_osc)
- 公式: [VRChat OSC連携](../plugin/plugin_vrchat_osc.md) / [VRChatのチャットとつなぐ](../cs/cs_vrchat.md)

---

### 3. Discordと連携したい

**2つの方法:**

| 方法 | 特徴 | 設定難易度 |
|-----|------|-----------|
| Discord BOT | 双方向通信、コマンド受信可能 | やや複雑 |
| Discord Webhook | 一方向送信のみ、簡単設定 | 簡単 |

**参照:**
- [QUICKSTART_SCENARIOS.md #Scenario 4](./QUICKSTART_SCENARIOS.md#sc4)
- [FAQ_TROUBLESHOOTING.md #Discord連携](./FAQ_TROUBLESHOOTING.md#faq-discord)
- 公式: [Discord BOT連携](../plugin/plugin_dicord.md) / [Discord Webhook連携](../plugin/plugin_dicordwebhook.md)

---

### 4. 読み上げ（TTS）を使いたい

**対応エンジン:**
- SAPI5 (Windows標準)
- VOICEVOX / COEIROINK（要事前起動）
- 棒読みちゃん
- AssistantSeika経由（VOICEROID等）

**参照:**
- [QUICKSTART_SCENARIOS.md #Scenario 5](./QUICKSTART_SCENARIOS.md#sc5)
- [PLUGINS_REFERENCE.md #Plugin_PlayVoice](./PLUGINS_REFERENCE.md#plugin_playvoice)
- 公式: [読み上げ](../plugin/plugin_playvoice.md) / [棒読みちゃん連携](../plugin/plugin_bouyomi.md)

---

### 5. 翻訳が動かない/設定したい

**確認ポイント:**
1. 翻訳エンジンが「OFF（翻訳しない）」になっていないか（**ID28**です。ID23はAnthropic Claude）
2. 有料エンジンはAPIキー設定が必要
3. 共用サーバは月間文字数制限あり

**無料で使える翻訳:**
- Google Apps Script (GAS) - 自作スクリプト必要
- 共用翻訳サーバ - 月5,000文字目安

**参照:**
- [SETTINGS_REFERENCE.md #Translation Settings](./SETTINGS_REFERENCE.md#translation-settings)
- [FAQ_TROUBLESHOOTING.md #翻訳機能関連](./FAQ_TROUBLESHOOTING.md#faq-translate)
- 公式: [無料で英語翻訳を出す](../cs/cs_en.md) / [GASの設定](../startup/startup_gas.md)

---

## ドキュメント構成

### ai_docs フォルダ内ファイル

| ファイル | 内容 | 用途 |
|---------|------|------|
| `INDEX.md` | このファイル | 全体案内・ユースケース別ガイド |
| `QUICKSTART_SCENARIOS.md` | ユースケース別設定例 | 具体的な設定パターン |
| `SETTINGS_REFERENCE.md` | 設定項目リファレンス | 外部から設定できる項目 |
| `PLUGINS_REFERENCE.md` | プラグインGUIリファレンス | 各プラグインの設定画面詳細 |
| `YNC_NEO_GUI_REFERENCE.md` | 本体GUIリファレンス | メイン画面の操作・設定 |
| `FAQ_TROUBLESHOOTING.md` | FAQ・トラブル対応 | よくある質問と解決方法 |

### 公式ドキュメント（mkdocs）主要セクション

| セクション | パス | 内容 |
|-----------|------|------|
| カンタンな使い方 | `v3.0/guide/`, `v3.0/cs/` | 画像付きチュートリアル |
| 設定について | `v3.0/startup/` | 各設定画面の詳細解説 |
| プラグイン | `v3.0/plugin/` | 各プラグインの詳細 |
| 困ったときは | `v3.0/qa/` | FAQ、トラブルシューティング |
| 技術者向け | `v3.0/tech/` | API、起動オプション |
| バージョン移行 | `mig/` | 版ごとの移行手順（v2.3→v3.0 は `mig/mig_neo_v3.0.md`） |

!!! Info "URL の構成"
    2026-09 に v2.3 / v3.0 でドキュメントを分けました。
    分ける前の URL（`/startup/...`、`/plugin/...`）は **v3.0 へ転送**されます。
    v2.3 の内容は `/v2.3/...` にあります。

---

## AI支援時の推奨フロー

```
0. 【最初に】ユーザーのバージョンを確認する（v2.3 / v3.0 で画面が違う）
   └─ 不明なら「タイトルバーの v◯.◯.◯ を教えてください」と聞く

1. ユーザーの質問を分類
   ├─ 「設定項目が見つからない」 → まず「設定をさがす」(左メニューの検索欄) を案内
   ├─ 初期設定・基本操作 → QUICKSTART_SCENARIOS.md + 公式guide/
   ├─ 特定の設定値を知りたい → SETTINGS_REFERENCE.md
   ├─ プラグイン設定 → PLUGINS_REFERENCE.md + 公式plugin/
   ├─ 画面操作がわからない → YNC_NEO_GUI_REFERENCE.md + 公式startup/
   └─ 動かない・エラー → FAQ_TROUBLESHOOTING.md + 公式qa/

2. ai_docs で概要・設定値を確認

3. 詳細な手順が必要な場合は公式ドキュメントを案内
```

---

## 関連リンク

- **公式ドキュメント**: https://nmori.github.io/yncneo-Docs/
- **公式サイト**: https://machanbazaar.com/
- **ダウンロード (BOOTH)**: https://booth.pm/ja/items/3432494
- **FANBOX支援**: https://nao.fanbox.cc/plans
- **コミュニティ (Discord)**: 公式サイトから参加

---

## 更新履歴

- 2025-01: 初版作成、mkdocsとの関連付け追加
- v2.3.128 時点で全面見直し。GUI構成・翻訳エンジン一覧・APIポート番号を実装に合わせて修正
- 2026-09: ドキュメントを v2.3 / v3.0 に分離。v3.0 の変更点の要約と、バージョン確認の手順を追加
