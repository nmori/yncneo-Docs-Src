# スクリーンショット撮り直しTODO

このファイルはドキュメント作成者向けのメモです。`docs/` の外に置いてあるため、サイトには公開されません。

各ページの該当箇所にも `<!-- TODO: ... -->` / `<!-- TODO(screenshot): ... -->` のコメントを入れてあります。
ドキュメントは 2026-09 に v2.3 / v3.0 へ分けました。**撮り直しの対象は `docs/v3.0/` 側だけ**です（`docs/v2.3/` は v2.3 時点の画面で凍結しているので、そのままにしてください）。

## 撮り直しが必要（内容が変わっている）

| 画像 | 撮影時点 | 撮り直しの理由 | 使っているページ |
|:--|:--|:--|:--|
| `docs/v3.0/startup/images/startup_menu1.png` | v2.3.59 | 左メニューの構成が変わった（グループ名・項目名） | v3.0/startup/startup_basic.md |
| `docs/v3.0/startup/images/startup_menu3.png` | v2.3.59 | レイアウトの選択肢が増えた（36種） | v3.0/startup/startup_basic.md |
| `docs/v3.0/startup/images/startup_menu4.png` | v2.3.59 | 翻訳エンジンに Parapper翻訳 が追加された | v3.0/startup/startup_basic.md |
| `docs/v3.0/startup/images/startup_menu5.png` | v2.3.59 | 音声認識に Parapper / Windows11音声認識 が追加された（計9種） | v3.0/startup/startup_basic.md |
| `docs/v3.0/startup/images/startup_menu9.png` | v2.3.59 | クイックボタンの並びが変わった（「支援状態」「？」が無くなり、手動入力枠・マニュアル・プラグイン一覧が入った） | v3.0/startup/startup_basic.md |
| `docs/v3.0/startup/images/startup_menu11.png` | v2.3.59 | 簡易設定の項目が11件になった | v3.0/startup/startup_basic.md |
| `docs/v3.0/startup/images/startup_option3.png` | v2.3.59 | 翻訳APIオプションのラベル文言が変わった | v3.0/startup/startup_option.md |
| `docs/v3.0/startup/images/startup_option4.png` | v2.3.59 | ブラウザのオプションに項目が増えた | v3.0/startup/startup_option.md |
| `docs/v3.0/startup/images/startup_option6.png` | v2.3.59 | Gemini の新モデルと Parapper の Port 欄が増えた | v3.0/startup/startup_option.md |
| `docs/v3.0/startup/images/startup_layout1.png` ～ `startup_layout6.png` | 2022-08 | 4年前の画面 | v3.0/startup/startup_layout.md |
| `docs/v3.0/startup/images/startup_layout_p01.png` ～ `startup_layout_p15.png` | 2022-09 | 4年前。わんコメ側のテンプレートも更新されている可能性がある | v3.0/startup/startup_layout.md |
| `docs/v3.0/startup/images/plugin_gas_p3.png` ～ `plugin_gas_p10.png` | 2022-10 | Google Apps Script の管理画面UIが変わっている | v3.0/startup/startup_gas.md |

## 未撮影（画像そのものが無い）

| 必要な画像 | 内容 | 使うページ |
|:--|:--|:--|
| `docs/v3.0/startup/images/startup_layout7.png` | レイアウト「ショート」の表示例 | v3.0/startup/startup_layout.md |
| `docs/v3.0/startup/images/startup_layout8.png` | レイアウト「ショート(動き控えめ)」の表示例 | v3.0/startup/startup_layout.md |
| `docs/v3.0/plugin/images/plugin_talkhistory_p1.png` | 会話の記録：有効化 | v3.0/plugin/plugin_talkhistory.md |
| `docs/v3.0/plugin/images/plugin_replacefwords_p1.png` | 不適切語の置換：有効化 | v3.0/plugin/plugin_replacefwords.md |
| `docs/v3.0/plugin/images/plugin_dynamickeeptime_p1.png` | 表示時間の自動調整：有効化 | v3.0/plugin/plugin_dynamickeeptime.md |

* 未出荷プラグイン（`plugin_MoviePickup.md` / `plugin_captioner.md`）の画像は不要です。配布していないため撮影できません。

## 撮り直したあとの作業

1. 上の表のパスにそのファイル名で置きます。
2. ページ内の `<!-- TODO: ... -->` コメントと、その下の `<!-- ![...](...) -->` のコメント記号を外します。
3. このファイルの該当行を消します。

> **画像は補助という前提で書いています。**
> 本文は、スクリーンショットが無くても設定にたどり着けるように書いてあります（画面名 → メニュー項目 → 項目ラベルの順）。撮り直しは急ぎではありません。

## v3.0 で新しく撮る必要があるもの（2026-09 追加）

| 必要な画像 | 内容 | 使うページ |
|:--|:--|:--|
| `docs/v3.0/startup/images/startup_cockpit.png` | コックピット画面（いま出ている字幕・表示テスト・OBSのアドレス） | v3.0/startup/startup_basic.md |
| `docs/v3.0/startup/images/startup_design_chips.png` | 「見た目を調整する」を押した状態のボタン列（テンプレ/文字/色/配置/タイミング/表示内容） | v3.0/startup/startup_basic.md |
| `docs/v3.0/cs/images/cs_startup_wizard1.png` | セットアップ案内 ステップ 1/3（あなたのこと・やりたいこと） | v3.0/cs/cs_startup.md |
| `docs/v3.0/cs/images/cs_startup_wizard2.png` | セットアップ案内 ステップ 2/3（声を入れる） | v3.0/cs/cs_startup.md |
| `docs/v3.0/cs/images/cs_startup_wizard3.png` | セットアップ案内 ステップ 3/3（配信ソフトに出す） | v3.0/cs/cs_startup.md |
| `docs/v3.0/startup/images/startup_migrate_v23.png` | 「設定保存・復元」の v2.3設定を移行 ボタンと確認ダイアログ | v3.0/startup/startup_profile.md |
| `docs/v3.0/startup/images/startup_layout_extpack.png` | ext-pack のテンプレート一覧（アイコン付き） | v3.0/startup/startup_layout.md |
| `docs/v3.0/plugin/images/v30/playvoice_settings_3.png`（撮り直し） | 読み上げと出力：「パラメータを Jev に調整させる」／「強さ」の欄が写っていない。HEAD でビルドし、Jev を使える状態（本体の呼び出し口あり）でスクロールして撮る（beta 24 で追加） | v3.0/plugin/plugin_playvoice.md |

## 撮影済み（2026-09-22、プラグインの試験用ハーネスで撮影）

プラグインの設定画面は、ソース側の撮影ハーネスで撮って `docs/v3.0/plugin/images/v30/` に置きました（127 枚）。
撮り直すときは同じ手順で撮れます。

* 共通の設定画面: `Machan2017/tools/PluginSettingsProbe`（`<hostBin> <plugin.dll> <outDir> light`）
  * ホストは **Debug ビルド**の `YNC_Neo/bin/x64/Debug` を使う（Release は難読化されていてリソースが引けない）
  * 出力先がそのまま設定フォルダになるので、見本の規則ファイル（`<Plugin_Tag>_rule.config` など）を先に置くと、表に中身が入った絵になる
* 読み上げ: `Plugin_PlayVoice/tools/PaletteProbe`（ボイス一覧 JSON を渡すとパレットと詳細設定 7 ページを撮る）

**公開していない画面**（説明文やフォルダ欄に設定フォルダの場所＝ユーザー名が入る、または撮影環境の情報が写るため）:
MIDI 入力「割り当て」、OBS 連携 WSv4「シーン切り替え」、Python 連携、わんコメ連携「わんコメから受ける」、更新通知、MTG カード「OBS へ渡す」。
実機で、人に見せてよいフォルダ構成の PC から撮ってください。

置き換えた項目（旧 TODO）:
| `docs/v3.0/plugin/images/plugin_playvoice_p2.png` `p5.png` `p7.png` `p8.png` | v2.3系 | 読み上げ連携の設定画面が WPF に変わった（ボイスパレット / 6ページの詳細設定 / 条件ルールの一覧+詳細）。本文からは参照を外してある | v3.0/plugin/plugin_playvoice.md |
| `docs/v3.0/plugin/images/plugin_niconama_p1.png` | ニコニコ生放送連携の設定画面 | v3.0/plugin/plugin_niconama.md |
| `docs/v3.0/plugin/images/plugin_infographics_p1.png` | InfoGraphics の設定画面 | v3.0/plugin/plugin_infographics.md |
| `docs/v3.0/plugin/images/plugin_talkhistory_p2.png` | 会話の記録：設定画面 | v3.0/plugin/plugin_talkhistory.md |
| `docs/v3.0/plugin/images/plugin_replacefwords_p2.png` | 不適切語の置換：設定画面 | v3.0/plugin/plugin_replacefwords.md |
| `docs/v3.0/plugin/images/plugin_dynamickeeptime_p2.png` | 表示時間の自動調整：設定画面 | v3.0/plugin/plugin_dynamickeeptime.md |
| `docs/v3.0/plugin/images/plugin_dynamickeeptime_graph.png` | 文字数と表示時間の関係グラフ | v3.0/plugin/plugin_dynamickeeptime.md |
| `docs/v3.0/plugin/images/plugin_playvoice_palette.png` | ボイスパレット（検索・エンジン絞り込み・お気に入り） | v3.0/plugin/plugin_playvoice.md |
| `docs/v3.0/plugin/images/plugin_playvoice_settings.png` | 詳細設定のホーム | v3.0/plugin/plugin_playvoice.md |
| `docs/v3.0/plugin/images/plugin_playvoice_rules.png` | 詳細設定の条件ルール | v3.0/plugin/plugin_playvoice.md |
| `docs/v3.0/plugin/images/plugin_playvoice_preset.png` | 設定プリセットの作成 | v3.0/plugin/plugin_playvoice.md |
| `docs/v3.0/plugin/images/plugin_ux_common.png` | 新しいプラグイン設定画面（WPF 共通土台）の見本 | v3.0/plugin/enabled.md ほか |
| `docs/v3.0/plugin/images/plugin_ux_table.png` | 新しい設定画面の規則の表（列幅が内容に合わせて配分されるもの） | v3.0/plugin/plugin_regexp.md ほか |

## v3.0.13 までの更新で必要になったもの（2026-11 追加）

ページ内の `<!-- TODO(screenshot): ... -->` と対応しています。

| 必要な画像 | 内容 | 使うページ |
|:--|:--|:--|
| `docs/v3.0/startup/images/startup_cockpit.png` | 操作パネル → いまの状態（中央に字幕ログ、右に選ぶ欄、下に機能ボタン） | v3.0/startup/startup_basic.md |
| `docs/v3.0/startup/images/startup_live_settings.png` | 操作パネル → ライブ設定（プラグインごとの欄と「反映」「接続」） | v3.0/startup/startup_basic.md |
| `docs/v3.0/startup/images/startup_menu3.png`（撮り直し） | 字幕デザイン → デザイン（プレビュー・タイルの一覧・右の分類のタブ） | v3.0/startup/startup_basic.md |
| `docs/v3.0/startup/images/startup_design_chips.png` | 「詳しい調整」を押した状態のボタン列 | v3.0/startup/startup_basic.md |
| `docs/v3.0/startup/images/startup_layout_citypop.png` ほか 8 枚 | 新しいテンプレートの表示例（citypop / avatar / game / counter / dopamine / list2 / retro / options） | v3.0/startup/startup_layout.md |
| オフライン翻訳（無料）の欄 | APIキーの設定のオフライン翻訳の欄（同意チェック・状態・フォルダを開く） | v3.0/startup/startup_option.md |
| モデルの保存先と管理 | 保存先の変更／既定に戻す、置き場ごとの一覧 | v3.0/startup/startup_option.md |
| API/Webサーバ設定 | Web許可ホスト・トークンのコピー／作り直す・アクセス状況（IP と端末名はぼかす） | v3.0/startup/startup_option.md |
| ブラウザ音声認識の画面 | ランプ・メーター・第1入力／第2入力・2本同時 | v3.0/startup/startup_asr.md |
| オフライン認識の ⚙ 設定 | モデル＋取得・句読点・GPU高速化 | v3.0/startup/startup_asr.md |
| MCP「AI クライアントの設定」ページ | 設定例のコピー | v3.0/tech/tech_api_neo.md |
| `docs/v3.0/plugin/images/v30/viewextend_emphasis_1.png` | 文字強調（表に 2〜3 行、右の編集欄を開いた状態） | v3.0/plugin/plugin_viewextend.md |
| `docs/v3.0/plugin/images/v30/viewextend_usercss_1.png` | ユーザCSS のページ | v3.0/plugin/plugin_viewextend.md |
| `docs/v3.0/plugin/images/v30/viewextend_1.png`（撮り直し） | 画像差し替えのページ（旧「スタンプの設定」窓のまま） | v3.0/plugin/plugin_viewextend.md |
| `regexp_1.png` / `regexpcolor_1.png` / `ruby_1.png`（撮り直し） | セクションの帯・絞り込み・並べ替え（⇅ / 並べ替えの帯）が写った状態 | v3.0/plugin/plugin_regexp*.md, plugin_ruby.md |
| `docs/v3.0/plugin/images/v30/countertrigger_1.png` | カウンター・トリガーのルールのページ（見本の行） | v3.0/plugin/plugin_countertrigger.md |
| `twitch_4.png` / `twitch_5.png` | Twitch のチャット翻訳／読み上げの教育のページ | v3.0/plugin/plugin_twitch.md |
| `clustertransfer_1.png`（撮り直し）/ `_2` / `_3` | cluster の送信／受信／接続タブ | v3.0/plugin/plugin_clustertransfer.md |
| `playvoice_settings_irodori.png` / `playvoice_settings_export.png` | 読み上げの Irodori-TTS の欄／音声ファイルの生成 | v3.0/plugin/plugin_playvoice.md |
| `vroverlay_1.png`（撮り直し） | VRオーバーレイの新しい項目 | v3.0/plugin/plugin_vroverlay.md |
| `playsound_1.png`（撮り直し）/ `playsound_2.png` | 効果音の 1 段の表と詳細パネル／再生のページ | v3.0/plugin/plugin_playsound.md |
