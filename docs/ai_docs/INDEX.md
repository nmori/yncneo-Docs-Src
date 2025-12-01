# ゆかコネNEO AI支援ドキュメント

> このフォルダは、AIアシスタントがユーザーを効率的にサポートするためのクイックリファレンスです。
> 詳細な手順や画像付き解説は [公式ドキュメント](https://nmori.github.io/yncneo-Docs/) を参照してください。

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
- [QUICKSTART_SCENARIOS.md #Scenario 1](./QUICKSTART_SCENARIOS.md#scenario-1-basic-streaming-setup-obs--caption)
- 公式: [OBSできれいに出す](../cs/cs_obs.md) / [配信ソフトに取り込む](../cs/cs_import_obs.md)

---

### 2. VRChatで字幕を表示したい

**必要な設定:**
1. Plugin_VRCHAT_OSC を有効化
2. VRChat側でOSCを有効化（Action Menu → Options → OSC）
3. 送信ポート: 9000（VRChat固定）

**参照:**
- [QUICKSTART_SCENARIOS.md #Scenario 3](./QUICKSTART_SCENARIOS.md#scenario-3-vrchat-caption-display)
- [PLUGINS_REFERENCE.md #Plugin_VRCHAT_OSC](./PLUGINS_REFERENCE.md#plugin_vrchat_osc---vrchat-osc連携)
- 公式: [VRChat OSC連携](../plugin/plugin_vrchat_osc.md) / [VRChatのチャットとつなぐ](../cs/cs_vrchat.md)

---

### 3. Discordと連携したい

**2つの方法:**

| 方法 | 特徴 | 設定難易度 |
|-----|------|-----------|
| Discord BOT | 双方向通信、コマンド受信可能 | やや複雑 |
| Discord Webhook | 一方向送信のみ、簡単設定 | 簡単 |

**参照:**
- [QUICKSTART_SCENARIOS.md #Scenario 4](./QUICKSTART_SCENARIOS.md#scenario-4-discord-bot-integration)
- [FAQ_TROUBLESHOOTING.md #Discord連携](./FAQ_TROUBLESHOOTING.md#8-discord連携関連)
- 公式: [Discord BOT連携](../plugin/plugin_dicord.md) / [Discord Webhook連携](../plugin/plugin_dicordwebhook.md)

---

### 4. 読み上げ（TTS）を使いたい

**対応エンジン:**
- SAPI5 (Windows標準)
- VOICEVOX / COEIROINK（要事前起動）
- 棒読みちゃん
- AssistantSeika経由（VOICEROID等）

**参照:**
- [QUICKSTART_SCENARIOS.md #Scenario 5](./QUICKSTART_SCENARIOS.md#scenario-5-tts-voice-output)
- [PLUGINS_REFERENCE.md #Plugin_PlayVoice](./PLUGINS_REFERENCE.md#plugin_playvoice---読み上げプラグイン)
- 公式: [読み上げ](../plugin/plugin_playvoice.md) / [棒読みちゃん連携](../plugin/plugin_bouyomi.md)

---

### 5. 翻訳が動かない/設定したい

**確認ポイント:**
1. 翻訳エンジンが「TransOFF(23)」になっていないか
2. 有料エンジンはAPIキー設定が必要
3. 共用サーバは月間文字数制限あり

**無料で使える翻訳:**
- Google Apps Script (GAS) - 自作スクリプト必要
- 共用翻訳サーバ - 月5,000文字目安

**参照:**
- [SETTINGS_REFERENCE.md #Translation Settings](./SETTINGS_REFERENCE.md#translation-settings)
- [FAQ_TROUBLESHOOTING.md #翻訳機能関連](./FAQ_TROUBLESHOOTING.md#3-翻訳機能関連)
- 公式: [無料で英語翻訳を出す](../cs/cs_en.md) / [GASの設定](../startup/startup_gas.md)

---

## ドキュメント構成

### ai_docs フォルダ内ファイル

| ファイル | 内容 | 用途 |
|---------|------|------|
| `INDEX.md` | このファイル | 全体案内・ユースケース別ガイド |
| `QUICKSTART_SCENARIOS.md` | ユースケース別設定例 | 具体的な設定パターン |
| `SETTINGS_REFERENCE.md` | 設定項目リファレンス | user.config の全設定項目 |
| `PLUGINS_REFERENCE.md` | プラグインGUIリファレンス | 各プラグインの設定画面詳細 |
| `YNC_NEO_GUI_REFERENCE.md` | 本体GUIリファレンス | メイン画面の操作・設定 |
| `FAQ_TROUBLESHOOTING.md` | FAQ・トラブル対応 | よくある質問と解決方法 |

### 公式ドキュメント（mkdocs）主要セクション

| セクション | パス | 内容 |
|-----------|------|------|
| カンタンな使い方 | `guide/`, `cs/` | 画像付きチュートリアル |
| 設定について | `startup/` | 各設定画面の詳細解説 |
| プラグイン | `plugin/` | 各プラグインの詳細 |
| 困ったときは | `qa/` | FAQ、トラブルシューティング |
| 技術者向け | `tech/` | API、起動オプション |

---

## AI支援時の推奨フロー

```
1. ユーザーの質問を分類
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
